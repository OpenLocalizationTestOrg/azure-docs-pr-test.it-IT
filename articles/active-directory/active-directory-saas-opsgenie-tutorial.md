---
title: 'Esercitazione: Integrazione di Azure Active Directory con OpsGenie | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e OpsGenie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 50d31c234fb9716d05d681b9bc4164740a3a662b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="24e12-103">Esercitazione: Integrazione di Azure Active Directory con OpsGenie</span><span class="sxs-lookup"><span data-stu-id="24e12-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="24e12-104">In questa esercitazione, è illustrato come toointegrate OpsGenie con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24e12-104">In this tutorial, you learn how toointegrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24e12-105">Integrazione OpsGenie con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="24e12-105">Integrating OpsGenie with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24e12-106">È possibile controllare in Azure AD che ha accesso tooOpsGenie</span><span class="sxs-lookup"><span data-stu-id="24e12-106">You can control in Azure AD who has access tooOpsGenie</span></span>
- <span data-ttu-id="24e12-107">È possibile abilitare l'utenti tooautomatically get connesso tooOpsGenie (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="24e12-107">You can enable your users tooautomatically get signed-on tooOpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24e12-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="24e12-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24e12-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24e12-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24e12-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="24e12-110">Prerequisites</span></span>

<span data-ttu-id="24e12-111">integrazione di Azure AD con OpsGenie tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="24e12-111">tooconfigure Azure AD integration with OpsGenie, you need hello following items:</span></span>

- <span data-ttu-id="24e12-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24e12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24e12-113">Sottoscrizione di OpsGenie abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="24e12-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24e12-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="24e12-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24e12-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="24e12-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24e12-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="24e12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24e12-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24e12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24e12-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="24e12-118">Scenario description</span></span>
<span data-ttu-id="24e12-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="24e12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24e12-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="24e12-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24e12-121">Aggiunta di OpsGenie dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="24e12-121">Adding OpsGenie from hello gallery</span></span>
2. <span data-ttu-id="24e12-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="24e12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-hello-gallery"></a><span data-ttu-id="24e12-123">Aggiunta di OpsGenie dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="24e12-123">Adding OpsGenie from hello gallery</span></span>
<span data-ttu-id="24e12-124">integrazione hello tooconfigure di OpsGenie in Azure AD, è necessario tooadd OpsGenie dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="24e12-124">tooconfigure hello integration of OpsGenie into Azure AD, you need tooadd OpsGenie from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24e12-125">**tooadd OpsGenie dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="24e12-125">**tooadd OpsGenie from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24e12-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="24e12-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24e12-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="24e12-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24e12-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="24e12-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="24e12-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="24e12-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="24e12-133">Nella casella di ricerca hello, digitare **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="24e12-133">In hello search box, type **OpsGenie**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="24e12-135">Nel riquadro dei risultati hello, selezionare **OpsGenie**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="24e12-135">In hello results panel, select **OpsGenie**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24e12-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="24e12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24e12-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con OpsGenie in base a un utente di prova di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="24e12-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24e12-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in OpsGenie è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24e12-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OpsGenie is tooa user in Azure AD.</span></span> <span data-ttu-id="24e12-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in OpsGenie deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="24e12-140">In other words, a link relationship between an Azure AD user and hello related user in OpsGenie needs toobe established.</span></span>

<span data-ttu-id="24e12-141">In OpsGenie, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="24e12-141">In OpsGenie, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="24e12-142">tooconfigure e prova AD Azure single sign-on con OpsGenie, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="24e12-142">tooconfigure and test Azure AD single sign-on with OpsGenie, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24e12-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="24e12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24e12-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="24e12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24e12-145">**[Creazione di un utente test OpsGenie](#creating-a-opsgenie-test-user)**  -toohave un equivalente di Britta Simon in OpsGenie che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="24e12-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - toohave a counterpart of Britta Simon in OpsGenie that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24e12-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="24e12-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24e12-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="24e12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24e12-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="24e12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24e12-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="24e12-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="24e12-150">**Azure AD tooconfigure single sign-on con OpsGenie, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="24e12-150">**tooconfigure Azure AD single sign-on with OpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="24e12-151">Nel portale di Azure su hello hello **OpsGenie** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="24e12-151">In hello Azure portal, on hello **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="24e12-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="24e12-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="24e12-155">In hello **OpsGenie dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="24e12-155">On hello **OpsGenie Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="24e12-157">In hello **Sign-on URL** casella di testo, digitare l'URL hello:`https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="24e12-157">In hello **Sign-on URL** textbox, type hello URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="24e12-158">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="24e12-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="24e12-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="24e12-160">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="24e12-162">In hello **OpsGenie configurazione** fare clic su **configurare OpsGenie** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="24e12-162">On hello **OpsGenie Configuration** section, click **Configure OpsGenie** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="24e12-163">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="24e12-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="24e12-165">Aprire un'altra istanza del browser e quindi log tooOpsGenie come amministratore.</span><span class="sxs-lookup"><span data-stu-id="24e12-165">Open another browser instance, and then log-in tooOpsGenie as an administrator.</span></span>

