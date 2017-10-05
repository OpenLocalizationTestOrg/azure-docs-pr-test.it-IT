---
title: 'Esercitazione: Integrazione di Azure Active Directory con Intacct | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Intacct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c203b192b9da0d280cbd7f6c123219242ee4a3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="d3221-103">Esercitazione: Integrazione di Azure Active Directory con Intacct</span><span class="sxs-lookup"><span data-stu-id="d3221-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="d3221-104">Questa esercitazione descrive come integrare Intacct con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3221-104">In this tutorial, you learn how to integrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3221-105">L'integrazione di Intacct con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3221-105">Integrating Intacct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3221-106">È possibile controllare in Azure AD chi può accedere a Intacct</span><span class="sxs-lookup"><span data-stu-id="d3221-106">You can control in Azure AD who has access to Intacct</span></span>
- <span data-ttu-id="d3221-107">È possibile abilitare gli utenti per l'accesso automatico a Intacct (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3221-107">You can enable your users to automatically get signed-on to Intacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3221-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3221-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d3221-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3221-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3221-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d3221-110">Prerequisites</span></span>

<span data-ttu-id="d3221-111">Per configurare l'integrazione di Azure AD con Intacct, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3221-111">To configure Azure AD integration with Intacct, you need the following items:</span></span>

- <span data-ttu-id="d3221-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3221-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3221-113">Sottoscrizione di Intacct abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d3221-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3221-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d3221-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3221-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3221-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3221-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d3221-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3221-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3221-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3221-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d3221-118">Scenario description</span></span>
<span data-ttu-id="d3221-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d3221-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3221-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3221-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3221-121">Aggiunta di Intacct dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d3221-121">Adding Intacct from the gallery</span></span>
2. <span data-ttu-id="d3221-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3221-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-the-gallery"></a><span data-ttu-id="d3221-123">Aggiunta di Intacct dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d3221-123">Adding Intacct from the gallery</span></span>
<span data-ttu-id="d3221-124">Per configurare l'integrazione di Intacct in Azure AD, è necessario aggiungere Intacct dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d3221-124">To configure the integration of Intacct into Azure AD, you need to add Intacct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3221-125">**Per aggiungere Intacct dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d3221-125">**To add Intacct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3221-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d3221-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3221-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d3221-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3221-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d3221-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d3221-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d3221-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d3221-133">Nella casella di ricerca digitare **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="d3221-133">In the search box, type **Intacct**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="d3221-135">Nel pannello dei risultati selezionare **Intacct** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d3221-135">In the results panel, select **Intacct**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3221-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3221-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3221-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Intacct con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d3221-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d3221-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Intacct che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3221-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intacct is to a user in Azure AD.</span></span> <span data-ttu-id="d3221-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Intacct.</span><span class="sxs-lookup"><span data-stu-id="d3221-140">In other words, a link relationship between an Azure AD user and the related user in Intacct needs to be established.</span></span>

