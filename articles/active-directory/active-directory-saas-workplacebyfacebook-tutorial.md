---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e all'area di lavoro da Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="fbad0-103">Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="fbad0-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="fbad0-104">In questa esercitazione, è illustrato come toointegrate all'area di lavoro da Facebook con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbad0-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbad0-105">L'integrazione all'area di lavoro da Facebook con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="fbad0-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fbad0-106">È possibile controllare in Azure AD che ha accesso tooWorkplace da Facebook</span><span class="sxs-lookup"><span data-stu-id="fbad0-106">You can control in Azure AD who has access tooWorkplace by Facebook</span></span>
- <span data-ttu-id="fbad0-107">È possibile abilitare l'utenti tooautomatically get connesso tooWorkplace da Facebook (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbad0-107">You can enable your users tooautomatically get signed-on tooWorkplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbad0-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fbad0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fbad0-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbad0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbad0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fbad0-110">Prerequisites</span></span>

<span data-ttu-id="fbad0-111">integrazione di Azure AD con area di lavoro da Facebook tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="fbad0-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="fbad0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbad0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbad0-113">Una sottoscrizione di Workplace by Facebook abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fbad0-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbad0-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="fbad0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbad0-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="fbad0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbad0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="fbad0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbad0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbad0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbad0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="fbad0-118">Scenario description</span></span>
<span data-ttu-id="fbad0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="fbad0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbad0-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="fbad0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbad0-121">Aggiunta all'area di lavoro da Facebook dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fbad0-121">Adding Workplace by Facebook from hello gallery</span></span>
2. <span data-ttu-id="fbad0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbad0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="fbad0-123">Aggiunta all'area di lavoro da Facebook dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fbad0-123">Adding Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="fbad0-124">integrazione hello tooconfigure di lavoro da Facebook in Azure AD, è necessario tooadd all'area di lavoro da Facebook dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="fbad0-124">tooconfigure hello integration of Workplace by Facebook into Azure AD, you need tooadd Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fbad0-125">**tooadd all'area di lavoro da Facebook dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fbad0-125">**tooadd Workplace by Facebook from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbad0-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fbad0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbad0-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fbad0-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="fbad0-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="fbad0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="fbad0-133">Nella casella di ricerca hello, digitare **all'area di lavoro da Facebook**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-133">In hello search box, type **Workplace by Facebook**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="fbad0-135">Nel riquadro dei risultati hello, selezionare **all'area di lavoro da Facebook**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="fbad0-135">In hello results panel, select **Workplace by Facebook**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbad0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbad0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbad0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workplace by Facebook usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fbad0-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fbad0-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nell'area di lavoro da Facebook è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbad0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="fbad0-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello nell'area di lavoro da Facebook deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="fbad0-140">In other words, a link relationship between an Azure AD user and hello related user in Workplace by Facebook needs toobe established.</span></span>

