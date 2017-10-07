---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e all'area di lavoro da Facebook.
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
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="c27cf-103">Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="c27cf-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="c27cf-104">In questa esercitazione, è illustrato come toointegrate all'area di lavoro da Facebook con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c27cf-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c27cf-105">L'integrazione all'area di lavoro da Facebook con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="c27cf-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c27cf-106">È possibile controllare in Azure AD che ha accesso tooWorkplace da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c27cf-106">You can control in Azure AD who has access tooWorkplace by Facebook.</span></span>
- <span data-ttu-id="c27cf-107">È possibile abilitare gli utenti tooautomatically ottenere l'accesso tooWorkplace da Facebook (single sign-on) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27cf-107">You can enable your users tooautomatically get signed on tooWorkplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c27cf-108">È possibile gestire gli account in un'unica posizione centrale: hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c27cf-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="c27cf-109">Per altri dettagli sull'integrazione di app SaaS (Software as a Service) con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c27cf-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c27cf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c27cf-110">Prerequisites</span></span>

<span data-ttu-id="c27cf-111">integrazione di Azure AD con area di lavoro da Facebook tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="c27cf-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="c27cf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c27cf-113">Una sottoscrizione a Workplace by Facebook abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="c27cf-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="c27cf-114">passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="c27cf-114">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="c27cf-115">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c27cf-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c27cf-116">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c27cf-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c27cf-117">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c27cf-117">Scenario description</span></span>
<span data-ttu-id="c27cf-118">In questa esercitazione viene testato l'accesso SSO di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c27cf-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="c27cf-119">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="c27cf-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c27cf-120">Aggiungere all'area di lavoro da Facebook dalla raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="c27cf-120">Add Workplace by Facebook from hello gallery.</span></span>
2. <span data-ttu-id="c27cf-121">Configurare e testare l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27cf-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="c27cf-122">Aggiungere all'area di lavoro da Facebook dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="c27cf-122">Add Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="c27cf-123">integrazione di hello tooconfigure di lavoro da Facebook in Azure AD, aggiungere all'area di lavoro da Facebook hello raccolta tooyour elenco di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c27cf-123">tooconfigure hello integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="c27cf-124">In hello [portale di Azure](https://portal.azure.com), nel riquadro sinistro di hello, selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-124">In hello [Azure portal](https://portal.azure.com), in hello left pane, select **Azure Active Directory**.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="c27cf-126">Sfoglia troppo**applicazioni aziendali** > **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-126">Browse too**Enterprise applications** > **All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="c27cf-128">tooadd hello nuova applicazione, seleziona **nuova applicazione** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="c27cf-128">tooadd hello new application, select **New application** on hello top of hello dialog box.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="c27cf-130">Nella casella di ricerca hello, digitare **all'area di lavoro da Facebook**e selezionare **all'area di lavoro da Facebook** dai risultati.</span><span class="sxs-lookup"><span data-stu-id="c27cf-130">In hello search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="c27cf-131">Selezionare quindi **Aggiungi**, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c27cf-131">Then select **Add**, tooadd hello application.</span></span>

    ![Nell'elenco dei risultati all'area di lavoro da Facebook in hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c27cf-133">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c27cf-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c27cf-134">In questa sezione viene configurato e testato l'accesso SSO di Azure AD con Workplace by Facebook usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c27cf-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c27cf-135">Per toowork SSO, Azure AD deve tooknow quale utente controparte hello nell'area di lavoro da Facebook è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27cf-135">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="c27cf-136">In altre parole, stabilire una relazione tra un utente di Azure Active Directory e l'utente correlato di hello nell'area di lavoro da Facebook collegata.</span><span class="sxs-lookup"><span data-stu-id="c27cf-136">In other words, a linked relationship between an Azure AD user and hello related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="c27cf-137">Stabilire questa relazione assegnando il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** nell'area di lavoro da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c27cf-137">Establish this relationship by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c27cf-138">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c27cf-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c27cf-139">In questa sezione, si abilita Azure Active Directory SSO in hello portale di Azure e si configura SSO nell'area di lavoro dall'applicazione Facebook.</span><span class="sxs-lookup"><span data-stu-id="c27cf-139">In this section, you enable Azure AD SSO in hello Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="c27cf-140">Nel portale di Azure su hello hello **all'area di lavoro da Facebook** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-140">In hello Azure portal, on hello **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Configurare il collegamento Single Sign-On][4]

2. <span data-ttu-id="c27cf-142">In hello **Single sign-on** nella finestra di dialogo **modalità** come **basato su SAML Sign-on** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="c27cf-142">In hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="c27cf-144">In hello **all'area di lavoro al dominio di Facebook e URL** sezione, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c27cf-144">In hello **Workplace by Facebook Domain and URLs** section, do hello following:</span></span>

    <span data-ttu-id="c27cf-145">a.</span><span class="sxs-lookup"><span data-stu-id="c27cf-145">a.</span></span> <span data-ttu-id="c27cf-146">In hello **Sign-on URL** nella casella di testo digitare l'URL che utilizza hello seguente motivo:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="c27cf-146">In hello **Sign-on URL** text box, type a URL that uses hello following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="c27cf-147">b.</span><span class="sxs-lookup"><span data-stu-id="c27cf-147">b.</span></span> <span data-ttu-id="c27cf-148">In hello **identificatore** nella casella di testo digitare l'URL che utilizza hello seguente motivo:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="c27cf-148">In hello **Identifier** text box, type a URL that uses hello following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="c27cf-149">Questi valori sono solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="c27cf-149">These values are an example only.</span></span> <span data-ttu-id="c27cf-150">Aggiornare questi valori con URL hello effettivo sign-on e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="c27cf-150">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="c27cf-151">Contatto hello [all'area di lavoro dal team di supporto Client di Facebook](https://workplace.fb.com/faq/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="c27cf-151">Contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="c27cf-152">In hello **certificato di firma SAML** selezionare **certificato (Base64)**e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c27cf-152">In hello **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="c27cf-154">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-154">Select **Save**.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c27cf-156">In hello **all'area di lavoro dalla configurazione di Facebook** selezionare **configurare all'area di lavoro da Facebook** tooopen hello **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="c27cf-156">In hello **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="c27cf-157">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **riferimento rapido** sezione.</span><span class="sxs-lookup"><span data-stu-id="c27cf-157">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Configurazione di Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="c27cf-159">In una finestra del web browser, accedere all'area di lavoro dal sito della società Facebook tooyour come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c27cf-159">In a different web browser window, sign in tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="c27cf-160">Come parte del processo di autenticazione SAML hello, all'area di lavoro è possibile utilizzare le stringhe di query di backup too2.5 kilobyte in dimensioni in ordine toopass parametri tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c27cf-160">As part of hello SAML authentication process, Workplace can use query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="c27cf-161">In hello **Dashboard aziendali**, visitare toohello **autenticazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="c27cf-161">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="c27cf-162">In **SAML Authentication**selezionare **SSO solo** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="c27cf-162">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="c27cf-163">Immettere i valori hello copiati hello **all'area di lavoro dalla configurazione di Facebook** sezione del portale di Azure nei campi corrispondenti hello hello:</span><span class="sxs-lookup"><span data-stu-id="c27cf-163">Enter hello values copied from hello **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="c27cf-164">Nel **SAML URL** Incolla hello valore della casella di testo **URL servizio Single Sign-On**, che è stato copiato da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c27cf-164">In the **SAML URL** text box, paste hello value of **Single Sign-On Service URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="c27cf-165">Nel **SAML Issuer URL** Incolla hello valore della casella di testo **ID entità SAML**, che è stato copiato da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c27cf-165">In the **SAML Issuer URL** text box, paste hello value of **SAML Entity ID**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="c27cf-166">In **SAML Logout Redirect (facoltativo)**, incollare il valore di hello di **Sign-Out URL**, che è stato copiato da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c27cf-166">In **SAML Logout Redirect (optional)**, paste hello value of **Sign-Out URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="c27cf-167">Aprire il **certificato con codifica base 64** nel blocco note, scaricato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c27cf-167">Open your **base-64 encoded certificate** in Notepad, downloaded from hello Azure portal.</span></span> <span data-ttu-id="c27cf-168">Copia contenuto hello negli Appunti e quindi incollarlo toothe **SAML Certificate** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="c27cf-168">Copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="c27cf-169">Potrebbe essere necessario destinatari hello tooenter URL, l'URL del destinatario e ACS (servizio Consumer di asserzione) URL, elencati in hello **configurazione SAML** sezione.</span><span class="sxs-lookup"><span data-stu-id="c27cf-169">You might need tooenter hello audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="c27cf-170">Scorrere nella parte inferiore toohello della sezione hello e selezionare **SSO Test**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-170">Scroll toohello bottom of hello section, and select **Test SSO**.</span></span> <span data-ttu-id="c27cf-171">Viene visualizzata una finestra popup con hello Azure AD nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="c27cf-171">A pop-up window appears, with hello Azure AD sign-in page.</span></span> <span data-ttu-id="c27cf-172">tooauthenticate, immettere le credenziali come di consueto.</span><span class="sxs-lookup"><span data-stu-id="c27cf-172">tooauthenticate, enter your credentials as normal.</span></span> <span data-ttu-id="c27cf-173">Verificare l'indirizzo di posta elettronica hello restituito da Azure AD è hello stesso hello account aziendale con cui si è connessi.</span><span class="sxs-lookup"><span data-stu-id="c27cf-173">Ensure hello email address returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="c27cf-174">Se è stato completato il test di hello, scorrere toohello parte inferiore della pagina hello e selezionare **salvare**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-174">If hello test has finished successfully, scroll toohello bottom of hello page and select **Save**.</span></span>

14. <span data-ttu-id="c27cf-175">Chiunque usi Workplace visualizza ora la pagina di accesso ad Azure AD per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c27cf-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="c27cf-176">È possibile scegliere tooconfigure un URL, che può essere utilizzato toopoint alla pagina di disconnessione hello Azure AD di disconnessione SAML.</span><span class="sxs-lookup"><span data-stu-id="c27cf-176">You can choose tooconfigure a SAML sign out URL, which can be used toopoint at hello Azure AD sign-out page.</span></span> <span data-ttu-id="c27cf-177">Quando questa impostazione è abilitata e configurata, hello utente non è più diretto toohello pagina di disconnessione all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c27cf-177">When this setting is enabled and configured, hello user is no longer directed toohello Workplace sign-out page.</span></span> <span data-ttu-id="c27cf-178">In alternativa, hello è reindirizzato toohello URL che è stato aggiunto in base alle impostazioni di reindirizzamento disconnessione SAML hello.</span><span class="sxs-lookup"><span data-stu-id="c27cf-178">Instead, hello user is redirected toohello URL that was added in hello SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="c27cf-179">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello.</span><span class="sxs-lookup"><span data-stu-id="c27cf-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app.</span></span> <span data-ttu-id="c27cf-180">Dopo l'aggiunta di questa app da hello **Active Directory** > **applicazioni aziendali** , selezionare semplicemente hello **Single Sign-On** scheda e hello accesso documentazione tramite hello incorporato **configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c27cf-180">After adding this app from hello **Active Directory** > **Enterprise Applications** section, simply select hello **Single Sign-On** tab, and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c27cf-181">Altre informazioni sulla funzionalità di documentazione embedded hello in hello [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c27cf-181">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="c27cf-182">Configurare la frequenza di riautenticazione</span><span class="sxs-lookup"><span data-stu-id="c27cf-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="c27cf-183">È possibile configurare tooprompt all'area di lavoro per un controllo SAML ogni giorno, tre giorni, una settimana, mese, due settimane o mai.</span><span class="sxs-lookup"><span data-stu-id="c27cf-183">You can configure Workplace tooprompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="c27cf-184">Hello valore minimo per il controllo SAML hello in applicazioni per dispositivi mobili è impostata tooone settimana.</span><span class="sxs-lookup"><span data-stu-id="c27cf-184">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="c27cf-185">È inoltre possibile forzare una reimpostazione SAML per tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="c27cf-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="c27cf-186">toodo hello, utilizzare **SAML richiedono l'autenticazione per tutti gli utenti ora** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c27cf-186">toodo this, use hello **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c27cf-187">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c27cf-187">Create an Azure AD test user</span></span>
<span data-ttu-id="c27cf-188">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c27cf-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

1. <span data-ttu-id="c27cf-190">In hello **portale di Azure**, nel riquadro sinistro di hello, selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-190">In hello **Azure portal**, in hello left pane, select **Azure Active Directory**.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c27cf-192">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**e selezionare **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-192">toodisplay hello list of users, go too**Users and groups**, and select **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c27cf-194">hello tooopen **utente** nella finestra di dialogo **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-194">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c27cf-196">In hello **utente** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c27cf-196">In hello **User** dialog box, do hello following:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c27cf-198">a.</span><span class="sxs-lookup"><span data-stu-id="c27cf-198">a.</span></span> <span data-ttu-id="c27cf-199">In hello **nome** nella casella di testo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-199">In hello **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c27cf-200">b.</span><span class="sxs-lookup"><span data-stu-id="c27cf-200">b.</span></span> <span data-ttu-id="c27cf-201">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c27cf-201">In hello **User name** text box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c27cf-202">c.</span><span class="sxs-lookup"><span data-stu-id="c27cf-202">c.</span></span> <span data-ttu-id="c27cf-203">Selezionare **Mostra password**e annotare la password.</span><span class="sxs-lookup"><span data-stu-id="c27cf-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="c27cf-204">d.</span><span class="sxs-lookup"><span data-stu-id="c27cf-204">d.</span></span> <span data-ttu-id="c27cf-205">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="c27cf-206">Creare un utente test di Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="c27cf-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="c27cf-207">In questa sezione si crea un utente di nome Britta Simon in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="c27cf-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="c27cf-208">Workplace by Facebook supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c27cf-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="c27cf-209">Non è necessaria alcuna azione dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="c27cf-209">There is no action for you in this section.</span></span> <span data-ttu-id="c27cf-210">Se un utente non esiste nell'area di lavoro da Facebook, una nuova istanza viene creata quando si tenta di tooaccess all'area di lavoro da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c27cf-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="c27cf-211">Se è necessario un utente toocreate manualmente, contattare hello [all'area di lavoro dal team di supporto Client di Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="c27cf-211">If you need toocreate a user manually, contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c27cf-212">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c27cf-212">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c27cf-213">In questa sezione per abilitare Britta Simon toouse SSO Azure concessione dell'accesso tooWorkplace da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c27cf-213">In this section, you enable Britta Simon toouse Azure SSO by granting access tooWorkplace by Facebook.</span></span>

![Assegnare utenti][200] 

1. <span data-ttu-id="c27cf-215">Consente di visualizzare applicazioni di portale, aprire hello in hello Azure.</span><span class="sxs-lookup"><span data-stu-id="c27cf-215">In hello Azure portal, open hello applications view.</span></span> <span data-ttu-id="c27cf-216">Vai a visualizzazione directory toohello, andare troppo**applicazioni aziendali**, quindi selezionare **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-216">Go toohello directory view, go too**Enterprise applications**, and then select **All applications**.</span></span>

    ![Assegnare utenti][201] 

2. <span data-ttu-id="c27cf-218">Nell'elenco di applicazioni hello, selezionare **all'area di lavoro da Facebook**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-218">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Hello all'area di lavoro da Facebook collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="c27cf-220">Dal menu hello hello sinistra, selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-220">In hello menu on hello left, select **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. <span data-ttu-id="c27cf-222">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-222">Select **Add**.</span></span> <span data-ttu-id="c27cf-223">Quindi, nel hello **Aggiungi** riquadro, selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-223">Then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="c27cf-225">In hello **utenti e gruppi** nella finestra di dialogo **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="c27cf-225">In hello **Users and groups** dialog box, select **Britta Simon** in hello users list.</span></span>

6. <span data-ttu-id="c27cf-226">In hello **utenti e gruppi** nella finestra di dialogo **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-226">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="c27cf-227">In hello **Aggiungi** nella finestra di dialogo **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="c27cf-227">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c27cf-228">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c27cf-228">Test single sign-on</span></span>

<span data-ttu-id="c27cf-229">Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="c27cf-229">If you want tootest your SSO settings, open hello Access Panel.</span></span>
<span data-ttu-id="c27cf-230">Per ulteriori informazioni, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c27cf-230">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c27cf-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c27cf-231">Next steps</span></span>

* <span data-ttu-id="c27cf-232">Vedere hello [elenco di esercitazioni sulla toointegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="c27cf-232">See hello [list of tutorials on how toointegrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="c27cf-233">Leggere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c27cf-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="c27cf-234">Per ulteriori informazioni su troppo[Configura provisioning utente](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c27cf-234">Learn more about how too[configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



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

