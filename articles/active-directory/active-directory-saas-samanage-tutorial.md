---
title: 'Esercitazione: Integrazione di Azure Active Directory con Samanage | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Samanage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="f6022-103">Esercitazione: Integrazione di Azure Active Directory con Samanage</span><span class="sxs-lookup"><span data-stu-id="f6022-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="f6022-104">In questa esercitazione, è illustrato come toointegrate Samanage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6022-104">In this tutorial, you learn how toointegrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6022-105">Integrazione di Samanage con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f6022-105">Integrating Samanage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f6022-106">È possibile controllare in Azure AD che ha accesso tooSamanage</span><span class="sxs-lookup"><span data-stu-id="f6022-106">You can control in Azure AD who has access tooSamanage</span></span>
- <span data-ttu-id="f6022-107">È possibile abilitare l'utenti tooautomatically get connesso tooSamanage (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6022-107">You can enable your users tooautomatically get signed-on tooSamanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6022-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f6022-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f6022-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6022-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6022-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f6022-110">Prerequisites</span></span>

<span data-ttu-id="f6022-111">integrazione di Azure AD con Samanage tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f6022-111">tooconfigure Azure AD integration with Samanage, you need hello following items:</span></span>

- <span data-ttu-id="f6022-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6022-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6022-113">Sottoscrizione di Samanage abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f6022-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6022-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f6022-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6022-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f6022-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6022-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f6022-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f6022-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6022-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6022-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f6022-118">Scenario description</span></span>
<span data-ttu-id="f6022-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f6022-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6022-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f6022-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6022-121">Aggiunta di Samanage dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f6022-121">Adding Samanage from hello gallery</span></span>
2. <span data-ttu-id="f6022-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6022-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-hello-gallery"></a><span data-ttu-id="f6022-123">Aggiunta di Samanage dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f6022-123">Adding Samanage from hello gallery</span></span>
<span data-ttu-id="f6022-124">integrazione hello tooconfigure di Samanage in Azure AD, è necessario tooadd Samanage dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f6022-124">tooconfigure hello integration of Samanage into Azure AD, you need tooadd Samanage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f6022-125">**tooadd Samanage dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f6022-125">**tooadd Samanage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6022-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f6022-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6022-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f6022-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f6022-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f6022-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f6022-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f6022-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f6022-133">Nella casella di ricerca hello, digitare **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="f6022-133">In hello search box, type **Samanage**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="f6022-135">Nel riquadro dei risultati hello, selezionare **Samanage**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f6022-135">In hello results panel, select **Samanage**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6022-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6022-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6022-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Samanage in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f6022-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6022-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Samanage è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6022-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Samanage is tooa user in Azure AD.</span></span> <span data-ttu-id="f6022-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Samanage deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f6022-140">In other words, a link relationship between an Azure AD user and hello related user in Samanage needs toobe established.</span></span>

