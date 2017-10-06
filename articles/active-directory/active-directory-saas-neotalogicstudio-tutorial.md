---
title: 'Esercitazione: Integrazione di Azure Active Directory con Neota Logic Studio | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Neota logica di Studio.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: a479ee49618de8275132dbc2c21a8ef723d92d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="1d866-103">Esercitazione: Integrazione di Azure Active Directory con Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="1d866-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="1d866-104">In questa esercitazione, è illustrato come toointegrate Neota logica Studio con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1d866-104">In this tutorial, you learn how toointegrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d866-105">Integrazione Neota logica Studio con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1d866-105">Integrating Neota Logic Studio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1d866-106">È possibile controllare in Azure AD che ha accesso tooNeota Studio logica</span><span class="sxs-lookup"><span data-stu-id="1d866-106">You can control in Azure AD who has access tooNeota Logic Studio</span></span>
- <span data-ttu-id="1d866-107">È possibile abilitare l'utenti tooautomatically get connesso tooNeota Studio logica (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d866-107">You can enable your users tooautomatically get signed-on tooNeota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d866-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1d866-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1d866-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere.</span><span class="sxs-lookup"><span data-stu-id="1d866-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="1d866-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1d866-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d866-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1d866-111">Prerequisites</span></span>

<span data-ttu-id="1d866-112">integrazione di Azure AD con Neota logica Studio tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1d866-112">tooconfigure Azure AD integration with Neota Logic Studio, you need hello following items:</span></span>

- <span data-ttu-id="1d866-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d866-113">An Azure AD subscription</span></span>
- <span data-ttu-id="1d866-114">Sottoscrizione di Neota Logic Studio abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1d866-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d866-115">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1d866-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d866-116">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1d866-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d866-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1d866-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1d866-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d866-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d866-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1d866-119">Scenario description</span></span>

<span data-ttu-id="1d866-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1d866-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d866-121">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1d866-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d866-122">Aggiunta di Studio logica Neota dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1d866-122">Adding Neota Logic Studio from hello gallery</span></span>
2. <span data-ttu-id="1d866-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d866-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-hello-gallery"></a><span data-ttu-id="1d866-124">Aggiunta di Studio logica Neota dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1d866-124">Adding Neota Logic Studio from hello gallery</span></span>

<span data-ttu-id="1d866-125">integrazione hello tooconfigure di Neota logica Studio in Azure AD, è necessario tooadd Studio logica Neota dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1d866-125">tooconfigure hello integration of Neota Logic Studio into Azure AD, you need tooadd Neota Logic Studio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1d866-126">**tooadd Neota logica Studio dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d866-126">**tooadd Neota Logic Studio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d866-127">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1d866-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d866-129">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1d866-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1d866-130">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1d866-130">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1d866-132">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1d866-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1d866-134">Nella casella di ricerca hello, digitare **Neota logica Studio**.</span><span class="sxs-lookup"><span data-stu-id="1d866-134">In hello search box, type **Neota Logic Studio**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="1d866-136">Nel riquadro dei risultati hello, selezionare **Neota logica Studio**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1d866-136">In hello results panel, select **Neota Logic Studio**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d866-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d866-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="1d866-139">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Neota Logic Studio con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1d866-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1d866-140">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Studio logica Neota è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d866-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Neota Logic Studio is tooa user in Azure AD.</span></span> <span data-ttu-id="1d866-141">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Studio logica Neota deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1d866-141">In other words, a link relationship between an Azure AD user and hello related user in Neota Logic Studio needs toobe established.</span></span>