<span data-ttu-id="d3221-141">Per stabilire la relazione di collegamento, in Intacct assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="d3221-141">In Intacct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d3221-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Intacct, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3221-142">To configure and test Azure AD single sign-on with Intacct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3221-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d3221-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3221-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3221-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3221-145">**[Creazione di un utente di test di Intacct](#creating-an-intacct-test-user)**: per avere una controparte di Britta Simon in Intacct collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3221-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - to have a counterpart of Britta Simon in Intacct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3221-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3221-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3221-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d3221-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3221-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3221-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3221-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Intacct.</span><span class="sxs-lookup"><span data-stu-id="d3221-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="d3221-150">**Per configurare l'accesso Single Sign-On di Azure AD con Intacct, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d3221-150">**To configure Azure AD single sign-on with Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="d3221-151">Nella pagina di integrazione dell'applicazione **Intacct** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d3221-151">In the Azure portal, on the **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d3221-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d3221-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="d3221-155">Nella sezione **URL e dominio Intacct** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d3221-155">On the **Intacct Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="d3221-157">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="d3221-157">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="d3221-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="d3221-158">This value is not real.</span></span> <span data-ttu-id="d3221-159">è necessario aggiornare questo valore con l'URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="d3221-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="d3221-160">Per ottenere questo valore, contattare il [team di supporto di Intacct](https://us.intacct.com/support).</span><span class="sxs-lookup"><span data-stu-id="d3221-160">Contact [Intacct support team](https://us.intacct.com/support) to get this value.</span></span>

4. <span data-ttu-id="d3221-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="d3221-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="d3221-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d3221-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d3221-165">Nella sezione **Configurazione di Intacct** fare clic su **Configura Intacct** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="d3221-165">On the **Intacct Configuration** section, click **Configure Intacct** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d3221-166">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d3221-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="d3221-168">In un'altra finestra del Web browser accedere al sito aziendale di Intacct come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d3221-168">In a different web browser window, sign in to your Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="d3221-169">Fare clic sulla scheda **Company** (Azienda) e quindi su **Company Info** (Informazioni sull'azienda).</span><span class="sxs-lookup"><span data-stu-id="d3221-169">Click the **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="d3221-170">![Azienda](./media/active-directory-saas-intacct-tutorial/ic790037.png "Azienda")</span><span class="sxs-lookup"><span data-stu-id="d3221-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="d3221-171">Fare clic sulla scheda **Security** (Sicurezza) e quindi su **Edit** (Modifica).</span><span class="sxs-lookup"><span data-stu-id="d3221-171">Click the **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="d3221-172">![Sicurezza](./media/active-directory-saas-intacct-tutorial/ic790038.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="d3221-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="d3221-173">Nella sezione **Single sign on (SSO)** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d3221-173">In the **Single sign on (SSO)** section, perform the following steps:</span></span>

    <span data-ttu-id="d3221-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span><span class="sxs-lookup"><span data-stu-id="d3221-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="d3221-175">a.</span><span class="sxs-lookup"><span data-stu-id="d3221-175">a.</span></span> <span data-ttu-id="d3221-176">Selezionare **Abilita Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d3221-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="d3221-177">b.</span><span class="sxs-lookup"><span data-stu-id="d3221-177">b.</span></span> <span data-ttu-id="d3221-178">In **Identity provider type** (Tipo di provider di identità) selezionare **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="d3221-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="d3221-179">c.</span><span class="sxs-lookup"><span data-stu-id="d3221-179">c.</span></span> <span data-ttu-id="d3221-180">Nella casella di testo **Issuer URL** (URL autorità emittente) incollare il valore dell'**ID entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3221-180">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="d3221-181">d.</span><span class="sxs-lookup"><span data-stu-id="d3221-181">d.</span></span> <span data-ttu-id="d3221-182">Nella casella di testo **URL di accesso** incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3221-182">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d3221-183">e.</span><span class="sxs-lookup"><span data-stu-id="d3221-183">e.</span></span> <span data-ttu-id="d3221-184">Aprire il certificato con codifica **Base 64** nel Blocco note, copiarne il contenuto negli Appunti e incollarlo nella casella **Certificato**.</span><span class="sxs-lookup"><span data-stu-id="d3221-184">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span></span>
   
    <span data-ttu-id="d3221-185">f.</span><span class="sxs-lookup"><span data-stu-id="d3221-185">f.</span></span> <span data-ttu-id="d3221-186">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="d3221-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d3221-187">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d3221-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3221-188">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d3221-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3221-189">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3221-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3221-190">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3221-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3221-191">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3221-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d3221-193">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d3221-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3221-194">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d3221-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3221-196">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d3221-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3221-198">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d3221-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3221-200">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d3221-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3221-202">a.</span><span class="sxs-lookup"><span data-stu-id="d3221-202">a.</span></span> <span data-ttu-id="d3221-203">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3221-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3221-204">b.</span><span class="sxs-lookup"><span data-stu-id="d3221-204">b.</span></span> <span data-ttu-id="d3221-205">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d3221-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3221-206">c.</span><span class="sxs-lookup"><span data-stu-id="d3221-206">c.</span></span> <span data-ttu-id="d3221-207">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d3221-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d3221-208">d.</span><span class="sxs-lookup"><span data-stu-id="d3221-208">d.</span></span> <span data-ttu-id="d3221-209">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d3221-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="d3221-210">Creazione di un utente di test di Intacct</span><span class="sxs-lookup"><span data-stu-id="d3221-210">Creating an Intacct test user</span></span>

<span data-ttu-id="d3221-211">Per consentire agli utenti di Azure AD di accedere a Intacct, è necessario eseguirne il provisioning in Intacct.</span><span class="sxs-lookup"><span data-stu-id="d3221-211">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="d3221-212">In Intacct il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="d3221-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="d3221-213">**Per eseguire il provisioning degli account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d3221-213">**To provision user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="d3221-214">Accedere al tenant di **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="d3221-214">Sign in to your **Intacct** tenant.</span></span>

2. <span data-ttu-id="d3221-215">Fare clic sulla scheda **Company** (Azienda) e quindi su **Users** (Utenti).</span><span class="sxs-lookup"><span data-stu-id="d3221-215">Click the **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="d3221-216">![Utenti](./media/active-directory-saas-intacct-tutorial/ic790041.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="d3221-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="d3221-217">Fare clic sulla scheda **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="d3221-217">Click the **Add** tab.</span></span>

    <span data-ttu-id="d3221-218">![Aggiungi](./media/active-directory-saas-intacct-tutorial/ic790042.png "Aggiungi")</span><span class="sxs-lookup"><span data-stu-id="d3221-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="d3221-219">Nella sezione **Informazioni utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d3221-219">In the **User Information** section, perform the following steps:</span></span>

    <span data-ttu-id="d3221-220">![Informazioni utente](./media/active-directory-saas-intacct-tutorial/ic790043.png "Informazioni utente")</span><span class="sxs-lookup"><span data-stu-id="d3221-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="d3221-221">a.</span><span class="sxs-lookup"><span data-stu-id="d3221-221">a.</span></span> <span data-ttu-id="d3221-222">Nelle caselle di testo **User ID**, **Last name**, **First name**, **Email address**, **Title** e **Phone** immettere l'ID utente, il cognome, il nome, l'indirizzo di posta elettronica, la posizione e il numero di telefono di un account Azure AD di cui si vuole eseguire il provisioning nella sezione **Informazioni utente**.</span><span class="sxs-lookup"><span data-stu-id="d3221-222">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span></span>

    <span data-ttu-id="d3221-223">b.</span><span class="sxs-lookup"><span data-stu-id="d3221-223">b.</span></span> <span data-ttu-id="d3221-224">Selezionare i **privilegi di amministratore** di un account Azure AD di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="d3221-224">Select the **Admin privileges** of an Azure AD account that you want to provision.</span></span>
   
    <span data-ttu-id="d3221-225">c.</span><span class="sxs-lookup"><span data-stu-id="d3221-225">c.</span></span> <span data-ttu-id="d3221-226">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d3221-226">Click **Save**.</span></span> <span data-ttu-id="d3221-227">Il titolare dell'account Azure AD riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="d3221-227">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="d3221-228">Per eseguire il provisioning degli account utente di Azure AD, è possibile usare altri strumenti o API per la creazione di account utente Intacct forniti da Intacct.</span><span class="sxs-lookup"><span data-stu-id="d3221-228">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d3221-229">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3221-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d3221-230">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Intacct.</span><span class="sxs-lookup"><span data-stu-id="d3221-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intacct.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d3221-232">**Per assegnare Britta Simon a Intacct, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d3221-232">**To assign Britta Simon to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="d3221-233">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d3221-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d3221-235">Nell'elenco delle applicazioni selezionare **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="d3221-235">In the applications list, select **Intacct**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="d3221-237">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d3221-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d3221-239">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d3221-239">Click **Add** button.</span></span> <span data-ttu-id="d3221-240">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d3221-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d3221-242">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d3221-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d3221-243">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d3221-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3221-244">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d3221-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3221-245">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d3221-245">Testing single sign-on</span></span>

<span data-ttu-id="d3221-246">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d3221-246">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="d3221-247">Quando si fa clic sul riquadro Intacct nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Intacct.</span><span class="sxs-lookup"><span data-stu-id="d3221-247">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3221-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d3221-248">Additional resources</span></span>

* [<span data-ttu-id="d3221-249">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3221-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3221-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3221-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

