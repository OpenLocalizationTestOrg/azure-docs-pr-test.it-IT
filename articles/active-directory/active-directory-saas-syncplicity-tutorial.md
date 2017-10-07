---
title: 'Esercitazione: Integrazione di Azure Active Directory con Syncplicity | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Syncplicity.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="dcf02-103">Esercitazione: Integrazione di Azure Active Directory con Syncplicity</span><span class="sxs-lookup"><span data-stu-id="dcf02-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="dcf02-104">In questa esercitazione, è illustrato come toointegrate Syncplicity con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dcf02-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dcf02-105">Integrazione di Syncplicity con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="dcf02-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dcf02-106">È possibile controllare in Azure AD che ha accesso tooSyncplicity</span><span class="sxs-lookup"><span data-stu-id="dcf02-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="dcf02-107">È possibile abilitare l'utenti tooautomatically get connesso tooSyncplicity (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcf02-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dcf02-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dcf02-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dcf02-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dcf02-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcf02-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dcf02-110">Prerequisites</span></span>

<span data-ttu-id="dcf02-111">integrazione di Azure AD con Syncplicity tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="dcf02-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="dcf02-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcf02-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dcf02-113">Sottoscrizione di Syncplicity abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dcf02-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dcf02-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="dcf02-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dcf02-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="dcf02-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dcf02-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="dcf02-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dcf02-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dcf02-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dcf02-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="dcf02-118">Scenario description</span></span>
<span data-ttu-id="dcf02-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="dcf02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dcf02-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="dcf02-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dcf02-121">Aggiunta di Syncplicity dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="dcf02-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="dcf02-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcf02-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="dcf02-123">Aggiunta di Syncplicity dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="dcf02-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="dcf02-124">integrazione hello tooconfigure di Syncplicity in Azure AD, è necessario tooadd Syncplicity dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="dcf02-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dcf02-125">**tooadd Syncplicity dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dcf02-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcf02-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="dcf02-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dcf02-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dcf02-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="dcf02-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="dcf02-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="dcf02-133">Nella casella di ricerca hello, digitare **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-133">In hello search box, type **Syncplicity**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="dcf02-135">Nel riquadro dei risultati hello, selezionare **Syncplicity**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="dcf02-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dcf02-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcf02-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dcf02-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Syncplicity usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dcf02-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dcf02-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Syncplicity è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcf02-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="dcf02-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Syncplicity richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="dcf02-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="dcf02-141">In Syncplicity, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="dcf02-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dcf02-142">tooconfigure e test Azure single sign-on AD con Syncplicity, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="dcf02-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dcf02-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="dcf02-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dcf02-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dcf02-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dcf02-145">**[Creazione di un utente test Syncplicity](#creating-a-syncplicity-test-user)**  -toohave un equivalente di Britta Simon in Syncplicity che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dcf02-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dcf02-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dcf02-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dcf02-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="dcf02-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dcf02-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcf02-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dcf02-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="dcf02-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="dcf02-150">**Azure AD tooconfigure single sign-on con Syncplicity, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dcf02-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcf02-151">Nel portale di Azure su hello hello **Syncplicity** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="dcf02-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dcf02-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="dcf02-155">In hello **Syncplicity dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="dcf02-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="dcf02-157">a.</span><span class="sxs-lookup"><span data-stu-id="dcf02-157">a.</span></span> <span data-ttu-id="dcf02-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="dcf02-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="dcf02-159">b.</span><span class="sxs-lookup"><span data-stu-id="dcf02-159">b.</span></span> <span data-ttu-id="dcf02-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="dcf02-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dcf02-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="dcf02-161">These values are not real.</span></span> <span data-ttu-id="dcf02-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="dcf02-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dcf02-163">Contatto [team di supporto Client di Syncplicity](https://www.syncplicity.com/contact-us) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="dcf02-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="dcf02-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="dcf02-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="dcf02-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="dcf02-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dcf02-168">In hello **Syncplicity configurazione** fare clic su **configurare Syncplicity** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="dcf02-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dcf02-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="dcf02-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="dcf02-171">Accedi tooyour **Syncplicity** tenant.</span><span class="sxs-lookup"><span data-stu-id="dcf02-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="dcf02-172">Scegliere dal menu hello in primo piano hello **admin**selezionare **impostazioni**e quindi fare clic su **dominio personalizzato e accesso single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="dcf02-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="dcf02-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="dcf02-174">In hello **Single Sign-On (SSO)** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="dcf02-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="dcf02-175">![Accesso Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="dcf02-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="dcf02-176">a.</span><span class="sxs-lookup"><span data-stu-id="dcf02-176">a.</span></span> <span data-ttu-id="dcf02-177">In hello **dominio personalizzato** casella di testo, nome del tipo hello del dominio.</span><span class="sxs-lookup"><span data-stu-id="dcf02-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="dcf02-178">b.</span><span class="sxs-lookup"><span data-stu-id="dcf02-178">b.</span></span> <span data-ttu-id="dcf02-179">Selezionare **Enabled** (Abilitato) come **Single Sign-On Status** (Stato Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="dcf02-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="dcf02-180">c.</span><span class="sxs-lookup"><span data-stu-id="dcf02-180">c.</span></span> <span data-ttu-id="dcf02-181">In hello **Id entità** casella di testo, incollare hello valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf02-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dcf02-182">d.</span><span class="sxs-lookup"><span data-stu-id="dcf02-182">d.</span></span> <span data-ttu-id="dcf02-183">In hello **accesso URL della pagina** casella di testo, hello Incolla **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf02-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dcf02-184">e.</span><span class="sxs-lookup"><span data-stu-id="dcf02-184">e.</span></span> <span data-ttu-id="dcf02-185">In hello **Logout page URL** casella di testo, hello Incolla **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf02-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dcf02-186">f.</span><span class="sxs-lookup"><span data-stu-id="dcf02-186">f.</span></span> <span data-ttu-id="dcf02-187">In **Identity Provider Certificate**, fare clic su **Choose file**e quindi caricare il certificato scaricato dal portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="dcf02-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="dcf02-188">g.</span><span class="sxs-lookup"><span data-stu-id="dcf02-188">g.</span></span> <span data-ttu-id="dcf02-189">Fare clic su **SAVE CHANGES** (Salva modifiche).</span><span class="sxs-lookup"><span data-stu-id="dcf02-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="dcf02-190">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="dcf02-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dcf02-191">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="dcf02-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dcf02-192">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dcf02-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dcf02-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcf02-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="dcf02-194">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="dcf02-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="dcf02-196">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dcf02-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcf02-197">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="dcf02-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dcf02-199">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dcf02-201">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="dcf02-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dcf02-203">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="dcf02-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dcf02-205">a.</span><span class="sxs-lookup"><span data-stu-id="dcf02-205">a.</span></span> <span data-ttu-id="dcf02-206">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dcf02-207">b.</span><span class="sxs-lookup"><span data-stu-id="dcf02-207">b.</span></span> <span data-ttu-id="dcf02-208">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dcf02-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dcf02-209">c.</span><span class="sxs-lookup"><span data-stu-id="dcf02-209">c.</span></span> <span data-ttu-id="dcf02-210">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dcf02-211">d.</span><span class="sxs-lookup"><span data-stu-id="dcf02-211">d.</span></span> <span data-ttu-id="dcf02-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="dcf02-213">Creazione di un utente di test di Syncplicity</span><span class="sxs-lookup"><span data-stu-id="dcf02-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="dcf02-214">Per AAD utenti toobe in grado di toosign in devono essere sottoposte a provisioning tooSyncplicity applicazione.</span><span class="sxs-lookup"><span data-stu-id="dcf02-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="dcf02-215">In questa sezione viene descritto come degli account utente AAD toocreate in Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="dcf02-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="dcf02-216">**tooprovision tooSyncplicity un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dcf02-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcf02-217">Accedi tooyour **Syncplicity** tenant (ad esempio: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="dcf02-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="dcf02-218">Fare clic su **admin** (Amministrazione) e selezionare **user accounts** (Account utente).</span><span class="sxs-lookup"><span data-stu-id="dcf02-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="dcf02-219">Fare clic su **ADD A USER** (Aggiungi utente).</span><span class="sxs-lookup"><span data-stu-id="dcf02-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="dcf02-220">![Gestione utenti](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Gestione utenti")</span><span class="sxs-lookup"><span data-stu-id="dcf02-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="dcf02-221">Hello tipo **indirizzi di posta elettronica** di un account AAD, si vuole tooprovision, selezionare **utente** come **ruolo**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="dcf02-222">![Informazioni sull'account](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Informazioni sull'account")</span><span class="sxs-lookup"><span data-stu-id="dcf02-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="dcf02-223">titolare dell'account AAD Hello Ottiene inclusi tooconfirm un collegamento tramite posta elettronica e attivare l'account hello.</span><span class="sxs-lookup"><span data-stu-id="dcf02-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="dcf02-224">Selezionare un gruppo nell'azienda a cui aggiungere il nuovo utente e quindi fare clic su **NEXT** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="dcf02-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="dcf02-225">![Appartenenza al gruppo](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Appartenenza al gruppo")</span><span class="sxs-lookup"><span data-stu-id="dcf02-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="dcf02-226">Se non sono elencati gruppi, fare clic su **NEXT** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="dcf02-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="dcf02-227">Selezionare le cartelle di hello come tooplace nel controllo di Syncplicity nel computer dell'utente hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="dcf02-228">![Cartelle di Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Cartelle di Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="dcf02-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="dcf02-229">È possibile usare qualsiasi altro Syncplicity utente account strumento di creazione o le API fornite da Syncplicity tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="dcf02-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dcf02-230">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcf02-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dcf02-231">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSyncplicity.</span><span class="sxs-lookup"><span data-stu-id="dcf02-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![Assegna utente][200] 

<span data-ttu-id="dcf02-233">**tooassign Britta Simon tooSyncplicity, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dcf02-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcf02-234">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="dcf02-236">Nell'elenco di applicazioni hello, selezionare **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-236">In hello applications list, select **Syncplicity**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="dcf02-238">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="dcf02-240">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-240">Click **Add** button.</span></span> <span data-ttu-id="dcf02-241">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="dcf02-243">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="dcf02-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dcf02-244">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dcf02-245">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dcf02-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dcf02-246">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dcf02-246">Testing single sign-on</span></span>

<span data-ttu-id="dcf02-247">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="dcf02-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dcf02-248">Quando si fa clic su riquadro Syncplicity hello in hello Pannello di accesso, è necessario ottenere applicazione Syncplicity tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="dcf02-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="dcf02-249">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="dcf02-249">Additional resources</span></span>

* [<span data-ttu-id="dcf02-250">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dcf02-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dcf02-251">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dcf02-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