<span data-ttu-id="1d866-142">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Neota logica di Studio.</span><span class="sxs-lookup"><span data-stu-id="1d866-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="1d866-143">tooconfigure e prova AD Azure single sign-on con Neota logica Studio, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1d866-143">tooconfigure and test Azure AD single sign-on with Neota Logic Studio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1d866-144">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1d866-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1d866-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1d866-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d866-146">**[Creazione di un utente test Neota logica Studio](#creating-a-neota-logic-studio-test-user)**  -toohave un equivalente di Britta Simon Neota logica Studio che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1d866-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - toohave a counterpart of Britta Simon in Neota Logic Studio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1d866-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1d866-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d866-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1d866-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d866-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d866-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d866-150">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Neota logica Studio.</span><span class="sxs-lookup"><span data-stu-id="1d866-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="1d866-151">**tooconfigure AD Azure single sign-on con Neota logica Studio, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d866-151">**tooconfigure Azure AD single sign-on with Neota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d866-152">Nel portale di Azure su hello hello **Neota logica Studio** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1d866-152">In hello Azure portal, on hello **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1d866-154">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1d866-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="1d866-156">In hello **Neota logica Studio dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1d866-156">On hello **Neota Logic Studio Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="1d866-158">a.</span><span class="sxs-lookup"><span data-stu-id="1d866-158">a.</span></span> <span data-ttu-id="1d866-159">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="1d866-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="1d866-160">b.</span><span class="sxs-lookup"><span data-stu-id="1d866-160">b.</span></span> <span data-ttu-id="1d866-161">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="1d866-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1d866-162">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="1d866-162">These values are not hello real.</span></span> <span data-ttu-id="1d866-163">Aggiornare questi valori con hello effettivo URL Sign-On e identificatore.</span><span class="sxs-lookup"><span data-stu-id="1d866-163">Update these values with hello actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="1d866-164">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="1d866-164">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="1d866-165">Contatto [team di supporto Client di Studio logica Neota](https://www.neotalogic.com/contact-us/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="1d866-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="1d866-166">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1d866-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="1d866-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1d866-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1d866-170">tooget SSO configurato per l'applicazione, contattare [supporto Studio logica Neota](https://www.neotalogic.com/contact-us/) del team e fornire loro con scaricato **Metadata XML** file.</span><span class="sxs-lookup"><span data-stu-id="1d866-170">tooget SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="1d866-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1d866-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1d866-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1d866-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1d866-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1d866-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d866-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d866-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d866-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1d866-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1d866-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d866-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d866-178">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1d866-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1d866-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d866-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d866-182">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1d866-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d866-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1d866-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d866-186">a.</span><span class="sxs-lookup"><span data-stu-id="1d866-186">a.</span></span> <span data-ttu-id="1d866-187">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1d866-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d866-188">b.</span><span class="sxs-lookup"><span data-stu-id="1d866-188">b.</span></span> <span data-ttu-id="1d866-189">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1d866-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d866-190">c.</span><span class="sxs-lookup"><span data-stu-id="1d866-190">c.</span></span> <span data-ttu-id="1d866-191">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1d866-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1d866-192">d.</span><span class="sxs-lookup"><span data-stu-id="1d866-192">d.</span></span> <span data-ttu-id="1d866-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1d866-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="1d866-194">Creazione di un utente test di Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="1d866-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="1d866-195">In questa sezione si crea un utente di nome Britta Simon in Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="1d866-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="1d866-196">funzionano con [team di supporto Client di Studio logica Neota](https://www.neotalogic.com/contact-us/) per aggiungere gli utenti di hello nella piattaforma Neota logica Studio hello.</span><span class="sxs-lookup"><span data-stu-id="1d866-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add hello users in hello Neota Logic Studio platform.</span></span> <span data-ttu-id="1d866-197">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1d866-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1d866-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d866-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1d866-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooNeota Studio logica.</span><span class="sxs-lookup"><span data-stu-id="1d866-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNeota Logic Studio.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1d866-201">**tooassign Britta Simon tooNeota logica Studio, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d866-201">**tooassign Britta Simon tooNeota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d866-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1d866-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1d866-204">Nell'elenco di applicazioni hello, selezionare **Neota logica Studio**.</span><span class="sxs-lookup"><span data-stu-id="1d866-204">In hello applications list, select **Neota Logic Studio**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="1d866-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d866-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1d866-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1d866-208">Click **Add** button.</span></span> <span data-ttu-id="1d866-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1d866-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1d866-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1d866-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1d866-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d866-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d866-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1d866-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1d866-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1d866-214">Testing single sign-on</span></span>

<span data-ttu-id="1d866-215">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1d866-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1d866-216">Fare clic sul riquadro Neota logica Studio hello in hello Pannello di accesso, sarà reindirizzato tooOrganization pagina sign-on.</span><span class="sxs-lookup"><span data-stu-id="1d866-216">Click hello Neota Logic Studio tile in hello Access Panel, you will be redirected tooOrganization sign-on page.</span></span> <span data-ttu-id="1d866-217">Dopo aver eseguito l'accesso, sarà connesso tooyour applicazione Neota logica Studio.</span><span class="sxs-lookup"><span data-stu-id="1d866-217">After successful login, you will be signed-on tooyour Neota Logic Studio application.</span></span> <span data-ttu-id="1d866-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="1d866-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="1d866-219">Per ulteriori informazioni su hello Pannello di accesso, vedere [Introduzione al pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="1d866-219">For more information about hello Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1d866-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1d866-220">Additional resources</span></span>

* [<span data-ttu-id="1d866-221">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d866-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d866-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d866-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

