---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kintone | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Kintone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="1dbbf-103">Esercitazione: Integrazione di Azure Active Directory con Kintone</span><span class="sxs-lookup"><span data-stu-id="1dbbf-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="1dbbf-104">In questa esercitazione, è illustrato come toointegrate Kintone con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1dbbf-104">In this tutorial, you learn how toointegrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1dbbf-105">Integrazione di Kintone con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-105">Integrating Kintone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1dbbf-106">È possibile controllare in Azure AD che ha accesso tooKintone</span><span class="sxs-lookup"><span data-stu-id="1dbbf-106">You can control in Azure AD who has access tooKintone</span></span>
- <span data-ttu-id="1dbbf-107">È possibile abilitare l'utenti tooautomatically get connesso tooKintone (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dbbf-107">You can enable your users tooautomatically get signed-on tooKintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1dbbf-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1dbbf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1dbbf-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1dbbf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dbbf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1dbbf-110">Prerequisites</span></span>

<span data-ttu-id="1dbbf-111">integrazione di Azure AD con Kintone tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-111">tooconfigure Azure AD integration with Kintone, you need hello following items:</span></span>

- <span data-ttu-id="1dbbf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1dbbf-113">Sottoscrizione di Kintone abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1dbbf-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1dbbf-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1dbbf-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1dbbf-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1dbbf-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1dbbf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1dbbf-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1dbbf-118">Scenario description</span></span>
<span data-ttu-id="1dbbf-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1dbbf-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1dbbf-121">Aggiunta di Kintone dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1dbbf-121">Adding Kintone from hello gallery</span></span>
2. <span data-ttu-id="1dbbf-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dbbf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-hello-gallery"></a><span data-ttu-id="1dbbf-123">Aggiunta di Kintone dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1dbbf-123">Adding Kintone from hello gallery</span></span>
<span data-ttu-id="1dbbf-124">integrazione hello tooconfigure di Kintone in Azure AD, è necessario tooadd Kintone dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-124">tooconfigure hello integration of Kintone into Azure AD, you need tooadd Kintone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1dbbf-125">**tooadd Kintone dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1dbbf-125">**tooadd Kintone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dbbf-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1dbbf-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1dbbf-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1dbbf-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1dbbf-133">Nella casella di ricerca hello, digitare **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-133">In hello search box, type **Kintone**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="1dbbf-135">Nel riquadro dei risultati hello, selezionare **Kintone**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-135">In hello results panel, select **Kintone**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1dbbf-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dbbf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1dbbf-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kintone mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1dbbf-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1dbbf-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Kintone è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kintone is tooa user in Azure AD.</span></span> <span data-ttu-id="1dbbf-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Kintone deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-140">In other words, a link relationship between an Azure AD user and hello related user in Kintone needs toobe established.</span></span>

