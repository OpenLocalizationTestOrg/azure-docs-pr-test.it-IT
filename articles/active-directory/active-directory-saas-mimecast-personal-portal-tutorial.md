---
title: 'Esercitazione: Integrazione di Azure Active Directory con Mimecast Personal Portal | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Mimecast Personal Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="ab4a2-103">Esercitazione: Integrazione di Azure Active Directory con Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="ab4a2-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="ab4a2-104">In questa esercitazione, è illustrato come toointegrate Mimecast Personal Portal con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ab4a2-104">In this tutorial, you learn how toointegrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab4a2-105">Integrazione di Mimecast Personal Portal con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-105">Integrating Mimecast Personal Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ab4a2-106">È possibile controllare in Azure AD che ha accesso tooMimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="ab4a2-106">You can control in Azure AD who has access tooMimecast Personal Portal</span></span>
- <span data-ttu-id="ab4a2-107">È possibile abilitare l'utenti tooautomatically get connesso tooMimecast Personal Portal (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab4a2-107">You can enable your users tooautomatically get signed-on tooMimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ab4a2-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ab4a2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ab4a2-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab4a2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab4a2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ab4a2-110">Prerequisites</span></span>

<span data-ttu-id="ab4a2-111">tooconfigure integrazione di Azure AD con Mimecast Personal Portal, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-111">tooconfigure Azure AD integration with Mimecast Personal Portal, you need hello following items:</span></span>

- <span data-ttu-id="ab4a2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab4a2-113">Sottoscrizione di Mimecast Personal Portal abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ab4a2-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab4a2-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab4a2-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab4a2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ab4a2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab4a2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab4a2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ab4a2-118">Scenario description</span></span>
<span data-ttu-id="ab4a2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab4a2-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab4a2-121">Aggiunta di Mimecast Personal Portal dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ab4a2-121">Adding Mimecast Personal Portal from hello gallery</span></span>
2. <span data-ttu-id="ab4a2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab4a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a><span data-ttu-id="ab4a2-123">Aggiunta di Mimecast Personal Portal dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ab4a2-123">Adding Mimecast Personal Portal from hello gallery</span></span>
<span data-ttu-id="ab4a2-124">integrazione hello tooconfigure di Mimecast Personal Portal in Azure AD, è necessario tooadd Mimecast Personal Portal dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-124">tooconfigure hello integration of Mimecast Personal Portal into Azure AD, you need tooadd Mimecast Personal Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ab4a2-125">**tooadd Mimecast Personal Portal dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ab4a2-125">**tooadd Mimecast Personal Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab4a2-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ab4a2-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ab4a2-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ab4a2-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ab4a2-133">Nella casella di ricerca hello, digitare **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-133">In hello search box, type **Mimecast Personal Portal**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="ab4a2-135">Nel riquadro dei risultati hello, selezionare **Mimecast Personal Portal**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-135">In hello results panel, select **Mimecast Personal Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ab4a2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab4a2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ab4a2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Mimecast Personal Portal con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ab4a2-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ab4a2-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Mimecast Personal Portal è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Personal Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="ab4a2-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Mimecast Personal Portal deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-140">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Personal Portal needs toobe established.</span></span>

