---
title: 'Esercitazione: Integrazione di Azure Active Directory con FM:Systems | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e FM:Systems.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3a597d228f6c9234ec2fd2644ec3ac50b98f3b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="26b86-103">Esercitazione: Integrazione di Azure Active Directory con FM:Systems</span><span class="sxs-lookup"><span data-stu-id="26b86-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="26b86-104">Questa esercitazione descrive come integrare FM:Systems con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26b86-104">In this tutorial, you learn how to integrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26b86-105">L'integrazione di FM:Systems con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="26b86-105">Integrating FM:Systems with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="26b86-106">È possibile controllare in Azure AD chi può accedere a FM:Systems</span><span class="sxs-lookup"><span data-stu-id="26b86-106">You can control in Azure AD who has access to FM:Systems</span></span>
- <span data-ttu-id="26b86-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a FM:Systems con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b86-107">You can enable your users to automatically get signed-on to FM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="26b86-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="26b86-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="26b86-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26b86-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26b86-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="26b86-110">Prerequisites</span></span>

<span data-ttu-id="26b86-111">Per configurare l'integrazione di Azure AD con FM:Systems sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="26b86-111">To configure Azure AD integration with FM:Systems, you need the following items:</span></span>

- <span data-ttu-id="26b86-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b86-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26b86-113">Sottoscrizione di FM:Systems abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="26b86-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26b86-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="26b86-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26b86-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="26b86-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26b86-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="26b86-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26b86-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26b86-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26b86-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="26b86-118">Scenario description</span></span>
<span data-ttu-id="26b86-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="26b86-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26b86-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="26b86-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26b86-121">Aggiunta di FM:Systems dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="26b86-121">Adding FM:Systems from the gallery</span></span>
2. <span data-ttu-id="26b86-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b86-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-the-gallery"></a><span data-ttu-id="26b86-123">Aggiunta di FM:Systems dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="26b86-123">Adding FM:Systems from the gallery</span></span>
<span data-ttu-id="26b86-124">Per configurare l'integrazione di FM:Systems in Azure AD è necessario aggiungere FM:Systems dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="26b86-124">To configure the integration of FM:Systems into Azure AD, you need to add FM:Systems from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26b86-125">**Per aggiungere FM:Systems dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="26b86-125">**To add FM:Systems from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26b86-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="26b86-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="26b86-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="26b86-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="26b86-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="26b86-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="26b86-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="26b86-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="26b86-133">Nella casella di ricerca digitare **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="26b86-133">In the search box, type **FM:Systems**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="26b86-135">Nel pannello dei risultati selezionare **FM:Systems** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="26b86-135">In the results panel, select **FM:Systems**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="26b86-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b86-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="26b86-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FM:Systems mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="26b86-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26b86-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di FM:Systems corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b86-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FM:Systems is to a user in Azure AD.</span></span> <span data-ttu-id="26b86-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="26b86-140">In other words, a link relationship between an Azure AD user and the related user in FM:Systems needs to be established.</span></span>

