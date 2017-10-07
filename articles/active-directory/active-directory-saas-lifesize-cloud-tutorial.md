---
title: 'Esercitazione: Integrazione di Azure Active Directory con Lifesize Cloud | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e offrendo Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="77422-103">Esercitazione: Integrazione di Azure Active Directory con Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="77422-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="77422-104">In questa esercitazione, è illustrato come toointegrate offrendo Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77422-104">In this tutorial, you learn how toointegrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77422-105">Integrazione offrendo Cloud con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="77422-105">Integrating Lifesize Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="77422-106">È possibile controllare in Azure AD che ha accesso tooLifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="77422-106">You can control in Azure AD who has access tooLifesize Cloud</span></span>
- <span data-ttu-id="77422-107">È possibile abilitare l'utenti tooautomatically get connesso tooLifesize Cloud (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="77422-107">You can enable your users tooautomatically get signed-on tooLifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77422-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="77422-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="77422-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77422-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77422-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="77422-110">Prerequisites</span></span>

<span data-ttu-id="77422-111">integrazione di Azure AD con Cloud offrendo tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="77422-111">tooconfigure Azure AD integration with Lifesize Cloud, you need hello following items:</span></span>

- <span data-ttu-id="77422-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77422-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77422-113">Sottoscrizione di Lifesize Cloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="77422-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77422-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="77422-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77422-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="77422-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77422-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="77422-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77422-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77422-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77422-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="77422-118">Scenario description</span></span>
<span data-ttu-id="77422-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="77422-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77422-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="77422-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77422-121">Aggiunta di Cloud totalmente dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="77422-121">Adding Lifesize Cloud from hello gallery</span></span>
2. <span data-ttu-id="77422-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77422-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-hello-gallery"></a><span data-ttu-id="77422-123">Aggiunta di Cloud totalmente dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="77422-123">Adding Lifesize Cloud from hello gallery</span></span>
<span data-ttu-id="77422-124">integrazione hello tooconfigure di offrendo Cloud in Azure AD, è necessario tooadd offrendo Cloud dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="77422-124">tooconfigure hello integration of Lifesize Cloud into Azure AD, you need tooadd Lifesize Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77422-125">**tooadd offrendo Cloud dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="77422-125">**tooadd Lifesize Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77422-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="77422-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77422-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="77422-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="77422-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="77422-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="77422-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="77422-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="77422-133">Nella casella di ricerca hello, digitare **offrendo Cloud**.</span><span class="sxs-lookup"><span data-stu-id="77422-133">In hello search box, type **Lifesize Cloud**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="77422-135">Nel riquadro dei risultati hello, selezionare **offrendo Cloud**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="77422-135">In hello results panel, select **Lifesize Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77422-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77422-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77422-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Lifesize Cloud con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="77422-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77422-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nel Cloud offrendo è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77422-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lifesize Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="77422-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nel Cloud offrendo deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="77422-140">In other words, a link relationship between an Azure AD user and hello related user in Lifesize Cloud needs toobe established.</span></span>