<span data-ttu-id="ab4a2-141">In Mimecast Personal Portal, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-141">In Mimecast Personal Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ab4a2-142">tooconfigure e prova AD Azure single sign-on con Mimecast Personal Portal, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-142">tooconfigure and test Azure AD single sign-on with Mimecast Personal Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ab4a2-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ab4a2-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab4a2-145">**[Creazione di un utente test Mimecast Personal Portal](#creating-a-mimecast-personal-portal-test-user)**  -toohave un equivalente di Britta Simon in Mimecast Personal Portal che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - toohave a counterpart of Britta Simon in Mimecast Personal Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab4a2-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab4a2-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ab4a2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab4a2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ab4a2-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="ab4a2-150">**tooconfigure AD Azure single sign-on con Mimecast Personal Portal, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ab4a2-150">**tooconfigure Azure AD single sign-on with Mimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab4a2-151">Nel portale di Azure su hello hello **Mimecast Personal Portal** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-151">In hello Azure portal, on hello **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ab4a2-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="ab4a2-155">In hello **Mimecast Personal Portal dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-155">On hello **Mimecast Personal Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="ab4a2-157">a.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-157">a.</span></span> <span data-ttu-id="ab4a2-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="ab4a2-159">b.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-159">b.</span></span> <span data-ttu-id="ab4a2-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="ab4a2-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ab4a2-161">These values are not real.</span></span> <span data-ttu-id="ab4a2-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ab4a2-163">Contatto [team di supporto Client di Mimecast Personal Portal](https://www.mimecast.com/customer-success/technical-support/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) tooget these values.</span></span> 
 


4. <span data-ttu-id="ab4a2-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="ab4a2-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ab4a2-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ab4a2-168">In hello **Mimecast Personal Portal configurazione** fare clic su **configurare Mimecast Personal Portal** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-168">On hello **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ab4a2-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ab4a2-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="ab4a2-171">In un'altra finestra del Web browser accedere a Mimecast Personal Portal come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="ab4a2-172">Andare troppo**servizi \> applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-172">Go too**Services \> Applications**.</span></span>
   
    <span data-ttu-id="ab4a2-173">![Applicazioni](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="ab4a2-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="ab4a2-174">Fare clic su **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="ab4a2-175">![Profili di autenticazione](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Profili di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="ab4a2-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="ab4a2-176">Fare clic su **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="ab4a2-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span><span class="sxs-lookup"><span data-stu-id="ab4a2-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="ab4a2-178">In hello **Authentication Profile** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-178">In hello **Authentication Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ab4a2-179">![Profilo di autenticazione](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Profilo di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="ab4a2-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="ab4a2-180">a.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-180">a.</span></span> <span data-ttu-id="ab4a2-181">In hello **descrizione** casella di testo, digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-181">In hello **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="ab4a2-182">b.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-182">b.</span></span> <span data-ttu-id="ab4a2-183">Selezionare **Enforce SAML Authentication for Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="ab4a2-184">c.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-184">c.</span></span> <span data-ttu-id="ab4a2-185">Come **Provider** selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="ab4a2-186">d.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-186">d.</span></span> <span data-ttu-id="ab4a2-187">In **URL autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-187">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="ab4a2-188">e.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-188">e.</span></span> <span data-ttu-id="ab4a2-189">In **URL di accesso** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-189">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="ab4a2-190">f.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-190">f.</span></span> <span data-ttu-id="ab4a2-191">In **Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-191">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ab4a2-192">g.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-192">g.</span></span> <span data-ttu-id="ab4a2-193">Aprire il **base 64** codificato nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti, certificato e quindi incollarlo toohello **Identity Provider Certificate (Metadata)** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="ab4a2-194">h.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-194">h.</span></span> <span data-ttu-id="ab4a2-195">Selezionare **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="ab4a2-196">i.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-196">i.</span></span> <span data-ttu-id="ab4a2-197">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ab4a2-198">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ab4a2-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ab4a2-199">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ab4a2-200">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ab4a2-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ab4a2-201">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab4a2-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="ab4a2-202">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ab4a2-204">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ab4a2-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab4a2-205">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ab4a2-207">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ab4a2-209">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ab4a2-211">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ab4a2-213">a.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-213">a.</span></span> <span data-ttu-id="ab4a2-214">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab4a2-215">b.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-215">b.</span></span> <span data-ttu-id="ab4a2-216">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ab4a2-217">c.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-217">c.</span></span> <span data-ttu-id="ab4a2-218">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ab4a2-219">d.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-219">d.</span></span> <span data-ttu-id="ab4a2-220">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="ab4a2-221">Creazione di un utente test di Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="ab4a2-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="ab4a2-222">In ordine tooenable Azure AD utenti toolog a Mimecast Personal Portal, è necessario eseguirne il provisioning in Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-222">In order tooenable Azure AD users toolog into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="ab4a2-223">Nel caso di hello di Mimecast Personal Portal, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-223">In hello case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="ab4a2-224">Prima di poter creare utenti, è necessario tooregister un dominio.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-224">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="ab4a2-225">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ab4a2-225">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab4a2-226">Accesso tooyour **Mimecast Personal Portal** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-226">Sign on tooyour **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="ab4a2-227">Andare troppo**directory \> interno**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-227">Go too**Directories \> Internal**.</span></span>
   
    <span data-ttu-id="ab4a2-228">![Directory](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directory")</span><span class="sxs-lookup"><span data-stu-id="ab4a2-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="ab4a2-229">Fare clic su **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="ab4a2-230">![Registra nuovo dominio](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Registra nuovo dominio")</span><span class="sxs-lookup"><span data-stu-id="ab4a2-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="ab4a2-231">Dopo aver creato il nuovo dominio, fare clic su **New Address**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="ab4a2-232">![Nuovo indirizzo](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "Nuovo indirizzo")</span><span class="sxs-lookup"><span data-stu-id="ab4a2-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="ab4a2-233">In hello indirizzo finestra di dialogo Nuovo, eseguire hello seguendo i passaggi di un valido di Azure si desidera tooprovision di account di Active Directory:</span><span class="sxs-lookup"><span data-stu-id="ab4a2-233">In hello new address dialog, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="ab4a2-234">![Salvare](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Salvare")</span><span class="sxs-lookup"><span data-stu-id="ab4a2-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="ab4a2-235">a.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-235">a.</span></span> <span data-ttu-id="ab4a2-236">In hello **indirizzo di posta elettronica** casella tipo **indirizzo di posta elettronica** dell'utente hello come  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ab4a2-236">In hello **Email Address** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="ab4a2-237">b.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-237">b.</span></span> <span data-ttu-id="ab4a2-238">In hello **nome globale** casella di testo, hello tipo **username** come **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-238">In hello **Global Name** textbox, type hello **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="ab4a2-239">c.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-239">c.</span></span> <span data-ttu-id="ab4a2-240">In hello **Password**, e **Conferma Password** nelle caselle di testo, hello tipo **Password** dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-240">In hello **Password**, and **Confirm Password** textboxes, type hello **Password** of hello user.</span></span>
   
    <span data-ttu-id="ab4a2-241">b.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-241">b.</span></span> <span data-ttu-id="ab4a2-242">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="ab4a2-243">È possibile utilizzare qualsiasi altro strumento di creazione di account utente Mimecast Personal Portal o le API fornite da account utente di Azure AD tooprovision Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ab4a2-244">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab4a2-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ab4a2-245">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooMimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Personal Portal.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ab4a2-247">**tooassign Britta Simon tooMimecast Personal Portal, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ab4a2-247">**tooassign Britta Simon tooMimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab4a2-248">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ab4a2-250">Nell'elenco di applicazioni hello, selezionare **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-250">In hello applications list, select **Mimecast Personal Portal**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="ab4a2-252">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ab4a2-254">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-254">Click **Add** button.</span></span> <span data-ttu-id="ab4a2-255">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ab4a2-257">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ab4a2-258">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab4a2-259">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ab4a2-260">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ab4a2-260">Testing single sign-on</span></span>
<span data-ttu-id="ab4a2-261">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ab4a2-262">Quando si fa clic su riquadro Mimecast Personal Portal hello in hello Pannello di accesso, è necessario ottenere applicazione Mimecast Personal Portal tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="ab4a2-262">When you click hello Mimecast Personal Portal tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Personal Portal application.</span></span> <span data-ttu-id="ab4a2-263">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ab4a2-263">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab4a2-264">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ab4a2-264">Additional resources</span></span>

* [<span data-ttu-id="ab4a2-265">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab4a2-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab4a2-266">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab4a2-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

