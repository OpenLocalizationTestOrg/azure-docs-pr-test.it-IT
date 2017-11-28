---
title: 'Esercitazione: Integrazione di Azure Active Directory con SensoScientific Wireless Temperature Monitoring System | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e di sistema di monitoraggio della temperatura SensoScientific Wireless.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="a7f65-103">Esercitazione: Integrazione di Azure Active Directory con SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="a7f65-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="a7f65-104">In questa esercitazione, è illustrato come toointegrate SensoScientific sistema di monitoraggio Wireless temperatura con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7f65-104">In this tutorial, you learn how toointegrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7f65-105">Integrazione di sistema di monitoraggio della temperatura SensoScientific Wireless con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="a7f65-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a7f65-106">È possibile controllare in Azure AD che ha accesso tooSensoScientific sistema di monitoraggio della temperatura Wireless</span><span class="sxs-lookup"><span data-stu-id="a7f65-106">You can control in Azure AD who has access tooSensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="a7f65-107">È possibile abilitare l'utenti tooautomatically get connesso tooSensoScientific Wireless temperatura monitoraggio del sistema (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7f65-107">You can enable your users tooautomatically get signed-on tooSensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7f65-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a7f65-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a7f65-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7f65-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7f65-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a7f65-110">Prerequisites</span></span>

<span data-ttu-id="a7f65-111">integrazione di Azure AD con sistema di monitoraggio della temperatura SensoScientific Wireless tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="a7f65-111">tooconfigure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need hello following items:</span></span>

- <span data-ttu-id="a7f65-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7f65-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7f65-113">Una sottoscrizione abilitata per l'accesso Single Sign-On per SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="a7f65-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7f65-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="a7f65-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7f65-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="a7f65-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7f65-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a7f65-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7f65-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7f65-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7f65-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a7f65-118">Scenario description</span></span>
<span data-ttu-id="a7f65-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a7f65-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7f65-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="a7f65-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7f65-121">Aggiunta di sistema di monitoraggio della temperatura Wireless SensoScientific dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a7f65-121">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
2. <span data-ttu-id="a7f65-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7f65-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a><span data-ttu-id="a7f65-123">Aggiunta di sistema di monitoraggio della temperatura Wireless SensoScientific dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a7f65-123">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
<span data-ttu-id="a7f65-124">integrazione hello tooconfigure di sistema di monitoraggio della temperatura SensoScientific Wireless in Azure AD, è necessario tooadd SensoScientific Wireless temperatura Monitoraggio sistema dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a7f65-124">tooconfigure hello integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a7f65-125">**tooadd SensoScientific Wireless temperatura Monitoraggio sistema dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a7f65-125">**tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7f65-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a7f65-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7f65-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a7f65-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a7f65-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a7f65-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a7f65-133">Nella casella di ricerca hello, digitare **SensoScientific Wireless sistema di monitoraggio della temperatura**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-133">In hello search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="a7f65-135">Nel riquadro dei risultati hello, selezionare **SensoScientific Wireless sistema di monitoraggio della temperatura**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a7f65-135">In hello results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7f65-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7f65-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7f65-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SensoScientific Wireless Temperature Monitoring System con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a7f65-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a7f65-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nel sistema di monitoraggio della temperatura SensoScientific Wireless è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7f65-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SensoScientific Wireless Temperature Monitoring System is tooa user in Azure AD.</span></span> <span data-ttu-id="a7f65-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nel sistema di monitoraggio della temperatura SensoScientific Wireless deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="a7f65-140">In other words, a link relationship between an Azure AD user and hello related user in SensoScientific Wireless Temperature Monitoring System needs toobe established.</span></span>

<span data-ttu-id="a7f65-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nel sistema di monitoraggio della temperatura SensoScientific Wireless.</span><span class="sxs-lookup"><span data-stu-id="a7f65-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="a7f65-142">tooconfigure e prova AD Azure single sign-on con sistema di monitoraggio della temperatura SensoScientific Wireless, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="a7f65-142">tooconfigure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a7f65-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a7f65-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a7f65-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7f65-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7f65-145">**[Creazione di un utente di test di sistema di monitoraggio della temperatura Wireless SensoScientific](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave un equivalente di Britta Simon SensoScientific Wireless temperatura Monitoraggio sistema che è collegato rappresentazione toohello Azure AD utente.</span><span class="sxs-lookup"><span data-stu-id="a7f65-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - toohave a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7f65-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a7f65-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7f65-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a7f65-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7f65-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7f65-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7f65-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nell'applicazione di sistema di monitoraggio della temperatura SensoScientific Wireless.</span><span class="sxs-lookup"><span data-stu-id="a7f65-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="a7f65-150">**tooconfigure Azure single sign-on AD SensoScientific Wireless temperatura monitoraggio di sistema, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a7f65-150">**tooconfigure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7f65-151">Nel portale di Azure su hello hello **SensoScientific Wireless sistema di monitoraggio della temperatura** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-151">In hello Azure portal, on hello **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a7f65-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a7f65-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="a7f65-155">In hello **SensoScientific Wireless temperatura Monitoraggio sistema dominio e gli URL** non sezione tooperform è necessario alcun passaggio come applicazione hello è già pre-integrata con Azure:</span><span class="sxs-lookup"><span data-stu-id="a7f65-155">On hello **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need tooperform any steps as hello app is already pre-integrated with Azure:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="a7f65-157">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="a7f65-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="a7f65-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a7f65-159">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a7f65-161">In hello **SensoScientific configurazione sistema di monitoraggio della temperatura di Wireless** fare clic su **configurazione sistema di monitoraggio SensoScientific Wireless temperatura** tooopen  **Configurare l'accesso** finestra.</span><span class="sxs-lookup"><span data-stu-id="a7f65-161">On hello **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a7f65-162">Hello copia **Sign-Out URL, ID entità SAML** e **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="a7f65-162">Copy hello **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="a7f65-164">Accesso tooyour applicazione di sistema di monitoraggio della temperatura Wireless SensoScientific come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a7f65-164">Sign on tooyour SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="a7f65-165">Nel menu di navigazione hello in primo piano hello, fare clic su **configurazione** e goto **configura** in **Single Sign-On** tooopen hello Single Sign On Settings.</span><span class="sxs-lookup"><span data-stu-id="a7f65-165">In hello navigation menu on hello top, click **Configuration** and goto **Configure** under **Single Sign On** tooopen hello Single Sign On Settings.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="a7f65-167">In **Single Sign On Settings** form eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a7f65-167">In **Single Sign On Settings** form perform hello following steps:</span></span>
 
    <span data-ttu-id="a7f65-168">a.</span><span class="sxs-lookup"><span data-stu-id="a7f65-168">a.</span></span> <span data-ttu-id="a7f65-169">Selezionare il **Nome autorità emittente** come Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7f65-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="a7f65-170">b.</span><span class="sxs-lookup"><span data-stu-id="a7f65-170">b.</span></span> <span data-ttu-id="a7f65-171">Hello Incolla **ID entità SAML** che è stato copiato dal portale di Azure nella casella di testo URL autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="a7f65-171">Paste hello **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="a7f65-172">c.</span><span class="sxs-lookup"><span data-stu-id="a7f65-172">c.</span></span> <span data-ttu-id="a7f65-173">Hello Incolla **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure nella casella di testo URL servizio Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a7f65-173">Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="a7f65-174">d.</span><span class="sxs-lookup"><span data-stu-id="a7f65-174">d.</span></span> <span data-ttu-id="a7f65-175">Hello Incolla **Sign-Out URL** che è stato copiato dal portale di Azure nella casella di testo URL del servizio Single Sign-Out.</span><span class="sxs-lookup"><span data-stu-id="a7f65-175">Paste hello **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="a7f65-176">e.</span><span class="sxs-lookup"><span data-stu-id="a7f65-176">e.</span></span> <span data-ttu-id="a7f65-177">Sfoglia hello certificato è stato scaricato dal portale di Azure e caricare qui.</span><span class="sxs-lookup"><span data-stu-id="a7f65-177">Browse hello certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="a7f65-178">f.</span><span class="sxs-lookup"><span data-stu-id="a7f65-178">f.</span></span> <span data-ttu-id="a7f65-179">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="a7f65-180">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="a7f65-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a7f65-181">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="a7f65-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a7f65-182">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7f65-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7f65-183">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7f65-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7f65-184">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a7f65-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a7f65-186">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a7f65-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7f65-187">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a7f65-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7f65-189">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7f65-191">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="a7f65-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7f65-193">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a7f65-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7f65-195">a.</span><span class="sxs-lookup"><span data-stu-id="a7f65-195">a.</span></span> <span data-ttu-id="a7f65-196">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7f65-197">b.</span><span class="sxs-lookup"><span data-stu-id="a7f65-197">b.</span></span> <span data-ttu-id="a7f65-198">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7f65-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7f65-199">c.</span><span class="sxs-lookup"><span data-stu-id="a7f65-199">c.</span></span> <span data-ttu-id="a7f65-200">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a7f65-201">d.</span><span class="sxs-lookup"><span data-stu-id="a7f65-201">d.</span></span> <span data-ttu-id="a7f65-202">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="a7f65-203">Creazione di un utente test di SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="a7f65-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="a7f65-204">toolog agli utenti di Azure AD tooenable in tooSensoScientific sistema di monitoraggio della temperatura Wireless, è necessario eseguirne il provisioning nel sistema di monitoraggio della temperatura SensoScientific Wireless.</span><span class="sxs-lookup"><span data-stu-id="a7f65-204">tooenable Azure AD users toolog in tooSensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="a7f65-205">Lavorare con [team di supporto di sistema di monitoraggio della temperatura Wireless SensoScientific](https://www.sensoscientific.com/contact-us/) per aggiungere gli utenti di hello nella piattaforma di sistema di monitoraggio della temperatura SensoScientific Wireless hello.</span><span class="sxs-lookup"><span data-stu-id="a7f65-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add hello users in hello SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="a7f65-206">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a7f65-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a7f65-207">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7f65-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a7f65-208">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSensoScientific sistema di monitoraggio della temperatura Wireless.</span><span class="sxs-lookup"><span data-stu-id="a7f65-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSensoScientific Wireless Temperature Monitoring System.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a7f65-210">**tooassign Britta Simon tooSensoScientific sistema di monitoraggio della temperatura Wireless, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a7f65-210">**tooassign Britta Simon tooSensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7f65-211">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a7f65-213">Nell'elenco di applicazioni hello, selezionare **SensoScientific Wireless sistema di monitoraggio della temperatura**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-213">In hello applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="a7f65-215">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a7f65-217">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-217">Click **Add** button.</span></span> <span data-ttu-id="a7f65-218">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a7f65-220">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="a7f65-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a7f65-221">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7f65-222">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a7f65-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7f65-223">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a7f65-223">Testing single sign-on</span></span>

<span data-ttu-id="a7f65-224">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a7f65-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="a7f65-225">Fare clic sul riquadro di sistema di monitoraggio della temperatura SensoScientific Wireless hello in hello Pannello di accesso, sarà l'applicazione di sistema di monitoraggio SensoScientific Wireless temperatura tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="a7f65-225">Click hello SensoScientific Wireless Temperature Monitoring System tile in hello Access Panel, you will be automatically signed-on tooyour SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="a7f65-226">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="a7f65-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7f65-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a7f65-227">Additional resources</span></span>

* [<span data-ttu-id="a7f65-228">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7f65-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7f65-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7f65-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

