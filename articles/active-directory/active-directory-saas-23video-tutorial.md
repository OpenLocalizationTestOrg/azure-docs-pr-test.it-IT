---
title: 'Esercitazione: Integrazione di Azure Active Directory con 23 Video | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e 23 Video.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 3430e4db3cd1114db62233e6699618071a3646ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="1eae1-103">Esercitazione: Integrazione di Azure Active Directory con 23 Video</span><span class="sxs-lookup"><span data-stu-id="1eae1-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="1eae1-104">In questa esercitazione, è illustrato come toointegrate 23 Video con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1eae1-104">In this tutorial, you learn how toointegrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1eae1-105">L'integrazione 23 Video con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1eae1-105">Integrating 23 Video with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1eae1-106">È possibile controllare in Azure AD che ha accesso too23 Video</span><span class="sxs-lookup"><span data-stu-id="1eae1-106">You can control in Azure AD who has access too23 Video</span></span>
- <span data-ttu-id="1eae1-107">È possibile consentire agli utenti di ottenere tooautomatically firmato on too23 Video (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eae1-107">You can enable your users tooautomatically get signed-on too23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1eae1-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1eae1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1eae1-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1eae1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1eae1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1eae1-110">Prerequisites</span></span>

<span data-ttu-id="1eae1-111">integrazione di Azure AD con Video 23 tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1eae1-111">tooconfigure Azure AD integration with 23 Video, you need hello following items:</span></span>

- <span data-ttu-id="1eae1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1eae1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1eae1-113">Sottoscrizione di 23 Video abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1eae1-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1eae1-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1eae1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1eae1-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1eae1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1eae1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1eae1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1eae1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1eae1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1eae1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1eae1-118">Scenario description</span></span>
<span data-ttu-id="1eae1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1eae1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1eae1-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1eae1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1eae1-121">Aggiunta di Video 23 dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1eae1-121">Adding 23 Video from hello gallery</span></span>
2. <span data-ttu-id="1eae1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eae1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-hello-gallery"></a><span data-ttu-id="1eae1-123">Aggiunta di Video 23 dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1eae1-123">Adding 23 Video from hello gallery</span></span>
<span data-ttu-id="1eae1-124">integrazione hello tooconfigure di Video 23 in Azure AD, è necessario tooadd 23 Video dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1eae1-124">tooconfigure hello integration of 23 Video into Azure AD, you need tooadd 23 Video from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1eae1-125">**eseguire Video dalla raccolta di hello, tooadd 23 hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="1eae1-125">**tooadd 23 Video from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1eae1-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1eae1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1eae1-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1eae1-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1eae1-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1eae1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1eae1-133">Nella casella di ricerca hello, digitare **Video 23**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-133">In hello search box, type **23 Video**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="1eae1-135">Nel riquadro dei risultati hello, selezionare **Video 23**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1eae1-135">In hello results panel, select **23 Video**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1eae1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eae1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1eae1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 23 Video con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1eae1-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1eae1-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in 23 Video è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1eae1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 23 Video is tooa user in Azure AD.</span></span> <span data-ttu-id="1eae1-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello 23 Video deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1eae1-140">In other words, a link relationship between an Azure AD user and hello related user in 23 Video needs toobe established.</span></span>

<span data-ttu-id="1eae1-141">Nel Video 23, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1eae1-141">In 23 Video, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1eae1-142">tooconfigure e prova AD Azure single sign-on con 23 Video, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1eae1-142">tooconfigure and test Azure AD single sign-on with 23 Video, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1eae1-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1eae1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1eae1-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1eae1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1eae1-145">**[Creazione di un utente di test Video 23](#creating-a-23-video-test-user)**  -toohave un equivalente di Britta Simon 23 video che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1eae1-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - toohave a counterpart of Britta Simon in 23 Video that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1eae1-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1eae1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1eae1-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1eae1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1eae1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eae1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1eae1-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Video 23.</span><span class="sxs-lookup"><span data-stu-id="1eae1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="1eae1-150">**Azure AD tooconfigure single sign-on con 23 Video, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1eae1-150">**tooconfigure Azure AD single sign-on with 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="1eae1-151">Nel portale di Azure su hello hello **Video 23** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-151">In hello Azure portal, on hello **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1eae1-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1eae1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="1eae1-155">In hello **23 Video dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1eae1-155">On hello **23 Video Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="1eae1-157">a.</span><span class="sxs-lookup"><span data-stu-id="1eae1-157">a.</span></span> <span data-ttu-id="1eae1-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="1eae1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="1eae1-159">b.</span><span class="sxs-lookup"><span data-stu-id="1eae1-159">b.</span></span> <span data-ttu-id="1eae1-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="1eae1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1eae1-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="1eae1-161">These values are not real.</span></span> <span data-ttu-id="1eae1-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="1eae1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1eae1-163">Contatto [team di supporto Client Video 23](mailto:support@23company.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="1eae1-163">Contact [23 Video Client support team](mailto:support@23company.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="1eae1-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1eae1-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="1eae1-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1eae1-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1eae1-168">In hello **configurazione Video 23** fare clic su **configurare Video 23** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="1eae1-168">On hello **23 Video Configuration** section, click **Configure 23 Video** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1eae1-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1eae1-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="1eae1-171">tooconfigure single sign-on sul **Video 23** lato, è necessario hello toosend scaricato **certificato (Base64)**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL**troppo[23 team di supporto Video](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="1eae1-171">tooconfigure single sign-on on **23 Video** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="1eae1-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1eae1-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1eae1-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1eae1-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1eae1-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1eae1-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1eae1-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eae1-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="1eae1-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1eae1-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1eae1-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1eae1-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1eae1-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1eae1-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1eae1-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1eae1-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1eae1-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1eae1-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1eae1-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1eae1-187">a.</span><span class="sxs-lookup"><span data-stu-id="1eae1-187">a.</span></span> <span data-ttu-id="1eae1-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1eae1-189">b.</span><span class="sxs-lookup"><span data-stu-id="1eae1-189">b.</span></span> <span data-ttu-id="1eae1-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1eae1-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1eae1-191">c.</span><span class="sxs-lookup"><span data-stu-id="1eae1-191">c.</span></span> <span data-ttu-id="1eae1-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1eae1-193">d.</span><span class="sxs-lookup"><span data-stu-id="1eae1-193">d.</span></span> <span data-ttu-id="1eae1-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="1eae1-195">Creazione di un utente di test di 23 Video</span><span class="sxs-lookup"><span data-stu-id="1eae1-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="1eae1-196">obiettivo di Hello di questa sezione è un utente denominato Britta Simon video 23 toocreate.</span><span class="sxs-lookup"><span data-stu-id="1eae1-196">hello objective of this section is toocreate a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="1eae1-197">**un utente denominato Britta Simon in 23 Video toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1eae1-197">**toocreate a user called Britta Simon in 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="1eae1-198">Accesso tooyour 23 sito della società di Video come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1eae1-198">Sign on tooyour 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="1eae1-199">Andare troppo**impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-199">Go too**Settings**.</span></span>
 
3. <span data-ttu-id="1eae1-200">Nella sezione **Users** (Utenti) fare clic su **Configure** (Configura).</span><span class="sxs-lookup"><span data-stu-id="1eae1-200">In **Users** section, click **Configure**.</span></span>
   
    ![Assegna utente][400]

4. <span data-ttu-id="1eae1-202">Fare clic su **Aggiungi nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-202">Click **Add a new user**.</span></span> 
   
    ![Assegna utente][401]

5. <span data-ttu-id="1eae1-204">In hello **invitare altri utenti toojoin questo sito** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1eae1-204">In hello **Invite someone toojoin this site** section, perform hello following steps:</span></span>
   
    ![Assegna utente][402]

    <span data-ttu-id="1eae1-206">a.</span><span class="sxs-lookup"><span data-stu-id="1eae1-206">a.</span></span> <span data-ttu-id="1eae1-207">In hello **indirizzi di posta elettronica** casella di testo, digitare l'indirizzo di posta elettronica Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1eae1-207">In hello **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="1eae1-208">b.</span><span class="sxs-lookup"><span data-stu-id="1eae1-208">b.</span></span> <span data-ttu-id="1eae1-209">Fare clic su **Aggiungi utente hello**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-209">Click **Add hello user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1eae1-210">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eae1-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1eae1-211">In questa sezione, si abilita Britta Simon toouse single sign-on Azure tramite la concessione di accesso too23 Video.</span><span class="sxs-lookup"><span data-stu-id="1eae1-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too23 Video.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1eae1-213">**tooassign Britta Simon too23 Video, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1eae1-213">**tooassign Britta Simon too23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="1eae1-214">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1eae1-216">Nell'elenco di applicazioni hello, selezionare **Video 23**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-216">In hello applications list, select **23 Video**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="1eae1-218">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1eae1-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-220">Click **Add** button.</span></span> <span data-ttu-id="1eae1-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1eae1-223">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1eae1-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1eae1-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1eae1-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1eae1-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1eae1-226">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1eae1-226">Testing single sign-on</span></span>

<span data-ttu-id="1eae1-227">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1eae1-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="1eae1-228">Quando si fa clic su riquadro Video hello 23 in hello Pannello di accesso, è necessario ottenere applicazioni Video tooyour automaticamente firmato in 23.</span><span class="sxs-lookup"><span data-stu-id="1eae1-228">When you click hello 23 Video tile in hello Access Panel, you should get automatically signed-on tooyour 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1eae1-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1eae1-229">Additional resources</span></span>

* [<span data-ttu-id="1eae1-230">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eae1-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1eae1-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eae1-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
