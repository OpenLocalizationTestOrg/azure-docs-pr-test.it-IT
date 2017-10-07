---
title: 'Esercitazione: Integrazione di Azure Active Directory con Namely | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e in particolare.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="90bc8-103">Esercitazione: Integrazione di Azure Active Directory con Namely</span><span class="sxs-lookup"><span data-stu-id="90bc8-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="90bc8-104">In questa esercitazione, è illustrato come toointegrate, vale a dire con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90bc8-104">In this tutorial, you learn how toointegrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90bc8-105">Vale a dire l'integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="90bc8-105">Integrating Namely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="90bc8-106">È possibile controllare in Azure AD che ha accesso tooNamely</span><span class="sxs-lookup"><span data-stu-id="90bc8-106">You can control in Azure AD who has access tooNamely</span></span>
- <span data-ttu-id="90bc8-107">È possibile abilitare l'utenti tooautomatically get connesso tooNamely (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="90bc8-107">You can enable your users tooautomatically get signed-on tooNamely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90bc8-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="90bc8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="90bc8-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90bc8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90bc8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="90bc8-110">Prerequisites</span></span>

<span data-ttu-id="90bc8-111">integrazione di tooconfigure Azure AD con in particolare, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="90bc8-111">tooconfigure Azure AD integration with Namely, you need hello following items:</span></span>

- <span data-ttu-id="90bc8-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90bc8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90bc8-113">Sottoscrizione di Namely abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="90bc8-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90bc8-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="90bc8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90bc8-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="90bc8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90bc8-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="90bc8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="90bc8-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90bc8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90bc8-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="90bc8-118">Scenario description</span></span>
<span data-ttu-id="90bc8-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="90bc8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90bc8-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="90bc8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90bc8-121">Vale a dire aggiunta dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="90bc8-121">Adding Namely from hello gallery</span></span>
2. <span data-ttu-id="90bc8-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90bc8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-hello-gallery"></a><span data-ttu-id="90bc8-123">Vale a dire aggiunta dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="90bc8-123">Adding Namely from hello gallery</span></span>
<span data-ttu-id="90bc8-124">integrazione hello tooconfigure di vale a dire in Azure AD, è necessario tooadd particolare elenco hello raccolta tooyour di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="90bc8-124">tooconfigure hello integration of Namely into Azure AD, you need tooadd Namely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="90bc8-125">**tooadd ovvero dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="90bc8-125">**tooadd Namely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="90bc8-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="90bc8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90bc8-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="90bc8-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="90bc8-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="90bc8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="90bc8-133">Nella casella di ricerca hello, digitare **vale a dire**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-133">In hello search box, type **Namely**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="90bc8-135">Nel riquadro dei risultati hello, selezionare **vale a dire**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="90bc8-135">In hello results panel, select **Namely**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90bc8-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90bc8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90bc8-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Namely in base a un utente di prova di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="90bc8-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="90bc8-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in particolare è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90bc8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Namely is tooa user in Azure AD.</span></span> <span data-ttu-id="90bc8-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in deve in particolare toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="90bc8-140">In other words, a link relationship between an Azure AD user and hello related user in Namely needs toobe established.</span></span>