<span data-ttu-id="1dbbf-141">In Kintone, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-141">In Kintone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1dbbf-142">tooconfigure e prova AD Azure single sign-on con Kintone, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-142">tooconfigure and test Azure AD single sign-on with Kintone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1dbbf-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1dbbf-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1dbbf-145">**[Creazione di un utente test Kintone](#creating-a-kintone-test-user)**  -toohave un equivalente di Britta Simon in Kintone che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - toohave a counterpart of Britta Simon in Kintone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1dbbf-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1dbbf-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1dbbf-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dbbf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1dbbf-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Kintone.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="1dbbf-150">**Azure AD tooconfigure single sign-on con Kintone, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1dbbf-150">**tooconfigure Azure AD single sign-on with Kintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dbbf-151">Nel portale di Azure su hello hello **Kintone** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-151">In hello Azure portal, on hello **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1dbbf-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="1dbbf-155">In hello **Kintone dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-155">On hello **Kintone Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="1dbbf-157">a.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-157">a.</span></span> <span data-ttu-id="1dbbf-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="1dbbf-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="1dbbf-159">b.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-159">b.</span></span> <span data-ttu-id="1dbbf-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="1dbbf-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="1dbbf-161">These values are not real.</span></span> <span data-ttu-id="1dbbf-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1dbbf-163">Contatto [team di supporto Client di Kintone](https://www.kintone.com/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="1dbbf-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="1dbbf-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1dbbf-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1dbbf-168">In hello **Kintone configurazione** fare clic su **configurare Kintone** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-168">On hello **Kintone Configuration** section, click **Configure Kintone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1dbbf-169">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1dbbf-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="1dbbf-171">In un'altra finestra del Web browser accedere al sito aziendale di **Kintone** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="1dbbf-172">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="1dbbf-173">![Impostazioni](./media/active-directory-saas-kintone-tutorial/ic785879.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="1dbbf-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="1dbbf-174">Fare clic su **Amministrazione utenti e di sistema**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="1dbbf-175">![Amministrazione utenti e di sistema](./media/active-directory-saas-kintone-tutorial/ic785880.png "Amministrazione utenti e di sistema")</span><span class="sxs-lookup"><span data-stu-id="1dbbf-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="1dbbf-176">In **Amministrazione di sistema \> Sicurezza** fare clic su **Accesso**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="1dbbf-177">![Account di accesso](./media/active-directory-saas-kintone-tutorial/ic785881.png "Account di accesso")</span><span class="sxs-lookup"><span data-stu-id="1dbbf-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="1dbbf-178">Fare clic su **Abilita autenticazione SAML**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="1dbbf-179">![Autenticazione SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="1dbbf-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="1dbbf-180">Nella sezione autenticazione SAML hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-180">In hello SAML Authentication section, perform hello following steps:</span></span>
    
    <span data-ttu-id="1dbbf-181">![Autenticazione SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="1dbbf-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="1dbbf-182">a.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-182">a.</span></span> <span data-ttu-id="1dbbf-183">In hello **URL di accesso** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-183">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="1dbbf-184">b.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-184">b.</span></span> <span data-ttu-id="1dbbf-185">In hello **Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1dbbf-186">c.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-186">c.</span></span> <span data-ttu-id="1dbbf-187">Fare clic su **Sfoglia** tooupload il certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-187">Click **Browse** tooupload your downloaded certificate.</span></span>
    
    <span data-ttu-id="1dbbf-188">d.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-188">d.</span></span> <span data-ttu-id="1dbbf-189">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1dbbf-190">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1dbbf-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1dbbf-191">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1dbbf-192">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1dbbf-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1dbbf-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dbbf-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="1dbbf-194">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1dbbf-196">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1dbbf-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dbbf-197">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1dbbf-199">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1dbbf-201">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1dbbf-203">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1dbbf-205">a.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-205">a.</span></span> <span data-ttu-id="1dbbf-206">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1dbbf-207">b.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-207">b.</span></span> <span data-ttu-id="1dbbf-208">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1dbbf-209">c.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-209">c.</span></span> <span data-ttu-id="1dbbf-210">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1dbbf-211">d.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-211">d.</span></span> <span data-ttu-id="1dbbf-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="1dbbf-213">Creazione di un utente test di Kintone</span><span class="sxs-lookup"><span data-stu-id="1dbbf-213">Creating a Kintone test user</span></span>

<span data-ttu-id="1dbbf-214">toolog agli utenti di Azure AD tooenable in tooKintone, è necessario eseguirne il provisioning in Kintone.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-214">tooenable Azure AD users toolog in tooKintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="1dbbf-215">Nel caso di hello di Kintone, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-215">In hello case of Kintone, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="1dbbf-216">tooprovision un account utente, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-216">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="1dbbf-217">Accedi tooyour **Kintone** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-217">Log in tooyour **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="1dbbf-218">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="1dbbf-219">![Impostazioni](./media/active-directory-saas-kintone-tutorial/ic785879.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="1dbbf-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="1dbbf-220">Fare clic su **Amministrazione utenti e di sistema**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="1dbbf-221">![Amministrazione utenti e di sistema](./media/active-directory-saas-kintone-tutorial/ic785880.png "Amministrazione utenti e di sistema")</span><span class="sxs-lookup"><span data-stu-id="1dbbf-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="1dbbf-222">In **Amministrazione Utente** fare clic su **Reparti e Utenti**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="1dbbf-223">![Reparto e utenti](./media/active-directory-saas-kintone-tutorial/ic785888.png "Reparto e utenti")</span><span class="sxs-lookup"><span data-stu-id="1dbbf-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="1dbbf-224">Fare clic su **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-224">Click **New User**.</span></span>
   
    <span data-ttu-id="1dbbf-225">![Nuovi utenti](./media/active-directory-saas-kintone-tutorial/ic785889.png "Nuovi utenti")</span><span class="sxs-lookup"><span data-stu-id="1dbbf-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="1dbbf-226">In hello **nuovo utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1dbbf-226">In hello **New User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1dbbf-227">![Nuovi utenti](./media/active-directory-saas-kintone-tutorial/ic785890.png "Nuovi utenti")</span><span class="sxs-lookup"><span data-stu-id="1dbbf-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="1dbbf-228">a.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-228">a.</span></span> <span data-ttu-id="1dbbf-229">Digitare un **nome visualizzato**, **nome account di accesso**, **nuova Password**, **Conferma Password**, **indirizzo di posta elettronica**, e altri dettagli di un account aAd di cui che si desidera tooprovision in hello correlati nelle caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
 
    <span data-ttu-id="1dbbf-230">b.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-230">b.</span></span> <span data-ttu-id="1dbbf-231">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="1dbbf-232">È possibile usare qualsiasi altro Kintone utente account strumento di creazione o le API fornite da Kintone tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-232">You can use any other Kintone user account creation tools or APIs provided by Kintone tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1dbbf-233">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dbbf-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1dbbf-234">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooKintone.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKintone.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1dbbf-236">**tooassign Britta Simon tooKintone, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1dbbf-236">**tooassign Britta Simon tooKintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dbbf-237">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1dbbf-239">Nell'elenco di applicazioni hello, selezionare **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-239">In hello applications list, select **Kintone**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="1dbbf-241">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1dbbf-243">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-243">Click **Add** button.</span></span> <span data-ttu-id="1dbbf-244">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1dbbf-246">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1dbbf-247">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1dbbf-248">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1dbbf-249">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1dbbf-249">Testing single sign-on</span></span>

<span data-ttu-id="1dbbf-250">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-250">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1dbbf-251">Quando si fa clic su riquadro Kintone hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Kintone applicazione.</span><span class="sxs-lookup"><span data-stu-id="1dbbf-251">When you click hello Kintone tile in hello Access Panel, you should get automatically signed-on tooyour Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1dbbf-252">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1dbbf-252">Additional resources</span></span>

* [<span data-ttu-id="1dbbf-253">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1dbbf-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1dbbf-254">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1dbbf-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