<span data-ttu-id="26b86-141">Per stabilire la relazione di collegamento, in FM:Systems assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="26b86-141">In FM:Systems, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="26b86-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con FM:Systems è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="26b86-142">To configure and test Azure AD single sign-on with FM:Systems, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26b86-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="26b86-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="26b86-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26b86-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26b86-145">**[Creazione di un utente test di FM:Systems](#creating-an-fmsystems-test-user)**: per avere una controparte di Britta Simon in FM:Systems collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b86-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - to have a counterpart of Britta Simon in FM:Systems that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="26b86-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b86-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26b86-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="26b86-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="26b86-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b86-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="26b86-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="26b86-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="26b86-150">**Per configurare l'accesso Single Sign-On di Azure AD con FM:Systems, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="26b86-150">**To configure Azure AD single sign-on with FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="26b86-151">Nella pagina di integrazione dell'applicazione **FM:Systems** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="26b86-151">In the Azure portal, on the **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="26b86-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="26b86-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="26b86-155">Nella sezione **URL e dominio FM:Systems** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="26b86-155">On the **FM:Systems Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="26b86-157">Nella casella di testo **URL di risposta** digitare l'**URL di risposta** usando il criterio seguente: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="26b86-157">In the **Reply URL** textbox, type your FM:Systems **Reply URL**, type the URL using the following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="26b86-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="26b86-158">This value is not real.</span></span> <span data-ttu-id="26b86-159">è necessario aggiornare questo valore con l'URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="26b86-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="26b86-160">Per ottenere il valore contattare il [team di supporto di FM:Systems](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="26b86-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) to get this value.</span></span>
 
4. <span data-ttu-id="26b86-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="26b86-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="26b86-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="26b86-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="26b86-165">Per configurare l'accesso Single Sign-On sul lato **FM:Systems** è necessario inviare il file **XML metadati** scaricato al [team di supporto di FM:Systems](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="26b86-165">To configure single sign-on on **FM:Systems** side, you need to send the downloaded **Metadata XML** to [FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="26b86-166">L'applicazione viene configurata in modo che la connessione SAML SSO sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="26b86-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="26b86-167">Una volta completata l'abilitazione dell'accesso Single Sign-On per la sottoscrizione, si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="26b86-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="26b86-168">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="26b86-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="26b86-169">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="26b86-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="26b86-170">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26b86-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="26b86-171">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b86-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="26b86-172">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="26b86-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="26b86-174">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="26b86-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26b86-175">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="26b86-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="26b86-177">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="26b86-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="26b86-179">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="26b86-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="26b86-181">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="26b86-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="26b86-183">a.</span><span class="sxs-lookup"><span data-stu-id="26b86-183">a.</span></span> <span data-ttu-id="26b86-184">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26b86-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26b86-185">b.</span><span class="sxs-lookup"><span data-stu-id="26b86-185">b.</span></span> <span data-ttu-id="26b86-186">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="26b86-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="26b86-187">c.</span><span class="sxs-lookup"><span data-stu-id="26b86-187">c.</span></span> <span data-ttu-id="26b86-188">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="26b86-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="26b86-189">d.</span><span class="sxs-lookup"><span data-stu-id="26b86-189">d.</span></span> <span data-ttu-id="26b86-190">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="26b86-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="26b86-191">Creazione di un utente test di FM:Systems</span><span class="sxs-lookup"><span data-stu-id="26b86-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="26b86-192">In una finestra del Web browser accedere al sito aziendale di FM:Systems come amministratore.</span><span class="sxs-lookup"><span data-stu-id="26b86-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="26b86-193">Passare a **Amministrazione del sistema \> Gestisci sicurezza \> Utenti \> Elenco utenti**.</span><span class="sxs-lookup"><span data-stu-id="26b86-193">Go to **System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="26b86-194">![Amministrazione del sistema](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Amministrazione del sistema")</span><span class="sxs-lookup"><span data-stu-id="26b86-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="26b86-195">Fare clic su **Crea nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="26b86-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="26b86-196">![Creazione di un nuovo utente](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Creazione di un nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="26b86-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="26b86-197">Nella sezione **Crea utente** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="26b86-197">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="26b86-198">![Crea utente](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="26b86-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="26b86-199">a.</span><span class="sxs-lookup"><span data-stu-id="26b86-199">a.</span></span> <span data-ttu-id="26b86-200">Nelle caselle di testo **UserName** (Nome utente), **Password**, **Confirm Password** (Conferma password), **E-mail** (Indirizzo di posta elettronica) ed **Employee ID** (ID dipendente) digitare i dati di un account Azure Active Directory valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="26b86-200">Type the **UserName**, the **Password**, **Confirm Password**, **E-mail** and the **Employee ID** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="26b86-201">b.</span><span class="sxs-lookup"><span data-stu-id="26b86-201">b.</span></span> <span data-ttu-id="26b86-202">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="26b86-202">Click **Next**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="26b86-203">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b86-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="26b86-204">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="26b86-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FM:Systems.</span></span>

![Assegna utente][200] 

<span data-ttu-id="26b86-206">**Per assegnare Britta Simon a FM:Systems, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="26b86-206">**To assign Britta Simon to FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="26b86-207">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="26b86-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="26b86-209">Nell'elenco delle applicazioni selezionare **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="26b86-209">In the applications list, select **FM:Systems**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="26b86-211">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="26b86-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="26b86-213">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="26b86-213">Click **Add** button.</span></span> <span data-ttu-id="26b86-214">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="26b86-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="26b86-216">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="26b86-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="26b86-217">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="26b86-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26b86-218">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="26b86-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="26b86-219">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="26b86-219">Testing single sign-on</span></span>

<span data-ttu-id="26b86-220">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="26b86-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="26b86-221">Quando si fa clic sul riquadro FM:Systems nel pannello di accesso si accede automaticamente all'applicazione FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="26b86-221">When you click the FM:Systems tile in the Access Panel, you should get automatically signed-on to your FM:Systems application.</span></span>
<span data-ttu-id="26b86-222">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="26b86-222">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="26b86-223">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="26b86-223">Additional resources</span></span>

* [<span data-ttu-id="26b86-224">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26b86-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26b86-225">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26b86-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

