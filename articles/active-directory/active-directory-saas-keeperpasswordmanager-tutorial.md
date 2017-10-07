---
title: 'Esercitazione: Integrazione di Azure Active Directory con Keeper Password Manager & Digital Vault | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e gestione di Password detentore & digitali insieme di credenziali.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 01e59004e6bdccfca08094f9da6f82270d5028d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="b1bda-103">Esercitazione: Integrazione di Azure Active Directory con Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="b1bda-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="b1bda-104">In questa esercitazione, è illustrato come toointegrate gestione Password detentore & digitali insieme di credenziali con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1bda-104">In this tutorial, you learn how toointegrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1bda-105">Integrazione di gestione di Password detentore & digitali insieme di credenziali con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b1bda-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b1bda-106">È possibile controllare in Azure AD che ha accesso tooKeeper gestione Password & digitali insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="b1bda-106">You can control in Azure AD who has access tooKeeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="b1bda-107">È possibile abilitare le utenti tooautomatically get connesso tooKeeper gestione Password & digitali insieme di credenziali (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bda-107">You can enable your users tooautomatically get signed-on tooKeeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1bda-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b1bda-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b1bda-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1bda-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1bda-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b1bda-110">Prerequisites</span></span>

<span data-ttu-id="b1bda-111">tooconfigure integrazione di Azure AD con gestione Password detentore & digitali insieme di credenziali, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b1bda-111">tooconfigure Azure AD integration with Keeper Password Manager & Digital Vault, you need hello following items:</span></span>

- <span data-ttu-id="b1bda-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1bda-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1bda-113">Sottoscrizione di Keeper Password Manager & Digital Vault abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b1bda-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1bda-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b1bda-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1bda-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="b1bda-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1bda-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b1bda-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1bda-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1bda-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1bda-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b1bda-118">Scenario description</span></span>
<span data-ttu-id="b1bda-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b1bda-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1bda-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="b1bda-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1bda-121">Aggiunta di gestione di Password detentore & digitali insieme di credenziali dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b1bda-121">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
2. <span data-ttu-id="b1bda-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bda-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-hello-gallery"></a><span data-ttu-id="b1bda-123">Aggiunta di gestione di Password detentore & digitali insieme di credenziali dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b1bda-123">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
<span data-ttu-id="b1bda-124">integrazione hello tooconfigure di gestione di Password detentore & digitali insieme di credenziali in Azure AD, è necessario tooadd gestione Password detentore & digitali insieme di credenziali dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b1bda-124">tooconfigure hello integration of Keeper Password Manager & Digital Vault into Azure AD, you need tooadd Keeper Password Manager & Digital Vault from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b1bda-125">**Gestione di Password detentore tooadd & digitali insieme di credenziali dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b1bda-125">**tooadd Keeper Password Manager & Digital Vault from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1bda-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b1bda-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b1bda-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b1bda-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b1bda-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b1bda-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b1bda-133">Nella casella di ricerca hello, digitare **gestione Password detentore & digitali insieme di credenziali**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-133">In hello search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="b1bda-135">Nel riquadro dei risultati hello, selezionare **gestione Password detentore & digitali insieme di credenziali**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b1bda-135">In hello results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b1bda-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bda-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b1bda-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Keeper Password Manager & Digital Vault mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b1bda-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b1bda-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Gestione Password detentore & digitali insieme di credenziali è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1bda-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Keeper Password Manager & Digital Vault is tooa user in Azure AD.</span></span> <span data-ttu-id="b1bda-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Gestione Password detentore & digitali insieme di credenziali deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="b1bda-140">In other words, a link relationship between an Azure AD user and hello related user in Keeper Password Manager & Digital Vault needs toobe established.</span></span>