<span data-ttu-id="fbad0-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nell'area di lavoro da Facebook.</span><span class="sxs-lookup"><span data-stu-id="fbad0-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="fbad0-142">tooconfigure e prova AD Azure single sign-on con area di lavoro da Facebook, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="fbad0-142">tooconfigure and test Azure AD single sign-on with Workplace by Facebook, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fbad0-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fbad0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fbad0-144">**[Configurazione di frequenza di riautenticazione](#configuring-reauthentication-frequency)**  -tooconfigure tooprompt di lavoro per un controllo di SAML.</span><span class="sxs-lookup"><span data-stu-id="fbad0-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - tooconfigure Workplace tooprompt for a SAML check.</span></span>
3. <span data-ttu-id="fbad0-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbad0-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="fbad0-146">**[Creazione di una rete aziendale da Facebook test utente](#creating-a-workplace-by-facebook-test-user)**  -toohave un equivalente di Britta Simon nell'area di lavoro da Facebook che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fbad0-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - toohave a counterpart of Britta Simon in Workplace by Facebook that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="fbad0-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fbad0-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="fbad0-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="fbad0-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbad0-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbad0-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbad0-150">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'area di lavoro dall'applicazione Facebook.</span><span class="sxs-lookup"><span data-stu-id="fbad0-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="fbad0-151">**Azure AD tooconfigure single sign-on con all'area di lavoro da Facebook, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fbad0-151">**tooconfigure Azure AD single sign-on with Workplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbad0-152">Nel portale di Azure su hello hello **all'area di lavoro da Facebook** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-152">In hello Azure portal, on hello **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="fbad0-154">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fbad0-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="fbad0-156">In hello **all'area di lavoro al dominio di Facebook e URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fbad0-156">On hello **Workplace by Facebook Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="fbad0-158">a.</span><span class="sxs-lookup"><span data-stu-id="fbad0-158">a.</span></span> <span data-ttu-id="fbad0-159">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="fbad0-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="fbad0-160">b.</span><span class="sxs-lookup"><span data-stu-id="fbad0-160">b.</span></span> <span data-ttu-id="fbad0-161">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="fbad0-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fbad0-162">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="fbad0-162">These values are not hello real.</span></span> <span data-ttu-id="fbad0-163">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="fbad0-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fbad0-164">Contatto [all'area di lavoro dal team di supporto Client di Facebook](https://workplace.fb.com/faq/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="fbad0-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="fbad0-165">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="fbad0-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="fbad0-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fbad0-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbad0-169">In hello **all'area di lavoro dalla configurazione di Facebook** fare clic su **configurare all'area di lavoro da Facebook** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="fbad0-169">On hello **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fbad0-170">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="fbad0-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="fbad0-172">In una finestra del web browser, account di accesso tooyour all'area di lavoro dal sito della società di Facebook come amministratore.</span><span class="sxs-lookup"><span data-stu-id="fbad0-172">In a different web browser window, login tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="fbad0-173">Come parte del processo di autenticazione SAML hello, all'area di lavoro può utilizzare le stringhe di query di backup too2.5 kilobyte in ordine toopass parametri tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fbad0-173">As part of hello SAML authentication process, Workplace may utilize query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="fbad0-174">In hello **Dashboard aziendali**, visitare toohello **autenticazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="fbad0-174">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="fbad0-175">In **SAML Authentication**selezionare **SSO solo** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="fbad0-175">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="fbad0-176">I valori di input hello copiati da **all'area di lavoro dalla configurazione di Facebook** sezione del portale di Azure nei campi corrispondenti hello hello:</span><span class="sxs-lookup"><span data-stu-id="fbad0-176">Input hello values copied from **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="fbad0-177">In **SAML URL** casella di testo, hello Incolla valore **URL servizio Single Sign-On**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbad0-177">In **SAML URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="fbad0-178">In **casella di testo URL autorità di certificazione SAML**, incollare il valore di hello di **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbad0-178">In **SAML Issuer URL textbox**, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="fbad0-179">In **SAML Logout Redirect** (facoltativo), incollare il valore di hello di **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbad0-179">In **SAML Logout Redirect** (Optional), paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="fbad0-180">Aprire il **certificato con codifica base 64** nel blocco note scaricato dal portale di Azure, copiarne contenuto hello negli Appunti e quindi incollarlo toothe **SAML Certificate** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="fbad0-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="fbad0-181">Potrebbe essere necessario tooenter hello URL pubblico, URL destinatario, e l'URL ACS (servizio Consumer di asserzione) elencati in hello **configurazione SAML** sezione.</span><span class="sxs-lookup"><span data-stu-id="fbad0-181">You may need tooenter hello Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="fbad0-182">Scorrere nella parte inferiore toohello della sezione hello e fare clic su hello **SSO Test** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fbad0-182">Scroll toohello bottom of hello section and click hello **Test SSO** button.</span></span> <span data-ttu-id="fbad0-183">Si ottiene una finestra popup visualizzata con la pagina di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbad0-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="fbad0-184">Immettere le credenziali in come tooauthenticate normale.</span><span class="sxs-lookup"><span data-stu-id="fbad0-184">Enter your credentials in as normal tooauthenticate.</span></span> 

    <span data-ttu-id="fbad0-185">**Risoluzione dei problemi:** indirizzo di posta elettronica hello verificare restituito da Azure AD è hello stesso hello account aziendale con cui si è connessi.</span><span class="sxs-lookup"><span data-stu-id="fbad0-185">**Troubleshooting:** Ensure hello email address being returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="fbad0-186">Una volta test hello è stato completato, scorrere toohello parte inferiore della pagina hello e fare clic su hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fbad0-186">Once hello test has been completed successfully, scroll toohello bottom of hello page and click hello **Save** button.</span></span>

