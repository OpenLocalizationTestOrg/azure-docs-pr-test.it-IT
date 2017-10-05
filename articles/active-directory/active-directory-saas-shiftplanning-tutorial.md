---
title: 'Esercitazione: Integrazione di Azure Active Directory con Humanity | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Humanity.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="d85cf-103">Esercitazione: integrazione di Azure Active Directory con Humanity</span><span class="sxs-lookup"><span data-stu-id="d85cf-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="d85cf-104">Questa esercitazione descrive come integrare Humanity con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d85cf-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d85cf-105">L'integrazione di Humanity con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d85cf-105">Integrating Humanity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d85cf-106">È possibile controllare in Azure AD chi può accedere a Humanity</span><span class="sxs-lookup"><span data-stu-id="d85cf-106">You can control in Azure AD who has access to Humanity</span></span>
- <span data-ttu-id="d85cf-107">È possibile abilitare gli utenti per l'accesso automatico a Humanity (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="d85cf-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d85cf-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d85cf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d85cf-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d85cf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d85cf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d85cf-110">Prerequisites</span></span>

<span data-ttu-id="d85cf-111">Per configurare l'integrazione di Azure AD con Humanity, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d85cf-111">To configure Azure AD integration with Humanity, you need the following items:</span></span>

- <span data-ttu-id="d85cf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d85cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d85cf-113">Sottoscrizione di Humanity abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d85cf-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d85cf-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d85cf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d85cf-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d85cf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d85cf-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d85cf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d85cf-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d85cf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d85cf-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d85cf-118">Scenario description</span></span>
<span data-ttu-id="d85cf-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d85cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d85cf-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d85cf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d85cf-121">Aggiunta di Humanity dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d85cf-121">Adding Humanity from the gallery</span></span>
2. <span data-ttu-id="d85cf-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d85cf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-the-gallery"></a><span data-ttu-id="d85cf-123">Aggiunta di Humanity dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d85cf-123">Adding Humanity from the gallery</span></span>
<span data-ttu-id="d85cf-124">Per configurare l'integrazione di Humanity in Azure AD, è necessario aggiungere Humanity dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d85cf-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d85cf-125">**Per aggiungere Humanity dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d85cf-125">**To add Humanity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d85cf-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d85cf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d85cf-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d85cf-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d85cf-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d85cf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d85cf-133">Nella casella di ricerca digitare **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-133">In the search box, type **Humanity**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="d85cf-135">Nel pannello dei risultati selezionare **Humanity** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d85cf-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d85cf-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d85cf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d85cf-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Humanity usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d85cf-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d85cf-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Humanity corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d85cf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span></span> <span data-ttu-id="d85cf-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Humanity.</span><span class="sxs-lookup"><span data-stu-id="d85cf-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span></span>

<span data-ttu-id="d85cf-141">Per stabilire la relazione di collegamento, in Humanity assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="d85cf-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d85cf-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Humanity, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="d85cf-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d85cf-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d85cf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d85cf-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d85cf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d85cf-145">**[Creazione di un utente di test di Humanity](#creating-a-humanity-test-user)**: per avere una controparte di Britta Simon in Humanity collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d85cf-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d85cf-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d85cf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d85cf-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d85cf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d85cf-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d85cf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d85cf-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Humanity.</span><span class="sxs-lookup"><span data-stu-id="d85cf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="d85cf-150">**Per configurare l'accesso Single Sign-On di Azure AD con Humanity, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d85cf-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="d85cf-151">Nella pagina di integrazione dell'applicazione **Humanity** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d85cf-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d85cf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="d85cf-155">Nella sezione **URL e dominio Humanity** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d85cf-155">On the **Humanity Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="d85cf-157">a.</span><span class="sxs-lookup"><span data-stu-id="d85cf-157">a.</span></span> <span data-ttu-id="d85cf-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://company.humanity.com/includes/saml/`.</span><span class="sxs-lookup"><span data-stu-id="d85cf-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="d85cf-159">b.</span><span class="sxs-lookup"><span data-stu-id="d85cf-159">b.</span></span> <span data-ttu-id="d85cf-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="d85cf-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d85cf-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d85cf-161">These values are not real.</span></span> <span data-ttu-id="d85cf-162">è necessario aggiornarli con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="d85cf-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d85cf-163">Per ottenere questi valori, contattare il [team di supporto di Humanity](https://www.humanity.com/support/).</span><span class="sxs-lookup"><span data-stu-id="d85cf-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="d85cf-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="d85cf-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="d85cf-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d85cf-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d85cf-168">Nella sezione **Configurazione di Humanity** fare clic su **Configura Humanity** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d85cf-169">Copiare l'**URL del servizio Single Sign-On SAML e l'URL di disconnessione** dalla **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d85cf-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="d85cf-171">In un'altra finestra del Web browser accedere al sito aziendale di **Humanity** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d85cf-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="d85cf-172">Nel menu in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="d85cf-173">![Amministratore](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="d85cf-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="d85cf-174">In **Integrazione** fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="d85cf-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d85cf-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="d85cf-176">Nella sezione **Single Sign-On** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d85cf-176">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d85cf-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d85cf-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="d85cf-178">a.</span><span class="sxs-lookup"><span data-stu-id="d85cf-178">a.</span></span> <span data-ttu-id="d85cf-179">Selezionare **Abilitato SAML**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="d85cf-180">b.</span><span class="sxs-lookup"><span data-stu-id="d85cf-180">b.</span></span> <span data-ttu-id="d85cf-181">Selezionare **Allow Password Login** (Consenti accesso tramite password).</span><span class="sxs-lookup"><span data-stu-id="d85cf-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="d85cf-182">c.</span><span class="sxs-lookup"><span data-stu-id="d85cf-182">c.</span></span> <span data-ttu-id="d85cf-183">Incollare il valore dell'**URL del servizio Single Sign-On SAML** nella casella di testo **SAML Issuer URL** (URL autorità di certificazione SAML).</span><span class="sxs-lookup"><span data-stu-id="d85cf-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="d85cf-184">d.</span><span class="sxs-lookup"><span data-stu-id="d85cf-184">d.</span></span> <span data-ttu-id="d85cf-185">Incollare il valore dell'**URL di disconnessione** nella casella di testo **Remote Logout URL** (URL disconnessione remota).</span><span class="sxs-lookup"><span data-stu-id="d85cf-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="d85cf-186">e.</span><span class="sxs-lookup"><span data-stu-id="d85cf-186">e.</span></span> <span data-ttu-id="d85cf-187">Aprire il certificato con codifica base 64 nel blocco note, copiarne il contenuto negli appunti e incollarlo nella casella di testo **Certificato X.509** .</span><span class="sxs-lookup"><span data-stu-id="d85cf-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="d85cf-188">Fare clic su **Salva impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="d85cf-189">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d85cf-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d85cf-190">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d85cf-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d85cf-191">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d85cf-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d85cf-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d85cf-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="d85cf-193">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d85cf-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d85cf-195">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d85cf-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d85cf-196">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d85cf-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d85cf-198">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d85cf-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d85cf-200">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d85cf-202">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d85cf-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d85cf-204">a.</span><span class="sxs-lookup"><span data-stu-id="d85cf-204">a.</span></span> <span data-ttu-id="d85cf-205">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d85cf-206">b.</span><span class="sxs-lookup"><span data-stu-id="d85cf-206">b.</span></span> <span data-ttu-id="d85cf-207">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d85cf-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d85cf-208">c.</span><span class="sxs-lookup"><span data-stu-id="d85cf-208">c.</span></span> <span data-ttu-id="d85cf-209">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d85cf-210">d.</span><span class="sxs-lookup"><span data-stu-id="d85cf-210">d.</span></span> <span data-ttu-id="d85cf-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="d85cf-212">Creazione di un utente di test di Humanity</span><span class="sxs-lookup"><span data-stu-id="d85cf-212">Creating a Humanity test user</span></span>