<span data-ttu-id="f6022-141">In Samanage, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="f6022-141">In Samanage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f6022-142">tooconfigure e test Azure single sign-on AD con Samanage, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f6022-142">tooconfigure and test Azure AD single sign-on with Samanage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f6022-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f6022-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f6022-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6022-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6022-145">**[Creazione di un utente test Samanage](#creating-a-samanage-test-user)**  -toohave un equivalente di Britta Simon in Samanage che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f6022-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - toohave a counterpart of Britta Simon in Samanage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f6022-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f6022-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6022-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f6022-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6022-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6022-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6022-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Samanage.</span><span class="sxs-lookup"><span data-stu-id="f6022-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="f6022-150">**Azure AD tooconfigure single sign-on con Samanage, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f6022-150">**tooconfigure Azure AD single sign-on with Samanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6022-151">Nel portale di Azure su hello hello **Samanage** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f6022-151">In hello Azure portal, on hello **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f6022-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f6022-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="f6022-155">In hello **Samanage dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f6022-155">On hello **Samanage Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="f6022-157">a.</span><span class="sxs-lookup"><span data-stu-id="f6022-157">a.</span></span> <span data-ttu-id="f6022-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="f6022-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="f6022-159">b.</span><span class="sxs-lookup"><span data-stu-id="f6022-159">b.</span></span> <span data-ttu-id="f6022-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="f6022-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f6022-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="f6022-161">These values are not real.</span></span> <span data-ttu-id="f6022-162">Aggiornare questi valori con URL hello effettivo Sign-on e l'identificatore, illustrato più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="f6022-162">Update these values with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> <span data-ttu-id="f6022-163">Per altri dettagli, contattare il [team di supporto clienti di Samanage](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="f6022-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="f6022-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f6022-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="f6022-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f6022-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f6022-168">In hello **Samanage configurazione** fare clic su **configurare Samanage** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="f6022-168">On hello **Samanage Configuration** section, click **Configure Samanage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f6022-169">Hello copia **Sign-Out URL e l'ID entità SAML** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f6022-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="f6022-171">In un'altra finestra del Web browser accedere al sito aziendale di Samanage come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f6022-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="f6022-172">Fare clic su **Dashboard** e selezionare **Setup** (Configurazione) nel riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f6022-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="f6022-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="f6022-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="f6022-174">Fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f6022-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="f6022-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f6022-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="f6022-176">Passare troppo**accesso tramite SAML** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f6022-176">Navigate too**Login using SAML** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f6022-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span><span class="sxs-lookup"><span data-stu-id="f6022-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="f6022-178">a.</span><span class="sxs-lookup"><span data-stu-id="f6022-178">a.</span></span> <span data-ttu-id="f6022-179">Fare clic su **Enable Single Sign-On with SAML**(Abilita Single Sign-On con SAML).</span><span class="sxs-lookup"><span data-stu-id="f6022-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="f6022-180">b.</span><span class="sxs-lookup"><span data-stu-id="f6022-180">b.</span></span> <span data-ttu-id="f6022-181">In hello **Identity Provider URL** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6022-181">In hello **Identity Provider URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="f6022-182">c.</span><span class="sxs-lookup"><span data-stu-id="f6022-182">c.</span></span> <span data-ttu-id="f6022-183">Conferma hello **URL di accesso** corrispondenze hello **URL di accesso** di **Samanage dominio e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6022-183">Confirm hello **Login URL** matches hello **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="f6022-184">d.</span><span class="sxs-lookup"><span data-stu-id="f6022-184">d.</span></span> <span data-ttu-id="f6022-185">In hello **Logout URL** casella di testo, immettere il valore di hello di **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6022-185">In hello **Logout URL** textbox, enter hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="f6022-186">e.</span><span class="sxs-lookup"><span data-stu-id="f6022-186">e.</span></span> <span data-ttu-id="f6022-187">In hello **autorità di certificazione SAML** textbox, URI dell'id app hello tipo impostato nel provider di identità.</span><span class="sxs-lookup"><span data-stu-id="f6022-187">In hello **SAML Issuer** textbox, type hello app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="f6022-188">f.</span><span class="sxs-lookup"><span data-stu-id="f6022-188">f.</span></span> <span data-ttu-id="f6022-189">Aprire il certificato con codifica base 64 scaricato dal portale di Azure nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **incollare la x. 509 del Provider di identità certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f6022-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="f6022-190">g.</span><span class="sxs-lookup"><span data-stu-id="f6022-190">g.</span></span> <span data-ttu-id="f6022-191">Fare clic su **Create users if they do not exist in Samanage**(Crea utenti se non presenti in Samanage).</span><span class="sxs-lookup"><span data-stu-id="f6022-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="f6022-192">h.</span><span class="sxs-lookup"><span data-stu-id="f6022-192">h.</span></span> <span data-ttu-id="f6022-193">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="f6022-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="f6022-194">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="f6022-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f6022-195">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="f6022-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f6022-196">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f6022-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6022-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6022-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6022-198">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f6022-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f6022-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f6022-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6022-201">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f6022-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6022-203">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f6022-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6022-205">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f6022-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6022-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f6022-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6022-209">a.</span><span class="sxs-lookup"><span data-stu-id="f6022-209">a.</span></span> <span data-ttu-id="f6022-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6022-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6022-211">b.</span><span class="sxs-lookup"><span data-stu-id="f6022-211">b.</span></span> <span data-ttu-id="f6022-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f6022-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6022-213">c.</span><span class="sxs-lookup"><span data-stu-id="f6022-213">c.</span></span> <span data-ttu-id="f6022-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="f6022-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f6022-215">d.</span><span class="sxs-lookup"><span data-stu-id="f6022-215">d.</span></span> <span data-ttu-id="f6022-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f6022-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="f6022-217">Creazione di un utente test per Samanage</span><span class="sxs-lookup"><span data-stu-id="f6022-217">Creating a Samanage test user</span></span>