14. <span data-ttu-id="fbad0-187">Tutti gli utenti che usano Workplace visualizzeranno ora una pagina di accesso di Azure AD per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fbad0-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="fbad0-188">**Reindirizzamento disconnessione SAML (facoltativo)** -</span><span class="sxs-lookup"><span data-stu-id="fbad0-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="fbad0-189">È possibile scegliere toooptionally configurare un Url di disconnessione SAML, che può essere utilizzato toopoint nella pagina di disconnessione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbad0-189">You can choose toooptionally configure a SAML Logout Url, which can be used toopoint at Azure AD's logout page.</span></span> <span data-ttu-id="fbad0-190">Quando questa impostazione è abilitata e configurata, l'utente hello non saranno pagina di disconnessione toohello diretti all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fbad0-190">When this setting is enabled and configured, hello user will no longer be directed toohello Workplace logout page.</span></span> <span data-ttu-id="fbad0-191">In alternativa, utente hello sarà reindirizzato toohello url che è stato aggiunto in base alle impostazioni di reindirizzamento disconnessione SAML hello.</span><span class="sxs-lookup"><span data-stu-id="fbad0-191">Instead, hello user will be redirected toohello url that was added in hello SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="fbad0-192">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="fbad0-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fbad0-193">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="fbad0-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fbad0-194">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbad0-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="fbad0-195">Configurazione della frequenza di riautenticazione</span><span class="sxs-lookup"><span data-stu-id="fbad0-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="fbad0-196">È possibile configurare tooprompt all'area di lavoro per un controllo SAML ogni giorno, tre giorni, settimane, due settimane, mesi o mai.</span><span class="sxs-lookup"><span data-stu-id="fbad0-196">You can configure Workplace tooprompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="fbad0-197">Hello valore minimo per il controllo SAML hello in applicazioni per dispositivi mobili è impostata tooone settimana.</span><span class="sxs-lookup"><span data-stu-id="fbad0-197">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="fbad0-198">È inoltre possibile forzare un SAML reimpostare per tutti gli utenti utilizzando il pulsante hello: SAML richiedono l'autenticazione per tutti gli utenti ora.</span><span class="sxs-lookup"><span data-stu-id="fbad0-198">You can also force a SAML reset for all users using hello button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbad0-199">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbad0-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbad0-200">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="fbad0-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="fbad0-202">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fbad0-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbad0-203">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fbad0-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbad0-205">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbad0-207">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="fbad0-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbad0-209">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fbad0-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbad0-211">a.</span><span class="sxs-lookup"><span data-stu-id="fbad0-211">a.</span></span> <span data-ttu-id="fbad0-212">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbad0-213">b.</span><span class="sxs-lookup"><span data-stu-id="fbad0-213">b.</span></span> <span data-ttu-id="fbad0-214">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fbad0-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbad0-215">c.</span><span class="sxs-lookup"><span data-stu-id="fbad0-215">c.</span></span> <span data-ttu-id="fbad0-216">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fbad0-217">d.</span><span class="sxs-lookup"><span data-stu-id="fbad0-217">d.</span></span> <span data-ttu-id="fbad0-218">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="fbad0-219">Creazione di un utente test di Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="fbad0-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="fbad0-220">In questa sezione si crea un utente di nome Britta Simon in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="fbad0-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="fbad0-221">Workplace by Facebook supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fbad0-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="fbad0-222">Non è necessaria alcuna azione dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="fbad0-222">There is no action for you in this section.</span></span> <span data-ttu-id="fbad0-223">Se un utente non esiste nell'area di lavoro da Facebook, una nuova istanza viene creata quando si tenta di tooaccess all'area di lavoro da Facebook.</span><span class="sxs-lookup"><span data-stu-id="fbad0-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="fbad0-224">Se è necessario toocreate manualmente, contattare l'utente [all'area di lavoro dal team di supporto Client di Facebook](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="fbad0-224">If you need toocreate a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fbad0-225">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbad0-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fbad0-226">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWorkplace da Facebook.</span><span class="sxs-lookup"><span data-stu-id="fbad0-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkplace by Facebook.</span></span>

![Assegna utente][200] 

<span data-ttu-id="fbad0-228">**tooassign tooWorkplace Britta Simon da Facebook, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fbad0-228">**tooassign Britta Simon tooWorkplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbad0-229">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="fbad0-231">Nell'elenco di applicazioni hello, selezionare **all'area di lavoro da Facebook**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-231">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="fbad0-233">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="fbad0-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-235">Click **Add** button.</span></span> <span data-ttu-id="fbad0-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="fbad0-238">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="fbad0-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fbad0-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbad0-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fbad0-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbad0-241">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fbad0-241">Testing single sign-on</span></span>

<span data-ttu-id="fbad0-242">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="fbad0-242">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>
<span data-ttu-id="fbad0-243">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbad0-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fbad0-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fbad0-244">Additional resources</span></span>

* [<span data-ttu-id="fbad0-245">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbad0-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbad0-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbad0-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fbad0-247">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="fbad0-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

