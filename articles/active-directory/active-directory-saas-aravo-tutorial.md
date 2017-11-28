---
title: 'Esercitazione: Integrazione di Azure Active Directory con Aravo | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Aravo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 224939d8-2c9c-4561-968d-62722f5ab5ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 8f1336fa307fa9e8d625440a573d9f9d79dd820b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aravo"></a><span data-ttu-id="1013a-103">Esercitazione: Integrazione di Azure Active Directory con Aravo</span><span class="sxs-lookup"><span data-stu-id="1013a-103">Tutorial: Azure Active Directory integration with Aravo</span></span>

<span data-ttu-id="1013a-104">In questa esercitazione, è illustrato come toointegrate Aravo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1013a-104">In this tutorial, you learn how toointegrate Aravo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1013a-105">Integrazione Aravo con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1013a-105">Integrating Aravo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1013a-106">È possibile controllare in Azure AD che ha accesso tooAravo</span><span class="sxs-lookup"><span data-stu-id="1013a-106">You can control in Azure AD who has access tooAravo</span></span>
- <span data-ttu-id="1013a-107">È possibile abilitare l'utenti tooautomatically get connesso tooAravo (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1013a-107">You can enable your users tooautomatically get signed-on tooAravo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1013a-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1013a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1013a-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1013a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1013a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1013a-110">Prerequisites</span></span>

<span data-ttu-id="1013a-111">integrazione di Azure AD con Aravo tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1013a-111">tooconfigure Azure AD integration with Aravo, you need hello following items:</span></span>

- <span data-ttu-id="1013a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1013a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1013a-113">Sottoscrizione di Aravo abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1013a-113">An Aravo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1013a-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1013a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1013a-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1013a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1013a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1013a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1013a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1013a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1013a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1013a-118">Scenario description</span></span>
<span data-ttu-id="1013a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1013a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1013a-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1013a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1013a-121">Aggiunta di Aravo dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1013a-121">Adding Aravo from hello gallery</span></span>
2. <span data-ttu-id="1013a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1013a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aravo-from-hello-gallery"></a><span data-ttu-id="1013a-123">Aggiunta di Aravo dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1013a-123">Adding Aravo from hello gallery</span></span>
<span data-ttu-id="1013a-124">integrazione hello tooconfigure di Aravo in Azure AD, è necessario tooadd Aravo dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1013a-124">tooconfigure hello integration of Aravo into Azure AD, you need tooadd Aravo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1013a-125">**tooadd Aravo dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1013a-125">**tooadd Aravo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1013a-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1013a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1013a-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1013a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1013a-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1013a-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1013a-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1013a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1013a-133">Nella casella di ricerca hello, digitare **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="1013a-133">In hello search box, type **Aravo**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_search.png)

5. <span data-ttu-id="1013a-135">Nel riquadro dei risultati hello, selezionare **Aravo**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1013a-135">In hello results panel, select **Aravo**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1013a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1013a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1013a-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Aravo in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1013a-138">In this section, you configure and test Azure AD single sign-on with Aravo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1013a-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Aravo è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1013a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aravo is tooa user in Azure AD.</span></span> <span data-ttu-id="1013a-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Aravo deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1013a-140">In other words, a link relationship between an Azure AD user and hello related user in Aravo needs toobe established.</span></span>

<span data-ttu-id="1013a-141">In Aravo, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1013a-141">In Aravo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1013a-142">tooconfigure e prova AD Azure single sign-on con Aravo, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1013a-142">tooconfigure and test Azure AD single sign-on with Aravo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1013a-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1013a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1013a-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1013a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1013a-145">**[Creazione di un utente test Aravo](#creating-an-aravo-test-user)**  -toohave un equivalente di Britta Simon in Aravo che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1013a-145">**[Creating an Aravo test user](#creating-an-aravo-test-user)** - toohave a counterpart of Britta Simon in Aravo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1013a-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1013a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1013a-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1013a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1013a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1013a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1013a-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Aravo.</span><span class="sxs-lookup"><span data-stu-id="1013a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aravo application.</span></span>

<span data-ttu-id="1013a-150">**Azure AD tooconfigure single sign-on con Aravo, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1013a-150">**tooconfigure Azure AD single sign-on with Aravo, perform hello following steps:**</span></span>

1. <span data-ttu-id="1013a-151">Nel portale di Azure su hello hello **Aravo** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1013a-151">In hello Azure portal, on hello **Aravo** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1013a-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1013a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_samlbase.png)

3. <span data-ttu-id="1013a-155">In hello **Aravo dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1013a-155">On hello **Aravo Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_url.png)

    <span data-ttu-id="1013a-157">a.</span><span class="sxs-lookup"><span data-stu-id="1013a-157">a.</span></span> <span data-ttu-id="1013a-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.aravo.com`</span><span class="sxs-lookup"><span data-stu-id="1013a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aravo.com`</span></span>

    <span data-ttu-id="1013a-159">b.</span><span class="sxs-lookup"><span data-stu-id="1013a-159">b.</span></span> <span data-ttu-id="1013a-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.aravo.com/aems/login.do`</span><span class="sxs-lookup"><span data-stu-id="1013a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.aravo.com/aems/login.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1013a-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="1013a-161">These values are not real.</span></span> <span data-ttu-id="1013a-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="1013a-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="1013a-163">Contatto [team di supporto Aravo](http://www.aravo.com/about-us/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="1013a-163">Contact [Aravo support team](http://www.aravo.com/about-us/contact/) tooget these values.</span></span>
 
4. <span data-ttu-id="1013a-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1013a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_certificate.png) 

5. <span data-ttu-id="1013a-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1013a-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-aravo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1013a-168">In hello **Aravo configurazione** fare clic su **configurare Aravo** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="1013a-168">On hello **Aravo Configuration** section, click **Configure Aravo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1013a-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1013a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_configure.png) 