<span data-ttu-id="77422-141">Nel Cloud offrendo, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="77422-141">In Lifesize Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="77422-142">tooconfigure e test Azure single sign-on AD offrendo cloud, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="77422-142">tooconfigure and test Azure AD single sign-on with Lifesize Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77422-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="77422-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77422-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77422-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77422-145">**[Creazione di un utente test offrendo Cloud](#creating-a-lifesize-cloud-test-user)**  -toohave un equivalente di Britta Simon in Cloud offrendo rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="77422-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - toohave a counterpart of Britta Simon in Lifesize Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="77422-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="77422-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77422-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="77422-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77422-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77422-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77422-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Cloud totalmente.</span><span class="sxs-lookup"><span data-stu-id="77422-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="77422-150">**Azure AD tooconfigure single sign-on con offrendo Cloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="77422-150">**tooconfigure Azure AD single sign-on with Lifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="77422-151">Nel portale di Azure su hello hello **offrendo Cloud** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="77422-151">In hello Azure portal, on hello **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="77422-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="77422-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="77422-155">In hello **offrendo Cloud dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77422-155">On hello **Lifesize Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="77422-157">a.</span><span class="sxs-lookup"><span data-stu-id="77422-157">a.</span></span> <span data-ttu-id="77422-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="77422-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="77422-159">b.</span><span class="sxs-lookup"><span data-stu-id="77422-159">b.</span></span> <span data-ttu-id="77422-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="77422-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="77422-161">Controllare **Mostra URL impostazioni avanzate**, eseguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="77422-161">Check **Show advanced URL settings**, perform hello following step:</span></span>  
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="77422-163">In hello **inoltro stato** casella di testo, digitare un URL utilizzando hello seguente modello:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="77422-163">In hello **Relay state** textbox, type a URL using hello following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="77422-164">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="77422-164">Please note that these are not hello real values.</span></span> <span data-ttu-id="77422-165">Hai tooupdate questi valori con hello effettivo URL Sign-On, lo stato di inoltro e identificatore.</span><span class="sxs-lookup"><span data-stu-id="77422-165">you have tooupdate these values with hello actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="77422-166">Contatto [team di supporto offrendo Cloud Client](https://www.lifesize.com/support) tooget Sign-On URL e valori dell'identificatore e ottenere il valore di stato inoltro dalla configurazione di SSO descritto più avanti nell'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="77422-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) tooget Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in hello tutorial.</span></span>

4. <span data-ttu-id="77422-167">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="77422-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="77422-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="77422-169">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77422-171">In hello **configurazione Cloud offrendo** fare clic su **configurare Cloud offrendo** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="77422-171">On hello **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="77422-172">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="77422-172">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="77422-174">tooget SSO è configurato per l'applicazione, l'account di accesso in hello applicazione Cloud offrendo con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="77422-174">tooget SSO configured for your application, login into hello Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="77422-175">In hello angolo superiore destro, fare clic sul proprio nome e quindi fare clic su hello **impostazioni di anticipo**.</span><span class="sxs-lookup"><span data-stu-id="77422-175">In hello top right corner click on your name and then click on hello **Advance Settings**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="77422-177">In impostazioni avanzate fare clic su hello hello **configurazione di SSO** collegamento.</span><span class="sxs-lookup"><span data-stu-id="77422-177">In hello Advance Settings now click on hello **SSO Configuration** link.</span></span> <span data-ttu-id="77422-178">Si aprirà hello pagina di configurazione SSO per l'istanza.</span><span class="sxs-lookup"><span data-stu-id="77422-178">It will open hello SSO Configuration page for your instance.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="77422-180">Configurare ora hello seguente i valori nella configurazione di SSO hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="77422-180">Now configure hello following values in hello SSO configuration UI.</span></span>    
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="77422-182">a.</span><span class="sxs-lookup"><span data-stu-id="77422-182">a.</span></span> <span data-ttu-id="77422-183">In **Identity Provider Issuer** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="77422-183">In **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="77422-184">b.</span><span class="sxs-lookup"><span data-stu-id="77422-184">b.</span></span>  <span data-ttu-id="77422-185">In **URL di accesso** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="77422-185">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="77422-186">c.</span><span class="sxs-lookup"><span data-stu-id="77422-186">c.</span></span> <span data-ttu-id="77422-187">Aprire il certificato con codifica base 64 nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="77422-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="77422-188">d.</span><span class="sxs-lookup"><span data-stu-id="77422-188">d.</span></span> <span data-ttu-id="77422-189">In hello attributo SAML mapping per la casella di testo Nome hello immettere il valore di hello come **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="77422-189">In hello SAML Attribute mappings for hello First Name text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="77422-190">e.</span><span class="sxs-lookup"><span data-stu-id="77422-190">e.</span></span> <span data-ttu-id="77422-191">Nel mapping di attributi SAML hello per hello **cognome** casella di testo immettere il valore di hello come **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="77422-191">In hello SAML Attribute mapping for hello **Last Name** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="77422-192">f.</span><span class="sxs-lookup"><span data-stu-id="77422-192">f.</span></span> <span data-ttu-id="77422-193">Nel mapping di attributi SAML hello per hello **posta elettronica** casella di testo immettere il valore di hello come **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="77422-193">In hello SAML Attribute mapping for hello **Email** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="77422-194">configurazione di hello toocheck è possibile fare clic su hello **Test** pulsante.</span><span class="sxs-lookup"><span data-stu-id="77422-194">toocheck hello configuration you can click on hello **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="77422-195">Per il test ha esito positivo è necessario configurazione guidata di toocomplete hello in Azure AD e forniscono anche accesso toousers o gruppi che possono eseguire test hello.</span><span class="sxs-lookup"><span data-stu-id="77422-195">For successful testing you need toocomplete hello configuration wizard in Azure AD and also provide access toousers or groups who can perform hello test.</span></span>

12. <span data-ttu-id="77422-196">Per abilitare SSO hello controllo hello **abilitare SSO** pulsante.</span><span class="sxs-lookup"><span data-stu-id="77422-196">Enable hello SSO by checking on hello **Enable SSO** button.</span></span>

13. <span data-ttu-id="77422-197">Fare clic su hello **aggiornamento** pulsante in modo che tutte le impostazioni di hello vengono salvate.</span><span class="sxs-lookup"><span data-stu-id="77422-197">Now click on hello **Update** button so that all hello settings are saved.</span></span> <span data-ttu-id="77422-198">Verrà generato il valore di RelayState hello.</span><span class="sxs-lookup"><span data-stu-id="77422-198">This will generate hello RelayState value.</span></span> <span data-ttu-id="77422-199">Hello copia valore RelayState, che viene generato nella casella di testo hello, incollarlo in hello **stato inoltro** casella di testo in **offrendo Cloud dominio e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="77422-199">Copy hello RelayState value, which is generated in hello text box, paste it in hello **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="77422-200">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="77422-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="77422-201">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="77422-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="77422-202">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77422-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77422-203">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77422-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="77422-204">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="77422-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="77422-206">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="77422-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77422-207">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="77422-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77422-209">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="77422-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77422-211">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="77422-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77422-213">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77422-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77422-215">a.</span><span class="sxs-lookup"><span data-stu-id="77422-215">a.</span></span> <span data-ttu-id="77422-216">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77422-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77422-217">b.</span><span class="sxs-lookup"><span data-stu-id="77422-217">b.</span></span> <span data-ttu-id="77422-218">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="77422-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77422-219">c.</span><span class="sxs-lookup"><span data-stu-id="77422-219">c.</span></span> <span data-ttu-id="77422-220">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="77422-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="77422-221">d.</span><span class="sxs-lookup"><span data-stu-id="77422-221">d.</span></span> <span data-ttu-id="77422-222">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="77422-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="77422-223">Creazione di un utente di test di Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="77422-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="77422-224">In questa sezione viene creato un utente chiamato Britta Simon in Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="77422-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="77422-225">Lifesize Cloud supporta il provisioning utenti automatico.</span><span class="sxs-lookup"><span data-stu-id="77422-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="77422-226">Dopo l'autenticazione in Azure AD, hello utente verrà eseguito automaticamente il provisioning in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="77422-226">After successful authentication at Azure AD, hello user will be automatically provisioned in hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="77422-227">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="77422-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="77422-228">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="77422-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLifesize Cloud.</span></span>

![Assegna utente][200] 

<span data-ttu-id="77422-230">**tooassign Britta Simon tooLifesize Cloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="77422-230">**tooassign Britta Simon tooLifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="77422-231">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="77422-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="77422-233">Nell'elenco di applicazioni hello, selezionare **offrendo Cloud**.</span><span class="sxs-lookup"><span data-stu-id="77422-233">In hello applications list, select **Lifesize Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="77422-235">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="77422-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="77422-237">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="77422-237">Click **Add** button.</span></span> <span data-ttu-id="77422-238">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="77422-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="77422-240">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="77422-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="77422-241">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="77422-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77422-242">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="77422-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77422-243">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="77422-243">Testing single sign-on</span></span>

<span data-ttu-id="77422-244">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="77422-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="77422-245">Quando si fa clic hello offrendo Cloud riquadro in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione Cloud totalmente.</span><span class="sxs-lookup"><span data-stu-id="77422-245">When you click hello Lifesize Cloud tile in hello Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="77422-246">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="77422-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77422-247">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="77422-247">Additional resources</span></span>

* [<span data-ttu-id="77422-248">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77422-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77422-249">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77422-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

