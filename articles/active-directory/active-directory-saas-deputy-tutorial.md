---
title: 'Esercitazione: Integrazione di Azure Active Directory con Deputy | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e vice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="1251b-103">Esercitazione: Integrazione di Azure Active Directory con Deputy</span><span class="sxs-lookup"><span data-stu-id="1251b-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="1251b-104">In questa esercitazione, è illustrato come toointegrate vicepresidente con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1251b-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1251b-105">Integrazione vicepresidente con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1251b-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1251b-106">È possibile controllare in Azure AD che ha accesso tooDeputy</span><span class="sxs-lookup"><span data-stu-id="1251b-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="1251b-107">È possibile abilitare l'utenti tooautomatically get connesso tooDeputy (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1251b-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1251b-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1251b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1251b-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1251b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1251b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1251b-110">Prerequisites</span></span>

<span data-ttu-id="1251b-111">integrazione di Azure AD con vicepresidente tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1251b-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="1251b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1251b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1251b-113">Sottoscrizione di Deputy abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1251b-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1251b-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1251b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1251b-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1251b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1251b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1251b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1251b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1251b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1251b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1251b-118">Scenario description</span></span>
<span data-ttu-id="1251b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1251b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1251b-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1251b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1251b-121">Aggiunta di vicepresidente dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1251b-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="1251b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1251b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="1251b-123">Aggiunta di vicepresidente dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1251b-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="1251b-124">integrazione hello tooconfigure di vicepresidente in Azure AD, è necessario tooadd vicepresidente dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1251b-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1251b-125">**tooadd vicepresidente dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1251b-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1251b-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1251b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1251b-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1251b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1251b-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1251b-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1251b-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1251b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1251b-133">Nella casella di ricerca hello, digitare **vicepresidente**.</span><span class="sxs-lookup"><span data-stu-id="1251b-133">In hello search box, type **Deputy**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="1251b-135">Nel riquadro dei risultati hello, selezionare **vicepresidente**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1251b-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1251b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1251b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1251b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Deputy mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1251b-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1251b-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in vicepresidente è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1251b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="1251b-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlati hello vicepresidente deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1251b-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="1251b-141">In parte, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1251b-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1251b-142">tooconfigure e prova AD Azure single sign-on con vicepresidente, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1251b-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1251b-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1251b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1251b-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1251b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1251b-145">**[Creazione di un utente test vicepresidente](#creating-a-deputy-test-user)**  -toohave un equivalente di Britta Simon nella parte che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1251b-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1251b-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1251b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1251b-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1251b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1251b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1251b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1251b-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione vicepresidente.</span><span class="sxs-lookup"><span data-stu-id="1251b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="1251b-150">**Azure AD tooconfigure single sign-on con vicepresidente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1251b-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="1251b-151">Nel portale di Azure su hello hello **vicepresidente** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1251b-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1251b-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1251b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="1251b-155">In hello **vicepresidente dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="1251b-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="1251b-157">a.</span><span class="sxs-lookup"><span data-stu-id="1251b-157">a.</span></span> <span data-ttu-id="1251b-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="1251b-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="1251b-159">b.</span><span class="sxs-lookup"><span data-stu-id="1251b-159">b.</span></span> <span data-ttu-id="1251b-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="1251b-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="1251b-161">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="1251b-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="1251b-162">Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="1251b-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="1251b-164">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="1251b-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="1251b-165">Il suffisso di area di Deputy è facoltativo. Se usato deve essere uno dei seguenti: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="1251b-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1251b-166">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="1251b-166">These values are not real.</span></span> <span data-ttu-id="1251b-167">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1251b-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1251b-168">Contatto [team di supporto vicepresidente](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="1251b-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="1251b-169">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1251b-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="1251b-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1251b-171">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1251b-173">In hello **configurazione vicepresidente** fare clic su **configurare vicepresidente** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="1251b-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1251b-174">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1251b-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="1251b-176">Passare l'URL seguente toohello:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="1251b-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="1251b-177">Andare troppo**le impostazioni di sicurezza** e fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="1251b-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="1251b-179">In questa pagina **Security Settings** (Impostazioni di sicurezza) attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="1251b-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="1251b-181">a.</span><span class="sxs-lookup"><span data-stu-id="1251b-181">a.</span></span> <span data-ttu-id="1251b-182">Abilitare **Social Login**(Accesso social).</span><span class="sxs-lookup"><span data-stu-id="1251b-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="1251b-183">b.</span><span class="sxs-lookup"><span data-stu-id="1251b-183">b.</span></span> <span data-ttu-id="1251b-184">Aprire il certificato con codificata Base64 scaricato dal portale di Azure nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato OpenSSL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="1251b-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="1251b-185">c.</span><span class="sxs-lookup"><span data-stu-id="1251b-185">c.</span></span> <span data-ttu-id="1251b-186">Nella casella di testo URL SSO SAML hello, digitare`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="1251b-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="1251b-187">d.</span><span class="sxs-lookup"><span data-stu-id="1251b-187">d.</span></span> <span data-ttu-id="1251b-188">Nella casella di testo URL SSO SAML hello sostituire `<your subdomain>` con il sottodominio.</span><span class="sxs-lookup"><span data-stu-id="1251b-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="1251b-189">e.</span><span class="sxs-lookup"><span data-stu-id="1251b-189">e.</span></span> <span data-ttu-id="1251b-190">Nella casella di testo URL SSO SAML hello sostituire `<saml sso url>` con hello **SAML Single Sign-On Service URL** copiata da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1251b-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="1251b-191">f.</span><span class="sxs-lookup"><span data-stu-id="1251b-191">f.</span></span> <span data-ttu-id="1251b-192">Fare clic su **Salva impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="1251b-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="1251b-193">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1251b-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1251b-194">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1251b-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1251b-195">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1251b-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1251b-196">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1251b-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="1251b-197">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1251b-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1251b-199">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1251b-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1251b-200">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1251b-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1251b-202">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1251b-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1251b-204">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1251b-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1251b-206">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1251b-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1251b-208">a.</span><span class="sxs-lookup"><span data-stu-id="1251b-208">a.</span></span> <span data-ttu-id="1251b-209">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1251b-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1251b-210">b.</span><span class="sxs-lookup"><span data-stu-id="1251b-210">b.</span></span> <span data-ttu-id="1251b-211">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1251b-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1251b-212">c.</span><span class="sxs-lookup"><span data-stu-id="1251b-212">c.</span></span> <span data-ttu-id="1251b-213">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1251b-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1251b-214">d.</span><span class="sxs-lookup"><span data-stu-id="1251b-214">d.</span></span> <span data-ttu-id="1251b-215">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1251b-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="1251b-216">Creazione di un utente test di Deputy</span><span class="sxs-lookup"><span data-stu-id="1251b-216">Creating a Deputy test user</span></span>

<span data-ttu-id="1251b-217">toolog agli utenti di Azure AD tooenable in tooDeputy, è necessario eseguirne il provisioning in parte.</span><span class="sxs-lookup"><span data-stu-id="1251b-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="1251b-218">Nel caso di Deputy il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="1251b-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="1251b-219">tooprovision un account utente, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1251b-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="1251b-220">Accedere nel sito della società di vicepresidente tooyour come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1251b-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="1251b-221">Nel riquadro di spostamento superiore hello, fare clic su **persone**.</span><span class="sxs-lookup"><span data-stu-id="1251b-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="1251b-222">![Persone](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="1251b-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="1251b-223">Fare clic su hello **aggiungere persone** scegliere **aggiungere una sola persona**.</span><span class="sxs-lookup"><span data-stu-id="1251b-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="1251b-224">![Aggiungere persone](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Aggiungere persone")</span><span class="sxs-lookup"><span data-stu-id="1251b-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="1251b-225">Eseguire hello alla procedura seguente e fare clic su **salvare e invitare**.</span><span class="sxs-lookup"><span data-stu-id="1251b-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="1251b-226">![Nuovo utente](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="1251b-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="1251b-227">a.</span><span class="sxs-lookup"><span data-stu-id="1251b-227">a.</span></span> <span data-ttu-id="1251b-228">In hello **nome** casella di testo, nome del tipo di utente hello come **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1251b-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="1251b-229">b.</span><span class="sxs-lookup"><span data-stu-id="1251b-229">b.</span></span> <span data-ttu-id="1251b-230">In hello **posta elettronica** casella Tipo hello di indirizzo di posta elettronica di un account di Azure AD si vuole tooprovision.</span><span class="sxs-lookup"><span data-stu-id="1251b-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="1251b-231">c.</span><span class="sxs-lookup"><span data-stu-id="1251b-231">c.</span></span> <span data-ttu-id="1251b-232">In hello **lavorare** casella di testo, nome del tipo hello business.</span><span class="sxs-lookup"><span data-stu-id="1251b-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="1251b-233">d.</span><span class="sxs-lookup"><span data-stu-id="1251b-233">d.</span></span> <span data-ttu-id="1251b-234">Fare clic sul pulsante **Save & Invite** (Salva e invita).</span><span class="sxs-lookup"><span data-stu-id="1251b-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="1251b-235">titolare dell'account AAD Hello riceve un messaggio di posta elettronica e segue il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="1251b-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="1251b-236">È possibile usare qualsiasi altro vicepresidente utente account strumento di creazione o le API fornite da vicepresidente tooprovision AAD gli account utente.</span><span class="sxs-lookup"><span data-stu-id="1251b-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1251b-237">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1251b-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1251b-238">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooDeputy.</span><span class="sxs-lookup"><span data-stu-id="1251b-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1251b-240">**tooassign Britta Simon tooDeputy, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1251b-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="1251b-241">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1251b-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1251b-243">Nell'elenco di applicazioni hello, selezionare **vicepresidente**.</span><span class="sxs-lookup"><span data-stu-id="1251b-243">In hello applications list, select **Deputy**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="1251b-245">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1251b-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1251b-247">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1251b-247">Click **Add** button.</span></span> <span data-ttu-id="1251b-248">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1251b-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1251b-250">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1251b-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1251b-251">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1251b-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1251b-252">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1251b-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1251b-253">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1251b-253">Testing single sign-on</span></span>

<span data-ttu-id="1251b-254">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1251b-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="1251b-255">Quando si fa clic hello vicepresidente riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour vicepresidente applicazione.</span><span class="sxs-lookup"><span data-stu-id="1251b-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1251b-256">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1251b-256">Additional resources</span></span>

* [<span data-ttu-id="1251b-257">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1251b-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1251b-258">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1251b-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

