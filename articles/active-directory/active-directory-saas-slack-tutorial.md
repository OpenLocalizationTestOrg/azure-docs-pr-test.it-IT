---
title: 'Esercitazione: Integrazione di Azure Active Directory con Slack | Microsoft Docs'
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e il margine di flessibilità."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="c0b39-103">Esercitazione: Integrazione di Azure Active Directory con Slack</span><span class="sxs-lookup"><span data-stu-id="c0b39-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="c0b39-104">In questa esercitazione, è illustrato come margine di flessibilità toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0b39-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0b39-105">Integrazione di Slack con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="c0b39-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c0b39-106">È possibile controllare in Azure AD che ha accesso tooSlack</span><span class="sxs-lookup"><span data-stu-id="c0b39-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="c0b39-107">È possibile abilitare l'utenti tooautomatically get connesso tooSlack (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0b39-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0b39-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c0b39-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c0b39-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0b39-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0b39-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c0b39-110">Prerequisites</span></span>

<span data-ttu-id="c0b39-111">integrazione di Azure AD con Slack tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="c0b39-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="c0b39-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0b39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0b39-113">Sottoscrizione di Slack abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c0b39-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0b39-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="c0b39-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0b39-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="c0b39-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0b39-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c0b39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0b39-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0b39-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0b39-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c0b39-118">Scenario description</span></span>
<span data-ttu-id="c0b39-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c0b39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0b39-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="c0b39-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0b39-121">Aggiunta di Slack dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c0b39-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="c0b39-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0b39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="c0b39-123">Aggiunta di Slack dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c0b39-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="c0b39-124">integrazione di hello tooconfigure di Slack in Azure AD, è necessario tooadd Slack dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c0b39-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c0b39-125">**tooadd Slack dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c0b39-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0b39-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c0b39-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0b39-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c0b39-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c0b39-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c0b39-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c0b39-133">Nella casella di ricerca hello, digitare **Slack**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-133">In hello search box, type **Slack**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="c0b39-135">Nel riquadro dei risultati hello, selezionare **Slack**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c0b39-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0b39-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0b39-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0b39-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Slack con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c0b39-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0b39-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Slack è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0b39-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="c0b39-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Slack deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="c0b39-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="c0b39-141">In Slack, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="c0b39-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c0b39-142">tooconfigure e prova AD Azure single sign-on con il margine di flessibilità, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="c0b39-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c0b39-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c0b39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c0b39-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0b39-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0b39-145">**[Creazione di un utente test Slack](#creating-a-slack-test-user)**  -toohave un equivalente di Britta Simon in Slack che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c0b39-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0b39-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c0b39-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0b39-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="c0b39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0b39-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0b39-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0b39-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Slack.</span><span class="sxs-lookup"><span data-stu-id="c0b39-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="c0b39-150">**Azure AD tooconfigure single sign-on con Slack, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c0b39-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0b39-151">Nel portale di Azure su hello hello **Slack** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c0b39-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c0b39-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="c0b39-155">In hello **Slack dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c0b39-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="c0b39-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0b39-157">a.</span></span> <span data-ttu-id="c0b39-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="c0b39-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="c0b39-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0b39-159">b.</span></span> <span data-ttu-id="c0b39-160">In hello **identificatore** casella di testo, digitare l'URL hello:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="c0b39-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0b39-161">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="c0b39-161">hello value is not real.</span></span> <span data-ttu-id="c0b39-162">È il valore hello tooupdate con hello effettivo URL di accesso.</span><span class="sxs-lookup"><span data-stu-id="c0b39-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="c0b39-163">Contatto [team di supporto Slack](https://slack.com/help/contact) valore hello tooget</span><span class="sxs-lookup"><span data-stu-id="c0b39-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="c0b39-164">Applicazione slack prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="c0b39-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c0b39-165">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="c0b39-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="c0b39-166">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c0b39-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="c0b39-167">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="c0b39-167">hello following screenshot shows an example for this.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="c0b39-169">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo Seleziona **user.mail** come **identificatore utente** e per ogni riga visualizzata Nella tabella hello riportata di seguito, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c0b39-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="c0b39-170">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="c0b39-170">Attribute Name</span></span> | <span data-ttu-id="c0b39-171">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="c0b39-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="c0b39-172">first_name</span><span class="sxs-lookup"><span data-stu-id="c0b39-172">first_name</span></span> | <span data-ttu-id="c0b39-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c0b39-173">user.givenname</span></span> |
    | <span data-ttu-id="c0b39-174">last_name</span><span class="sxs-lookup"><span data-stu-id="c0b39-174">last_name</span></span> | <span data-ttu-id="c0b39-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="c0b39-175">user.surname</span></span> |
    | <span data-ttu-id="c0b39-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="c0b39-176">User.Email</span></span> | <span data-ttu-id="c0b39-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="c0b39-177">user.mail</span></span> |  
    | <span data-ttu-id="c0b39-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="c0b39-178">User.Username</span></span> | <span data-ttu-id="c0b39-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="c0b39-179">user.userprincipalname</span></span> |

    <span data-ttu-id="c0b39-180">a.</span><span class="sxs-lookup"><span data-stu-id="c0b39-180">a.</span></span> <span data-ttu-id="c0b39-181">Fare clic su **attributo** tooopen **Modifica attributo** finestra di dialogo casella ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c0b39-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="c0b39-183">a.</span><span class="sxs-lookup"><span data-stu-id="c0b39-183">a.</span></span> <span data-ttu-id="c0b39-184">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="c0b39-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c0b39-185">b.</span><span class="sxs-lookup"><span data-stu-id="c0b39-185">b.</span></span> <span data-ttu-id="c0b39-186">Da hello **valore** elenco, il valore di attributo hello selezionare mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="c0b39-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c0b39-187">c.</span><span class="sxs-lookup"><span data-stu-id="c0b39-187">c.</span></span> <span data-ttu-id="c0b39-188">Fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="c0b39-188">Click **OK**</span></span>