<span data-ttu-id="90bc8-141">In particolare, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="90bc8-141">In Namely, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="90bc8-142">tooconfigure e test di Azure AD single sign-on in particolare, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="90bc8-142">tooconfigure and test Azure AD single sign-on with Namely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="90bc8-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="90bc8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="90bc8-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90bc8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90bc8-145">**[Creazione di un particolare utente di test](#creating-a-namely-test-user)**  -toohave un equivalente di Britta Simon in vale a dire che è collegato toohello rappresentazione in forma di Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="90bc8-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - toohave a counterpart of Britta Simon in Namely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="90bc8-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="90bc8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90bc8-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="90bc8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90bc8-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90bc8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90bc8-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in particolare è l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="90bc8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="90bc8-150">**Azure AD tooconfigure single sign-on con, ovvero eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="90bc8-150">**tooconfigure Azure AD single sign-on with Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="90bc8-151">Nel portale di Azure su hello hello **vale a dire** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-151">In hello Azure portal, on hello **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="90bc8-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="90bc8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="90bc8-155">In hello **vale a dire dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="90bc8-155">On hello **Namely Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="90bc8-157">a.</span><span class="sxs-lookup"><span data-stu-id="90bc8-157">a.</span></span> <span data-ttu-id="90bc8-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="90bc8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="90bc8-159">b.</span><span class="sxs-lookup"><span data-stu-id="90bc8-159">b.</span></span> <span data-ttu-id="90bc8-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="90bc8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="90bc8-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="90bc8-161">These values are not real.</span></span> <span data-ttu-id="90bc8-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="90bc8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="90bc8-163">Contatto [team di supporto Client vale a dire](https://www.namely.com/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="90bc8-163">Contact [Namely Client support team](https://www.namely.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="90bc8-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="90bc8-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="90bc8-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="90bc8-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="90bc8-168">In hello **particolare configurazione** fare clic su **configurare ovvero** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="90bc8-168">On hello **Namely Configuration** section, click **Configure Namely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="90bc8-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="90bc8-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="90bc8-171">In un'altra finestra del browser, accedere tooyour vale a dire il sito della società come amministratore.</span><span class="sxs-lookup"><span data-stu-id="90bc8-171">In another browser window, sign on tooyour Namely company site as an administrator.</span></span>

8. <span data-ttu-id="90bc8-172">Nella barra degli strumenti hello in primo piano hello, fare clic su **società**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-172">In hello toolbar on hello top, click **Company**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="90bc8-174">Fare clic su hello **impostazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="90bc8-174">Click hello **Settings** tab.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="90bc8-176">Fare clic su **SAML**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-176">Click **SAML**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="90bc8-178">In hello **impostazioni SAML** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="90bc8-178">On hello **SAML Settings** page, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="90bc8-180">a.</span><span class="sxs-lookup"><span data-stu-id="90bc8-180">a.</span></span> <span data-ttu-id="90bc8-181">Fare clic su **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="90bc8-182">b.</span><span class="sxs-lookup"><span data-stu-id="90bc8-182">b.</span></span> <span data-ttu-id="90bc8-183">In hello **SSO url provider di identità** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="90bc8-183">In hello **Identity provider SSO url** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="90bc8-184">c.</span><span class="sxs-lookup"><span data-stu-id="90bc8-184">c.</span></span> <span data-ttu-id="90bc8-185">Aprire il certificato scaricato nel blocco note, hello copia il contenuto e quindi incollarlo hello **certificato provider di identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="90bc8-185">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="90bc8-186">d.</span><span class="sxs-lookup"><span data-stu-id="90bc8-186">d.</span></span> <span data-ttu-id="90bc8-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="90bc8-188">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="90bc8-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="90bc8-189">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="90bc8-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="90bc8-190">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="90bc8-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90bc8-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90bc8-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="90bc8-192">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="90bc8-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="90bc8-194">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="90bc8-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="90bc8-195">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="90bc8-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90bc8-197">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90bc8-199">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="90bc8-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90bc8-201">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="90bc8-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90bc8-203">a.</span><span class="sxs-lookup"><span data-stu-id="90bc8-203">a.</span></span> <span data-ttu-id="90bc8-204">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90bc8-205">b.</span><span class="sxs-lookup"><span data-stu-id="90bc8-205">b.</span></span> <span data-ttu-id="90bc8-206">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="90bc8-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90bc8-207">c.</span><span class="sxs-lookup"><span data-stu-id="90bc8-207">c.</span></span> <span data-ttu-id="90bc8-208">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="90bc8-209">d.</span><span class="sxs-lookup"><span data-stu-id="90bc8-209">d.</span></span> <span data-ttu-id="90bc8-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="90bc8-211">Creazione di un utente test per Namely</span><span class="sxs-lookup"><span data-stu-id="90bc8-211">Creating a Namely test user</span></span>

<span data-ttu-id="90bc8-212">obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon in particolare.</span><span class="sxs-lookup"><span data-stu-id="90bc8-212">hello objective of this section is toocreate a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="90bc8-213">**un utente denominato Britta Simon in particolare, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="90bc8-213">**toocreate a user called Britta Simon in Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="90bc8-214">Vale a dire, tooyour Sign-on aziendali sito come amministratore.</span><span class="sxs-lookup"><span data-stu-id="90bc8-214">Sign-on tooyour Namely company site as an administrator.</span></span>

2. <span data-ttu-id="90bc8-215">Nella barra degli strumenti hello in primo piano hello, fare clic su **persone**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-215">In hello toolbar on hello top, click **People**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="90bc8-217">Fare clic su hello **Directory** scheda.</span><span class="sxs-lookup"><span data-stu-id="90bc8-217">Click hello **Directory** tab.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="90bc8-219">Fare clic su **Add New Person**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-219">Click **Add New Person**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="90bc8-221">In hello **Add New Person** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="90bc8-221">On hello **Add New Person** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="90bc8-222">a.</span><span class="sxs-lookup"><span data-stu-id="90bc8-222">a.</span></span> <span data-ttu-id="90bc8-223">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-223">In hello **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="90bc8-224">b.</span><span class="sxs-lookup"><span data-stu-id="90bc8-224">b.</span></span> <span data-ttu-id="90bc8-225">In hello **cognome** casella tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-225">In hello **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="90bc8-226">c.</span><span class="sxs-lookup"><span data-stu-id="90bc8-226">c.</span></span> <span data-ttu-id="90bc8-227">In hello **posta elettronica** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="90bc8-227">In hello **Email** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90bc8-228">d.</span><span class="sxs-lookup"><span data-stu-id="90bc8-228">d.</span></span> <span data-ttu-id="90bc8-229">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-229">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="90bc8-230">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="90bc8-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="90bc8-231">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooNamely.</span><span class="sxs-lookup"><span data-stu-id="90bc8-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNamely.</span></span>

![Assegna utente][200] 

<span data-ttu-id="90bc8-233">**tooassign Britta Simon tooNamely, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="90bc8-233">**tooassign Britta Simon tooNamely, perform hello following steps:**</span></span>

1. <span data-ttu-id="90bc8-234">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="90bc8-236">Nell'elenco di applicazioni hello, selezionare **vale a dire**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-236">In hello applications list, select **Namely**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="90bc8-238">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="90bc8-240">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-240">Click **Add** button.</span></span> <span data-ttu-id="90bc8-241">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="90bc8-243">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="90bc8-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="90bc8-244">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90bc8-245">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="90bc8-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="90bc8-246">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="90bc8-246">Testing single sign-on</span></span>

<span data-ttu-id="90bc8-247">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="90bc8-247">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="90bc8-248">Quando si fa clic hello riquadro vale a dire in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in particolare dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="90bc8-248">When you click hello Namely tile in hello Access Panel, you should get automatically signed-on tooyour Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90bc8-249">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="90bc8-249">Additional resources</span></span>

* [<span data-ttu-id="90bc8-250">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90bc8-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90bc8-251">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90bc8-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

