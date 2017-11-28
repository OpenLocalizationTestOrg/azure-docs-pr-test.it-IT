---
title: 'Esercitazione: Integrazione di Azure Active Directory con Gigya | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Gigya.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="dd6a7-103">Esercitazione: Integrazione di Azure Active Directory con Gigya</span><span class="sxs-lookup"><span data-stu-id="dd6a7-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="dd6a7-104">In questa esercitazione, è illustrato come toointegrate Gigya con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd6a7-104">In this tutorial, you learn how toointegrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd6a7-105">Integrazione di Gigya con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="dd6a7-105">Integrating Gigya with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dd6a7-106">È possibile controllare in Azure AD che ha accesso tooGigya</span><span class="sxs-lookup"><span data-stu-id="dd6a7-106">You can control in Azure AD who has access tooGigya</span></span>
- <span data-ttu-id="dd6a7-107">È possibile abilitare l'utenti tooautomatically get connesso tooGigya (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6a7-107">You can enable your users tooautomatically get signed-on tooGigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd6a7-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dd6a7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dd6a7-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd6a7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd6a7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dd6a7-110">Prerequisites</span></span>

<span data-ttu-id="dd6a7-111">integrazione di Azure AD con Gigya tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="dd6a7-111">tooconfigure Azure AD integration with Gigya, you need hello following items:</span></span>

- <span data-ttu-id="dd6a7-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd6a7-113">Sottoscrizione di Gigya abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dd6a7-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd6a7-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd6a7-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="dd6a7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd6a7-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd6a7-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd6a7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd6a7-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="dd6a7-118">Scenario description</span></span>
<span data-ttu-id="dd6a7-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd6a7-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="dd6a7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd6a7-121">Aggiunta di Gigya dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="dd6a7-121">Adding Gigya from hello gallery</span></span>
2. <span data-ttu-id="dd6a7-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6a7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-hello-gallery"></a><span data-ttu-id="dd6a7-123">Aggiunta di Gigya dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="dd6a7-123">Adding Gigya from hello gallery</span></span>
<span data-ttu-id="dd6a7-124">integrazione hello tooconfigure di Gigya in Azure AD, è necessario tooadd Gigya dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-124">tooconfigure hello integration of Gigya into Azure AD, you need tooadd Gigya from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dd6a7-125">**tooadd Gigya dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dd6a7-125">**tooadd Gigya from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd6a7-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd6a7-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dd6a7-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="dd6a7-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="dd6a7-133">Nella casella di ricerca hello, digitare **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-133">In hello search box, type **Gigya**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="dd6a7-135">Nel riquadro dei risultati hello, selezionare **Gigya**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-135">In hello results panel, select **Gigya**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd6a7-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6a7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd6a7-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Gigya mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dd6a7-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dd6a7-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Gigya è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Gigya is tooa user in Azure AD.</span></span> <span data-ttu-id="dd6a7-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Gigya deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-140">In other words, a link relationship between an Azure AD user and hello related user in Gigya needs toobe established.</span></span>

<span data-ttu-id="dd6a7-141">In Gigya, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-141">In Gigya, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dd6a7-142">tooconfigure e prova AD Azure single sign-on con Gigya, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="dd6a7-142">tooconfigure and test Azure AD single sign-on with Gigya, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dd6a7-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dd6a7-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd6a7-145">**[Creazione di un utente test Gigya](#creating-a-gigya-test-user)**  -toohave un equivalente di Britta Simon in Gigya che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - toohave a counterpart of Britta Simon in Gigya that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd6a7-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd6a7-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd6a7-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6a7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd6a7-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Gigya.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="dd6a7-150">**Azure AD tooconfigure single sign-on con Gigya, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dd6a7-150">**tooconfigure Azure AD single sign-on with Gigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd6a7-151">Nel portale di Azure su hello hello **Gigya** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-151">In hello Azure portal, on hello **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="dd6a7-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="dd6a7-155">In hello **Gigya dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="dd6a7-155">On hello **Gigya Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="dd6a7-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-157">a.</span></span> <span data-ttu-id="dd6a7-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="dd6a7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="dd6a7-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-159">b.</span></span> <span data-ttu-id="dd6a7-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="dd6a7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd6a7-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="dd6a7-161">These values are not real.</span></span> <span data-ttu-id="dd6a7-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dd6a7-163">Contatto [team di supporto Client di Gigya](https://www.gigya.com/support-policy/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) tooget these values.</span></span> 
 