<span data-ttu-id="d85cf-213">Per consentire agli utenti di Azure AD di accedere a Humanity, è necessario effettuarne il provisioning in Humanity.</span><span class="sxs-lookup"><span data-stu-id="d85cf-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="d85cf-214">Nel caso di Humanity, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="d85cf-214">In the case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="d85cf-215">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d85cf-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d85cf-216">Accedere al sito aziendale di **Humanity** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d85cf-216">Log in to your **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="d85cf-217">Fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="d85cf-218">![Amministratore](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="d85cf-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="d85cf-219">Fare clic su **Personale**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="d85cf-220">![Personale](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Personale")</span><span class="sxs-lookup"><span data-stu-id="d85cf-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="d85cf-221">In **Actions** (Azioni) fare clic su **Add Employees** (Aggiungi dipendenti).</span><span class="sxs-lookup"><span data-stu-id="d85cf-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="d85cf-222">![Aggiungi dipendenti](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Aggiungi dipendenti")</span><span class="sxs-lookup"><span data-stu-id="d85cf-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="d85cf-223">Nella sezione **Aggiungi dipendenti** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d85cf-223">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d85cf-224">![Salvare i dipendenti](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Salvare i dipendenti")</span><span class="sxs-lookup"><span data-stu-id="d85cf-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="d85cf-225">a.</span><span class="sxs-lookup"><span data-stu-id="d85cf-225">a.</span></span> <span data-ttu-id="d85cf-226">Digitare il **nome**, il **cognome** e l'**indirizzo di posta elettronica** di un account di Azure Active Directory valido di cui si desidera eseguire il provisioning nelle relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="d85cf-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="d85cf-227">b.</span><span class="sxs-lookup"><span data-stu-id="d85cf-227">b.</span></span> <span data-ttu-id="d85cf-228">Fare clic su **Salva dipendenti**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="d85cf-229">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Humanity per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d85cf-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d85cf-230">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d85cf-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d85cf-231">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Humanity.</span><span class="sxs-lookup"><span data-stu-id="d85cf-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d85cf-233">**Per assegnare Britta Simon a Humanity, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d85cf-233">**To assign Britta Simon to Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="d85cf-234">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d85cf-236">Nell'elenco delle applicazioni selezionare **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-236">In the applications list, select **Humanity**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="d85cf-238">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d85cf-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d85cf-240">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-240">Click **Add** button.</span></span> <span data-ttu-id="d85cf-241">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d85cf-243">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d85cf-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d85cf-244">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d85cf-245">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d85cf-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d85cf-246">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d85cf-246">Testing single sign-on</span></span>

<span data-ttu-id="d85cf-247">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d85cf-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d85cf-248">Quando si fa clic sul riquadro Humanity nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Humanity.</span><span class="sxs-lookup"><span data-stu-id="d85cf-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span></span>
<span data-ttu-id="d85cf-249">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d85cf-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d85cf-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d85cf-250">Additional resources</span></span>

* [<span data-ttu-id="d85cf-251">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d85cf-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d85cf-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d85cf-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