7. <span data-ttu-id="1013a-171">tooconfigure single sign-on sul **Aravo** lato, è necessario hello toosend scaricato **certificato (Base64)**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL**troppo[team di supporto Aravo](http://www.aravo.com/about-us/contact/).</span><span class="sxs-lookup"><span data-stu-id="1013a-171">tooconfigure single sign-on on **Aravo** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Aravo support team](http://www.aravo.com/about-us/contact/).</span></span> 


> [!TIP]
> <span data-ttu-id="1013a-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1013a-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1013a-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1013a-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1013a-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1013a-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1013a-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1013a-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="1013a-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1013a-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1013a-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1013a-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1013a-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1013a-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1013a-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1013a-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1013a-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1013a-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1013a-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1013a-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1013a-187">a.</span><span class="sxs-lookup"><span data-stu-id="1013a-187">a.</span></span> <span data-ttu-id="1013a-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1013a-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1013a-189">b.</span><span class="sxs-lookup"><span data-stu-id="1013a-189">b.</span></span> <span data-ttu-id="1013a-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1013a-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1013a-191">c.</span><span class="sxs-lookup"><span data-stu-id="1013a-191">c.</span></span> <span data-ttu-id="1013a-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1013a-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1013a-193">d.</span><span class="sxs-lookup"><span data-stu-id="1013a-193">d.</span></span> <span data-ttu-id="1013a-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1013a-194">Click **Create**.</span></span>
 
### <a name="creating-an-aravo-test-user"></a><span data-ttu-id="1013a-195">Creazione di un utente test Aravo</span><span class="sxs-lookup"><span data-stu-id="1013a-195">Creating an Aravo test user</span></span>

<span data-ttu-id="1013a-196">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Aravo toocreate.</span><span class="sxs-lookup"><span data-stu-id="1013a-196">hello objective of this section is toocreate a user called Britta Simon in Aravo.</span></span> <span data-ttu-id="1013a-197">Lavorare con [team di supporto Aravo](http://www.aravo.com/about-us/contact/) tooadd utenti hello hello Aravo account.</span><span class="sxs-lookup"><span data-stu-id="1013a-197">Work with [Aravo support team](http://www.aravo.com/about-us/contact/) tooadd hello users in hello Aravo account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1013a-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1013a-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1013a-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAravo.</span><span class="sxs-lookup"><span data-stu-id="1013a-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAravo.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1013a-201">**tooassign Britta Simon tooAravo, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1013a-201">**tooassign Britta Simon tooAravo, perform hello following steps:**</span></span>

1. <span data-ttu-id="1013a-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1013a-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1013a-204">Nell'elenco di applicazioni hello, selezionare **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="1013a-204">In hello applications list, select **Aravo**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_app.png) 

3. <span data-ttu-id="1013a-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1013a-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1013a-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1013a-208">Click **Add** button.</span></span> <span data-ttu-id="1013a-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1013a-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1013a-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1013a-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1013a-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1013a-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1013a-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1013a-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1013a-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1013a-214">Testing single sign-on</span></span>

<span data-ttu-id="1013a-215">obiettivo di Hello di questa sezione è tootest il servizio Microsoft Azure AD Single Sign-On configuration utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1013a-215">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="1013a-216">Quando si fa clic su riquadro Aravo hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Aravo applicazione.</span><span class="sxs-lookup"><span data-stu-id="1013a-216">When you click hello Aravo tile in hello Access Panel, you should get automatically signed-on tooyour Aravo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1013a-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1013a-217">Additional resources</span></span>

* [<span data-ttu-id="1013a-218">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1013a-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1013a-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1013a-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_203.png