<span data-ttu-id="b1bda-141">In Gestione Password detentore & digitali insieme di credenziali, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="b1bda-141">In Keeper Password Manager & Digital Vault, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b1bda-142">tooconfigure e prova AD Azure single sign-on con gestione Password detentore & digitali insieme di credenziali, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="b1bda-142">tooconfigure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b1bda-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b1bda-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b1bda-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1bda-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1bda-145">**[Creazione di un utente di test di gestione di Password detentore & digitali insieme di credenziali](#creating-a-keeperpasswordmanager-test-user)**  -toohave un equivalente di Britta Simon nella gestione di Password detentore & digitali insieme di credenziali di rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b1bda-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - toohave a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1bda-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b1bda-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1bda-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="b1bda-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b1bda-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bda-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b1bda-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Gestione Password detentore & digitali insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b1bda-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="b1bda-150">**tooconfigure AD Azure single sign-on con gestione Password detentore & digitali insieme di credenziali, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b1bda-150">**tooconfigure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1bda-151">Nel portale di Azure su hello hello **gestione Password detentore & digitali insieme di credenziali** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-151">In hello Azure portal, on hello **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b1bda-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b1bda-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="b1bda-155">In hello **gestione Password detentore & digitali insieme di credenziali di dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b1bda-155">On hello **Keeper Password Manager & Digital Vault Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="b1bda-157">a.</span><span class="sxs-lookup"><span data-stu-id="b1bda-157">a.</span></span> <span data-ttu-id="b1bda-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="b1bda-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="b1bda-159">b.</span><span class="sxs-lookup"><span data-stu-id="b1bda-159">b.</span></span> <span data-ttu-id="b1bda-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="b1bda-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="b1bda-161">c.</span><span class="sxs-lookup"><span data-stu-id="b1bda-161">c.</span></span> <span data-ttu-id="b1bda-162">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="b1bda-162">In hello **Identifier** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b1bda-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b1bda-163">These values are not real.</span></span> <span data-ttu-id="b1bda-164">Aggiornare questi valori con l'URL di risposta effettivo hello e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b1bda-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b1bda-165">Contatto [team di supporto di gestione di Password detentore & digitali insieme di credenziali Client](https://keepersecurity.com/contact.html) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="b1bda-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="b1bda-166">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b1bda-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="b1bda-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b1bda-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b1bda-170">In hello **gestione Password detentore & digitali Configurazione archivi** fare clic su **configurare Gestione Password detentore & digitali insieme di credenziali** tooopen **configurasign-on**finestra.</span><span class="sxs-lookup"><span data-stu-id="b1bda-170">On hello **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b1bda-171">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b1bda-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="b1bda-173">tooconfigure single sign-on sul **gestione Password detentore & digitali Configurazione archivi** sul lato, attenersi alle linee guida hello assegnate al [detentore Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="b1bda-173">tooconfigure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow hello guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="b1bda-174">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="b1bda-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b1bda-175">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b1bda-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b1bda-176">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b1bda-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b1bda-177">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bda-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="b1bda-178">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b1bda-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b1bda-180">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b1bda-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1bda-181">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b1bda-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1bda-183">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1bda-185">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="b1bda-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1bda-187">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b1bda-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1bda-189">a.</span><span class="sxs-lookup"><span data-stu-id="b1bda-189">a.</span></span> <span data-ttu-id="b1bda-190">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1bda-191">b.</span><span class="sxs-lookup"><span data-stu-id="b1bda-191">b.</span></span> <span data-ttu-id="b1bda-192">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b1bda-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1bda-193">c.</span><span class="sxs-lookup"><span data-stu-id="b1bda-193">c.</span></span> <span data-ttu-id="b1bda-194">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b1bda-195">d.</span><span class="sxs-lookup"><span data-stu-id="b1bda-195">d.</span></span> <span data-ttu-id="b1bda-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="b1bda-197">Creazione di un utente test di Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="b1bda-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="b1bda-198">toolog agli utenti di Azure AD tooenable tooKeeper gestione Password & digitali insieme di credenziali, è necessario eseguirne il provisioning in Gestione Password detentore & digitali insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b1bda-198">tooenable Azure AD users toolog in tooKeeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="b1bda-199">L'applicazione supporta solo in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti verrà creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b1bda-199">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="b1bda-200">È possibile contattare [supporto detentore](https://keepersecurity.com/contact.html), se si desidera che gli utenti toosetup manualmente.</span><span class="sxs-lookup"><span data-stu-id="b1bda-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want toosetup users manually.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b1bda-201">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bda-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b1bda-202">In questa sezione, si abilita Britta Simon toouse single sign-on Azure concedendo tooKeeper gestione Password & digitali insieme di credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="b1bda-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKeeper Password Manager & Digital Vault.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b1bda-204">**tooassign Britta Simon tooKeeper gestione Password & digitali insieme di credenziali, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b1bda-204">**tooassign Britta Simon tooKeeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1bda-205">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b1bda-207">Nell'elenco di applicazioni hello, selezionare **gestione Password detentore & digitali insieme di credenziali**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-207">In hello applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="b1bda-209">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b1bda-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-211">Click **Add** button.</span></span> <span data-ttu-id="b1bda-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b1bda-214">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b1bda-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b1bda-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1bda-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b1bda-217">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b1bda-217">Testing single sign-on</span></span>

<span data-ttu-id="b1bda-218">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b1bda-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b1bda-219">Quando si fa clic su gestione Password detentore hello & riquadro digitale insieme di credenziali in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione di gestione di Password detentore & digitali insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b1bda-219">When you click hello Keeper Password Manager & Digital Vault tile in hello Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="b1bda-220">Quando l'autenticazione ha esito positivo, viene visualizzato in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b1bda-220">Upon successful authentication, you should get into hello application.</span></span> <span data-ttu-id="b1bda-221">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b1bda-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b1bda-222">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b1bda-222">Additional resources</span></span>

* [<span data-ttu-id="b1bda-223">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1bda-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1bda-224">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1bda-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