4. <span data-ttu-id="dd6a7-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="dd6a7-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="dd6a7-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd6a7-168">In hello **Gigya configurazione** fare clic su **configurare Gigya** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-168">On hello **Gigya Configuration** section, click **Configure Gigya** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dd6a7-169">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="dd6a7-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="dd6a7-171">In un'altra finestra del Web browser accedere al sito aziendale di Sign On come amministratore.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="dd6a7-172">Andare troppo**impostazioni \> SAML Login**, quindi fare clic su hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-172">Go too**Settings \> SAML Login**, and then click hello **Add** button.</span></span>
   
    <span data-ttu-id="dd6a7-173">![Login SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "Login SAML")</span><span class="sxs-lookup"><span data-stu-id="dd6a7-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="dd6a7-174">In hello **SAML Login** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="dd6a7-174">In hello **SAML Login** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd6a7-175">![Configurazione SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="dd6a7-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="dd6a7-176">a.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-176">a.</span></span> <span data-ttu-id="dd6a7-177">In hello **nome** casella di testo, digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-177">In hello **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="dd6a7-178">b.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-178">b.</span></span> <span data-ttu-id="dd6a7-179">In **dell'autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-179">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="dd6a7-180">c.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-180">c.</span></span> <span data-ttu-id="dd6a7-181">In **URL servizio Single Sign-On** casella di testo, hello Incolla valore **URL servizio Single Sign-On** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-181">In **Single Sign-On Service URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="dd6a7-182">d.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-182">d.</span></span> <span data-ttu-id="dd6a7-183">In **formato ID nome** casella di testo, hello Incolla valore **Name Identifier Format** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-183">In **Name ID Format** textbox, paste hello value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="dd6a7-184">e.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-184">e.</span></span> <span data-ttu-id="dd6a7-185">Aprire il certificato con codifica base 64 nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="dd6a7-186">f.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-186">f.</span></span> <span data-ttu-id="dd6a7-187">Fare clic su **Salva impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="dd6a7-188">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="dd6a7-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dd6a7-189">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dd6a7-190">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd6a7-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd6a7-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6a7-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="dd6a7-192">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="dd6a7-194">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dd6a7-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd6a7-195">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd6a7-197">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd6a7-199">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd6a7-201">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="dd6a7-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd6a7-203">a.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-203">a.</span></span> <span data-ttu-id="dd6a7-204">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd6a7-205">b.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-205">b.</span></span> <span data-ttu-id="dd6a7-206">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd6a7-207">c.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-207">c.</span></span> <span data-ttu-id="dd6a7-208">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dd6a7-209">d.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-209">d.</span></span> <span data-ttu-id="dd6a7-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="dd6a7-211">Creazione di un utente test di Gigya</span><span class="sxs-lookup"><span data-stu-id="dd6a7-211">Creating a Gigya test user</span></span>

<span data-ttu-id="dd6a7-212">In ordine tooenable Azure AD utenti toolog a Gigya, è necessario eseguirne il provisioning in Gigya.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-212">In order tooenable Azure AD users toolog into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="dd6a7-213">Nel caso di hello di Gigya, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-213">In hello case of Gigya, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="dd6a7-214">eseguire un account utente, tooprovision hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd6a7-214">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="dd6a7-215">Accedi tooyour **Gigya** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-215">Log in tooyour **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="dd6a7-216">Andare troppo**Admin \> Gestisci utenti**, quindi fare clic su **invitare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-216">Go too**Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="dd6a7-217">![Gestione utenti](./media/active-directory-saas-gigya-tutorial/ic789535.png "Gestione utenti")</span><span class="sxs-lookup"><span data-stu-id="dd6a7-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="dd6a7-218">Nella finestra di dialogo Invite Users hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="dd6a7-218">On hello Invite Users dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd6a7-219">![Invitare utenti](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invitare utenti")</span><span class="sxs-lookup"><span data-stu-id="dd6a7-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="dd6a7-220">a.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-220">a.</span></span> <span data-ttu-id="dd6a7-221">In hello **posta elettronica** casella di testo, alias del tipo di messaggio di posta elettronica hello di un account Azure Active Directory valido, si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-221">In hello **Email** textbox, type hello email alias of a valid Azure Active Directory account you want tooprovision.</span></span>
    
    <span data-ttu-id="dd6a7-222">b.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-222">b.</span></span> <span data-ttu-id="dd6a7-223">Fare clic su **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="dd6a7-224">titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica che include un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-224">hello Azure Active Directory account holder will receive an email that includes a link tooconfirm hello account before it becomes active.</span></span>
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dd6a7-225">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6a7-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dd6a7-226">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooGigya.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGigya.</span></span>

![Assegna utente][200] 

<span data-ttu-id="dd6a7-228">**tooassign Britta Simon tooGigya, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dd6a7-228">**tooassign Britta Simon tooGigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd6a7-229">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="dd6a7-231">Nell'elenco di applicazioni hello, selezionare **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-231">In hello applications list, select **Gigya**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="dd6a7-233">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="dd6a7-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-235">Click **Add** button.</span></span> <span data-ttu-id="dd6a7-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="dd6a7-238">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dd6a7-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd6a7-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd6a7-241">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dd6a7-241">Testing single sign-on</span></span>

<span data-ttu-id="dd6a7-242">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="dd6a7-243">Quando si fa clic su riquadro Gigya hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Gigya applicazione.</span><span class="sxs-lookup"><span data-stu-id="dd6a7-243">When you click hello Gigya tile in hello Access Panel, you should get automatically signed-on tooyour Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd6a7-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="dd6a7-244">Additional resources</span></span>

* [<span data-ttu-id="dd6a7-245">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd6a7-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd6a7-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd6a7-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

