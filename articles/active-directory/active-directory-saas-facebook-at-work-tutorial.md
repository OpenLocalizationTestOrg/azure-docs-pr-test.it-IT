---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Workplace by Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: 27e62a00832484667117d8718db9f2fc05e2f4e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="e1992-103">Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="e1992-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="e1992-104">Questa esercitazione descrive come integrare Workplace by Facebook con Azure Active Directory, ovvero Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1992-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1992-105">L'integrazione di Workplace by Facebook con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e1992-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e1992-106">In Azure AD è possibile controllare chi può accedere a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e1992-106">You can control in Azure AD who has access to Workplace by Facebook.</span></span>
- <span data-ttu-id="e1992-107">È possibile abilitare gli utenti per l'accesso automatico a Workplace by Facebook (Single Sign-On) con i loro account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1992-107">You can enable your users to automatically get signed on to Workplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e1992-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1992-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="e1992-109">Per altri dettagli sull'integrazione di app SaaS (Software as a Service) con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1992-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1992-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e1992-110">Prerequisites</span></span>

<span data-ttu-id="e1992-111">Per configurare l'integrazione di Azure AD con Workplace by Facebook, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e1992-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="e1992-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1992-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1992-113">Una sottoscrizione a Workplace by Facebook abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="e1992-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="e1992-114">A questo scopo, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="e1992-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="e1992-115">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e1992-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1992-116">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1992-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1992-117">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e1992-117">Scenario description</span></span>
<span data-ttu-id="e1992-118">In questa esercitazione viene testato l'accesso SSO di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e1992-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="e1992-119">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="e1992-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1992-120">Aggiungere Workplace by Facebook dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="e1992-120">Add Workplace by Facebook from the gallery.</span></span>
2. <span data-ttu-id="e1992-121">Configurare e testare l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1992-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="e1992-122">Aggiungere Workplace by Facebook dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e1992-122">Add Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="e1992-123">Per configurare l'integrazione di Workplace by Facebook in Azure AD, aggiungere Workplace by Facebook dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e1992-123">To configure the integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="e1992-124">Nel [portale di Azure](https://portal.azure.com) fare clic su **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="e1992-124">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="e1992-126">Esplorare **Applicazioni aziendali** > **All applications** (Tutte le applicazioni).</span><span class="sxs-lookup"><span data-stu-id="e1992-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="e1992-128">Per aggiungere una nuova applicazione, fare clic su **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e1992-128">To add the new application, select **New application** on the top of the dialog box.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="e1992-130">Nella casella di ricerca digitare **Workplace by Facebook** e selezionare **Workplace by Facebook** dai risultati.</span><span class="sxs-lookup"><span data-stu-id="e1992-130">In the search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="e1992-131">Selezionare quindi **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1992-131">Then select **Add**, to add the application.</span></span>

    ![Workplace by Facebook nell'elenco risultati](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e1992-133">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1992-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e1992-134">In questa sezione viene configurato e testato l'accesso SSO di Azure AD con Workplace by Facebook usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e1992-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e1992-135">Affinché l'accesso SSO funzioni correttamente, Azure AD deve conoscere il rapporto tra l'utente controparte di Workplace by Facebook e un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1992-135">For SSO to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="e1992-136">In altre parole, è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e1992-136">In other words, a linked relationship between an Azure AD user and the related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="e1992-137">Stabilire questa relazione assegnando il valore di **nome utente** in Azure AD al valore **Username** in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e1992-137">Establish this relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e1992-138">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1992-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e1992-139">In questa sezione viene abilitato l'accesso SSO di Azure AD nel portale di Azure e viene configurato l'accesso SSO nell'applicazione Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e1992-139">In this section, you enable Azure AD SSO in the Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="e1992-140">Nella pagina di integrazione dell'applicazione **Workplace by Facebook** del portale di Azure selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e1992-140">In the Azure portal, on the **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Configurare il collegamento Single Sign-On][4]

2. <span data-ttu-id="e1992-142">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso SSO.</span><span class="sxs-lookup"><span data-stu-id="e1992-142">In the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="e1992-144">Nella sezione **Workplace by Facebook Domain and URLs** (URL e dominio Workplace by Facebook) eseguire i passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="e1992-144">In the **Workplace by Facebook Domain and URLs** section, do the following:</span></span>

    <span data-ttu-id="e1992-145">a.</span><span class="sxs-lookup"><span data-stu-id="e1992-145">a.</span></span> <span data-ttu-id="e1992-146">Nella casella di testo **URL accesso** digitare un URL che usa il modello seguente: `https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="e1992-146">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="e1992-147">b.</span><span class="sxs-lookup"><span data-stu-id="e1992-147">b.</span></span> <span data-ttu-id="e1992-148">Nella casella di testo **Identificatore** digitare l'URL che usa il modello seguente:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="e1992-148">In the **Identifier** text box, type a URL that uses the following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="e1992-149">Questi valori sono solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="e1992-149">These values are an example only.</span></span> <span data-ttu-id="e1992-150">Aggiornare questi valori con URL di accesso e identificatore effettivi.</span><span class="sxs-lookup"><span data-stu-id="e1992-150">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="e1992-151">Per ottenere questi valori, contattare il [team di supporto client Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="e1992-151">Contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="e1992-152">Nella sezione **Certificato di firma SAML** selezionare **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="e1992-152">In the **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="e1992-154">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e1992-154">Select **Save**.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1992-156">Nella sezione **Workplace by Facebook Configuration** (Configurazione di Workplace by Facebook) selezionare **Configure Workplace by Facebook** (Configurare Workplace by Facebook) per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="e1992-156">In the **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="e1992-157">Copiare l'**URL di disconnessione, l'ID entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="e1992-157">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Configurazione di Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="e1992-159">In un'altra finestra del Web browser accedere al sito aziendale di Workplace by Facebook come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e1992-159">In a different web browser window, sign in to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="e1992-160">Nell'ambito del processo di autenticazione SAML, Workplace può usare stringhe di query di dimensioni massime di 2,5 kilobyte per passare i parametri ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1992-160">As part of the SAML authentication process, Workplace can use query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="e1992-161">In **Company Dashboard** (Company Dashboard) passare alla scheda **Authentication** (Autenticazione).</span><span class="sxs-lookup"><span data-stu-id="e1992-161">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="e1992-162">In **SAML Authentication** (Autenticazione SAML) selezionare **SSO Only** (Solo SSO) dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="e1992-162">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="e1992-163">Immettere i valori copiati dalla sezione **Workplace by Facebook Configuration** (Configurazione di Workplace by Facebook) del portale di Azure nei campi corrispondenti:</span><span class="sxs-lookup"><span data-stu-id="e1992-163">Enter the values copied from the **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="e1992-164">Nella casella di testo **SAML URL** (URL SAML) incollare il valore di **URL servizio Single Sign-On** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1992-164">In the **SAML URL** text box, paste the value of **Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="e1992-165">Nella casella di testo **SAML Issuer URL** (URL emittente SAML) incollare il valore dell'**ID entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1992-165">In the **SAML Issuer URL** text box, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="e1992-166">In **SAML Logout Redirect (Optional)** (Reindirizzamento disconnessione SAML (facoltativo)) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1992-166">In **SAML Logout Redirect (optional)**, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="e1992-167">Aprire nel Blocco note il **certificato con codifica base 64** scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1992-167">Open your **base-64 encoded certificate** in Notepad, downloaded from the Azure portal.</span></span> <span data-ttu-id="e1992-168">Copiare il contenuto negli Appunti e quindi incollarlo nella casella di testo **Certificato SAML**.</span><span class="sxs-lookup"><span data-stu-id="e1992-168">Copy the content of it into your clipboard, and then paste it to the **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="e1992-169">Potrebbe essere necessario inserire l'URL dei partecipanti, l'URL del destinatario e l'URL ACS (servizio consumer di asserzione) elencati nella sezione **SAML Configuration** (Configurazione SAML).</span><span class="sxs-lookup"><span data-stu-id="e1992-169">You might need to enter the audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="e1992-170">Scorrere fino alla fine della sezione e selezionare **Test SSO** (Testa SSO).</span><span class="sxs-lookup"><span data-stu-id="e1992-170">Scroll to the bottom of the section, and select **Test SSO**.</span></span> <span data-ttu-id="e1992-171">Viene visualizzata una finestra popup con la pagina di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1992-171">A pop-up window appears, with the Azure AD sign-in page.</span></span> <span data-ttu-id="e1992-172">Per autenticarsi, immettere le credenziali come di consueto.</span><span class="sxs-lookup"><span data-stu-id="e1992-172">To authenticate, enter your credentials as normal.</span></span> <span data-ttu-id="e1992-173">Assicurarsi che l'indirizzo di posta elettronica restituito da Azure AD corrisponda a quello dell'account Workplace con cui si è connessi.</span><span class="sxs-lookup"><span data-stu-id="e1992-173">Ensure the email address returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="e1992-174">Se il test è stato completato, scorrere fino alla fine della pagina e selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e1992-174">If the test has finished successfully, scroll to the bottom of the page and select **Save**.</span></span>

14. <span data-ttu-id="e1992-175">Chiunque usi Workplace visualizza ora la pagina di accesso ad Azure AD per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e1992-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="e1992-176">È possibile scegliere di configurare un URL di disconnessione SAML, che può essere usato per puntare alla pagina di disconnessione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1992-176">You can choose to configure a SAML sign out URL, which can be used to point at the Azure AD sign-out page.</span></span> <span data-ttu-id="e1992-177">Quando questa impostazione è abilitata e configurata, l'utente non viene più indirizzato alla pagina di disconnessione di Workplace.</span><span class="sxs-lookup"><span data-stu-id="e1992-177">When this setting is enabled and configured, the user is no longer directed to the Workplace sign-out page.</span></span> <span data-ttu-id="e1992-178">Invece che a questa pagina, l'utente viene reindirizzato all'URL aggiunto nell'impostazione di reindirizzamento di disconnessione SAML.</span><span class="sxs-lookup"><span data-stu-id="e1992-178">Instead, the user is redirected to the URL that was added in the SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="e1992-179">Un riepilogo delle istruzioni è disponibile nel [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="e1992-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="e1992-180">Dopo aver aggiunto l'app dalla sezione **Active Directory** > **Applicazioni aziendali** è sufficiente selezionare la scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="e1992-180">After adding this app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e1992-181">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1992-181">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="e1992-182">Configurare la frequenza di riautenticazione</span><span class="sxs-lookup"><span data-stu-id="e1992-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="e1992-183">È possibile configurare Workplace in modo che chieda una verifica SAML ogni giorno, ogni tre giorni, ogni settimana, ogni due settimane, ogni mese o mai.</span><span class="sxs-lookup"><span data-stu-id="e1992-183">You can configure Workplace to prompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="e1992-184">Il valore minimo per la verifica SAML nelle applicazioni per dispositivi mobili è impostato su una settimana.</span><span class="sxs-lookup"><span data-stu-id="e1992-184">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="e1992-185">È inoltre possibile forzare una reimpostazione SAML per tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="e1992-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="e1992-186">A tale scopo, usare il pulsante **Require SAML authentication for all users now** (Richiedi ora autenticazione SAML per tutti gli utenti).</span><span class="sxs-lookup"><span data-stu-id="e1992-186">To do this, use the **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e1992-187">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1992-187">Create an Azure AD test user</span></span>
<span data-ttu-id="e1992-188">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1992-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

1. <span data-ttu-id="e1992-190">Nel **portale di Azure** fare clic su **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="e1992-190">In the **Azure portal**, in the left pane, select **Azure Active Directory**.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1992-192">Per visualizzare l'elenco di utenti, passare a **Users and groups** (Utenti e gruppi) e selezionare **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e1992-192">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1992-194">Per aprire la finestra di dialogo **Utente**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e1992-194">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1992-196">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e1992-196">In the **User** dialog box, do the following:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1992-198">a.</span><span class="sxs-lookup"><span data-stu-id="e1992-198">a.</span></span> <span data-ttu-id="e1992-199">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1992-199">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1992-200">b.</span><span class="sxs-lookup"><span data-stu-id="e1992-200">b.</span></span> <span data-ttu-id="e1992-201">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e1992-201">In the **User name** text box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1992-202">c.</span><span class="sxs-lookup"><span data-stu-id="e1992-202">c.</span></span> <span data-ttu-id="e1992-203">Selezionare **Mostra password**e annotare la password.</span><span class="sxs-lookup"><span data-stu-id="e1992-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="e1992-204">d.</span><span class="sxs-lookup"><span data-stu-id="e1992-204">d.</span></span> <span data-ttu-id="e1992-205">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e1992-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="e1992-206">Creare un utente test di Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="e1992-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="e1992-207">In questa sezione si crea un utente di nome Britta Simon in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e1992-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="e1992-208">Workplace by Facebook supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e1992-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="e1992-209">Non è necessaria alcuna azione dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="e1992-209">There is no action for you in this section.</span></span> <span data-ttu-id="e1992-210">Se un utente non esiste in Workplace by Facebook, si crea una nuova istanza quando si tenta di accedere a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e1992-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="e1992-211">Se è necessario creare un utente manualmente, contattare il [team di supporto al client di Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="e1992-211">If you need to create a user manually, contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e1992-212">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1992-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="e1992-213">In questa sezione Britta Simon viene abilitata all'uso dell'accesso SSO di Azure concedendo l'accesso a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e1992-213">In this section, you enable Britta Simon to use Azure SSO by granting access to Workplace by Facebook.</span></span>

![Assegnare utenti][200] 

1. <span data-ttu-id="e1992-215">Nel portale di Azure aprire la visualizzazione applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e1992-215">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="e1992-216">Passare alla visualizzazione directory, accedere ad **Applicazioni aziendali** e quindi selezionare **All applications** (Tutte le applicazioni).</span><span class="sxs-lookup"><span data-stu-id="e1992-216">Go to the directory view, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![Assegnare utenti][201] 

2. <span data-ttu-id="e1992-218">Nell'elenco di applicazioni selezionare **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="e1992-218">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Collegamento di Workplace by Facebook nell'elenco delle applicazioni](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="e1992-220">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e1992-220">In the menu on the left, select **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202] 

4. <span data-ttu-id="e1992-222">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e1992-222">Select **Add**.</span></span> <span data-ttu-id="e1992-223">Quindi nel riquadro **Aggiungi assegnazione** selezionare **Users and groups** (Utenti e gruppi).</span><span class="sxs-lookup"><span data-stu-id="e1992-223">Then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="e1992-225">Nella finestra di dialogo **Users and groups** (Utenti e gruppi) selezionare **Britta Simon** nell'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="e1992-225">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="e1992-226">Nella finestra di dialogo **Utenti e gruppi** fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="e1992-226">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="e1992-227">Nella finestra di dialogo **Aggiungi assegnazione** selezionare **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="e1992-227">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e1992-228">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e1992-228">Test single sign-on</span></span>

<span data-ttu-id="e1992-229">Per testare le impostazioni di SSO, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e1992-229">If you want to test your SSO settings, open the Access Panel.</span></span>
<span data-ttu-id="e1992-230">Per altre informazioni, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e1992-230">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e1992-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e1992-231">Next steps</span></span>

* <span data-ttu-id="e1992-232">Vedere l'[elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="e1992-232">See the [list of tutorials on how to integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="e1992-233">Leggere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1992-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="e1992-234">Altre informazioni su come [configurare il provisioning utente](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e1992-234">Learn more about how to [configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