8. <span data-ttu-id="24e12-166">Fare clic su **impostazioni**, quindi fare clic su hello **Single Sign-On** scheda.</span><span class="sxs-lookup"><span data-stu-id="24e12-166">Click **Settings**, and then click hello **Single Sign On** tab.</span></span>
   
    ![Accesso Single Sign-On di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="24e12-168">Selezionare tooenable SSO, **abilitato**.</span><span class="sxs-lookup"><span data-stu-id="24e12-168">tooenable SSO, select **Enabled**.</span></span>
   
    ![Impostazioni di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="24e12-170">In hello **Provider** fare clic su hello **Azure Active Directory** scheda.</span><span class="sxs-lookup"><span data-stu-id="24e12-170">In hello **Provider** section, click hello **Azure Active Directory** tab.</span></span>
   
    ![Impostazioni di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="24e12-172">Nella pagina della finestra di Azure Active Directory hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="24e12-172">On hello Azure Active Directory dialog page, perform hello following steps:</span></span>
   
    ![Impostazioni di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="24e12-174">a.</span><span class="sxs-lookup"><span data-stu-id="24e12-174">a.</span></span> <span data-ttu-id="24e12-175">Incolla **Single Sign On Service URL**, che è stato copiato dal portale di Azure hello in hello **SAML 2.0 Endpoint** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="24e12-175">Paste **Single Sign On Service URL**, which you have copied from hello Azure portal into hello **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="24e12-176">b.</span><span class="sxs-lookup"><span data-stu-id="24e12-176">b.</span></span> <span data-ttu-id="24e12-177">Aprire il certificato con codificato base 64 scaricato nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo hello **certificato x. 500** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="24e12-177">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="24e12-178">c.</span><span class="sxs-lookup"><span data-stu-id="24e12-178">c.</span></span> <span data-ttu-id="24e12-179">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="24e12-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="24e12-180">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="24e12-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24e12-181">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="24e12-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24e12-182">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24e12-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24e12-183">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="24e12-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="24e12-184">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="24e12-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="24e12-186">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="24e12-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24e12-187">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="24e12-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24e12-189">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="24e12-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24e12-191">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="24e12-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24e12-193">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="24e12-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24e12-195">a.</span><span class="sxs-lookup"><span data-stu-id="24e12-195">a.</span></span> <span data-ttu-id="24e12-196">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24e12-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24e12-197">b.</span><span class="sxs-lookup"><span data-stu-id="24e12-197">b.</span></span> <span data-ttu-id="24e12-198">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="24e12-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24e12-199">c.</span><span class="sxs-lookup"><span data-stu-id="24e12-199">c.</span></span> <span data-ttu-id="24e12-200">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="24e12-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24e12-201">d.</span><span class="sxs-lookup"><span data-stu-id="24e12-201">d.</span></span> <span data-ttu-id="24e12-202">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="24e12-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="24e12-203">Creazione di un utente di test di OpsGenie</span><span class="sxs-lookup"><span data-stu-id="24e12-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="24e12-204">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in OpsGenie toocreate.</span><span class="sxs-lookup"><span data-stu-id="24e12-204">hello objective of this section is toocreate a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="24e12-205">In una finestra del Web browser accedere al tenant di OpsGenie come amministratore.</span><span class="sxs-lookup"><span data-stu-id="24e12-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="24e12-206">Passare tooUsers elenco facendo clic su **utente** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="24e12-206">Navigate tooUsers list by clicking **User** in left panel.</span></span>
   
   ![Impostazioni di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="24e12-208">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="24e12-208">Click **Add User**.</span></span>

4. <span data-ttu-id="24e12-209">In hello **Aggiungi utente** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="24e12-209">On hello **Add User** dialog, perform hello following steps:</span></span>
   
   ![Impostazioni di OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="24e12-211">a.</span><span class="sxs-lookup"><span data-stu-id="24e12-211">a.</span></span> <span data-ttu-id="24e12-212">In hello **posta elettronica** casella Indirizzo di posta elettronica di tipo hello del BrittaSimon indirizzati in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="24e12-212">In hello **Email** textbox, type hello email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="24e12-213">b.</span><span class="sxs-lookup"><span data-stu-id="24e12-213">b.</span></span> <span data-ttu-id="24e12-214">In hello **nome completo** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="24e12-214">In hello **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="24e12-215">c.</span><span class="sxs-lookup"><span data-stu-id="24e12-215">c.</span></span> <span data-ttu-id="24e12-216">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="24e12-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="24e12-217">Britta riceve un messaggio di posta elettronica con istruzioni per la configurazione del profilo.</span><span class="sxs-lookup"><span data-stu-id="24e12-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="24e12-218">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="24e12-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="24e12-219">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooOpsGenie.</span><span class="sxs-lookup"><span data-stu-id="24e12-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOpsGenie.</span></span>

![Assegna utente][200] 

<span data-ttu-id="24e12-221">**tooassign Britta Simon tooOpsGenie, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="24e12-221">**tooassign Britta Simon tooOpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="24e12-222">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="24e12-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="24e12-224">Nell'elenco di applicazioni hello, selezionare **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="24e12-224">In hello applications list, select **OpsGenie**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="24e12-226">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="24e12-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="24e12-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="24e12-228">Click **Add** button.</span></span> <span data-ttu-id="24e12-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="24e12-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="24e12-231">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="24e12-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24e12-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="24e12-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24e12-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="24e12-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24e12-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="24e12-234">Testing single sign-on</span></span>

<span data-ttu-id="24e12-235">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="24e12-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="24e12-236">Quando si fa clic su riquadro OpsGenie hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour OpsGenie applicazione.</span><span class="sxs-lookup"><span data-stu-id="24e12-236">When you click hello OpsGenie tile in hello Access Panel, you should get automatically signed-on tooyour OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24e12-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="24e12-237">Additional resources</span></span>

* [<span data-ttu-id="24e12-238">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24e12-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24e12-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24e12-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