<span data-ttu-id="f6022-218">toolog agli utenti di Azure AD tooenable in tooSamanage, è necessario eseguirne il provisioning in Samanage.</span><span class="sxs-lookup"><span data-stu-id="f6022-218">tooenable Azure AD users toolog in tooSamanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="f6022-219">Nel caso di hello di Samanage, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f6022-219">In hello case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="f6022-220">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f6022-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6022-221">Accedere al sito aziendale di Samanage come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f6022-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="f6022-222">Fare clic su **Dashboard** e selezionare **Setup** (Configurazione) nel riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f6022-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="f6022-223">![Installazione](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="f6022-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="f6022-224">Fare clic su hello **utenti** scheda</span><span class="sxs-lookup"><span data-stu-id="f6022-224">Click hello **Users** tab</span></span>
   
    <span data-ttu-id="f6022-225">![Utenti](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="f6022-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="f6022-226">Fare clic su **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="f6022-226">Click **New User**.</span></span>
   
    <span data-ttu-id="f6022-227">![Nuovo utente](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="f6022-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="f6022-228">Hello tipo **nome** hello e **indirizzo di posta elettronica** di un account di Azure Active Directory tooprovision desiderato e fare clic su **Create user**.</span><span class="sxs-lookup"><span data-stu-id="f6022-228">Type hello **Name** and hello **Email Address** of an Azure Active Directory account you want tooprovision and click **Create user**.</span></span>
   
    <span data-ttu-id="f6022-229">![Crea utente](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="f6022-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f6022-230">titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="f6022-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="f6022-231">È possibile usare qualsiasi altro Samanage strumento account utente la creazione o qualsiasi API fornita da Samanage tooprovision Azure Active Directory gli account utente.</span><span class="sxs-lookup"><span data-stu-id="f6022-231">You can use any other Samanage user account creation tools or APIs provided by Samanage tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f6022-232">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6022-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f6022-233">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="f6022-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSamanage.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f6022-235">**tooassign Britta Simon tooSamanage, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f6022-235">**tooassign Britta Simon tooSamanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6022-236">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f6022-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f6022-238">Nell'elenco di applicazioni hello, selezionare **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="f6022-238">In hello applications list, select **Samanage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="f6022-240">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f6022-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f6022-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f6022-242">Click **Add** button.</span></span> <span data-ttu-id="f6022-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f6022-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f6022-245">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f6022-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f6022-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f6022-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6022-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f6022-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f6022-248">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f6022-248">Testing single sign-on</span></span>

<span data-ttu-id="f6022-249">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f6022-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f6022-250">Quando si fa clic su riquadro Samanage hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Samanage applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6022-250">When you click hello Samanage tile in hello Access Panel, you should get automatically signed-on tooyour Samanage application.</span></span>
<span data-ttu-id="f6022-251">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f6022-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6022-252">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f6022-252">Additional resources</span></span>

* [<span data-ttu-id="f6022-253">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6022-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6022-254">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6022-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