6. <span data-ttu-id="c0b39-189">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c0b39-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="c0b39-191">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c0b39-191">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c0b39-193">In hello **configurazione Slack** fare clic su **configurare Slack** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="c0b39-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c0b39-194">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="c0b39-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="c0b39-196">In una finestra del web browser, accedere come amministratore nel sito della società Slack tooyour.</span><span class="sxs-lookup"><span data-stu-id="c0b39-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="c0b39-197">Passare troppo**Microsoft Azure AD** andare troppo**le impostazioni del Team**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="c0b39-199">In hello **le impostazioni del Team** fare clic su hello **autenticazione** scheda e quindi fare clic su **Cambia impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="c0b39-201">In hello **SAML Authentication Settings** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c0b39-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="c0b39-203">a.</span><span class="sxs-lookup"><span data-stu-id="c0b39-203">a.</span></span>  <span data-ttu-id="c0b39-204">In hello **SAML 2.0 Endpoint (HTTP)** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0b39-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c0b39-205">b.</span><span class="sxs-lookup"><span data-stu-id="c0b39-205">b.</span></span>  <span data-ttu-id="c0b39-206">In hello **Identity Provider Issuer** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0b39-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c0b39-207">c.</span><span class="sxs-lookup"><span data-stu-id="c0b39-207">c.</span></span>  <span data-ttu-id="c0b39-208">Aprire il file di certificato scaricato nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato pubblico** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="c0b39-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="c0b39-209">d.</span><span class="sxs-lookup"><span data-stu-id="c0b39-209">d.</span></span> <span data-ttu-id="c0b39-210">Configurare hello sopra e tre le impostazioni appropriate per il team di flessibilità.</span><span class="sxs-lookup"><span data-stu-id="c0b39-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="c0b39-211">Per ulteriori informazioni sulle impostazioni di hello, trovare hello **Guida alla configurazione di SSO del margine di flessibilità** qui.</span><span class="sxs-lookup"><span data-stu-id="c0b39-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="c0b39-212">e.</span><span class="sxs-lookup"><span data-stu-id="c0b39-212">e.</span></span>  <span data-ttu-id="c0b39-213">Fare clic su **Salva configurazione**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="c0b39-214">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="c0b39-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c0b39-215">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c0b39-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c0b39-216">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0b39-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0b39-217">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0b39-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0b39-218">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c0b39-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c0b39-220">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c0b39-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0b39-221">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c0b39-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0b39-223">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0b39-225">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="c0b39-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0b39-227">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c0b39-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0b39-229">a.</span><span class="sxs-lookup"><span data-stu-id="c0b39-229">a.</span></span> <span data-ttu-id="c0b39-230">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0b39-231">b.</span><span class="sxs-lookup"><span data-stu-id="c0b39-231">b.</span></span> <span data-ttu-id="c0b39-232">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0b39-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0b39-233">c.</span><span class="sxs-lookup"><span data-stu-id="c0b39-233">c.</span></span> <span data-ttu-id="c0b39-234">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c0b39-235">d.</span><span class="sxs-lookup"><span data-stu-id="c0b39-235">d.</span></span> <span data-ttu-id="c0b39-236">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="c0b39-237">Creazione di un utente test di Slack</span><span class="sxs-lookup"><span data-stu-id="c0b39-237">Creating a Slack test user</span></span>

<span data-ttu-id="c0b39-238">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Slack toocreate.</span><span class="sxs-lookup"><span data-stu-id="c0b39-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="c0b39-239">Slack supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c0b39-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="c0b39-240">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="c0b39-240">There is no action item for you in this section.</span></span> <span data-ttu-id="c0b39-241">Se non esiste ancora, viene creato un nuovo utente durante un tooaccess tentativo Slack.</span><span class="sxs-lookup"><span data-stu-id="c0b39-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="c0b39-242">Se è necessario un utente toocreate manualmente, è necessario tooContact [team di supporto Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="c0b39-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c0b39-243">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0b39-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c0b39-244">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSlack.</span><span class="sxs-lookup"><span data-stu-id="c0b39-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c0b39-246">**tooassign Britta Simon tooSlack, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c0b39-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0b39-247">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c0b39-249">Nell'elenco di applicazioni hello, selezionare **Slack**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-249">In hello applications list, select **Slack**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="c0b39-251">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c0b39-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-253">Click **Add** button.</span></span> <span data-ttu-id="c0b39-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c0b39-256">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="c0b39-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c0b39-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0b39-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c0b39-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0b39-259">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c0b39-259">Testing single sign-on</span></span>

<span data-ttu-id="c0b39-260">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c0b39-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c0b39-261">Quando si fa clic sul riquadro Slack hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Slack applicazione.</span><span class="sxs-lookup"><span data-stu-id="c0b39-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0b39-262">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c0b39-262">Additional resources</span></span>

* [<span data-ttu-id="c0b39-263">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0b39-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0b39-264">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0b39-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

