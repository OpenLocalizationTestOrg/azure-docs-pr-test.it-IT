---
title: 'Esercitazione: Integrazione di Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e servizio di sicurezza Web Symantec (WSS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: f4575e6f5eb63cd0e1d63edd35e30be3cacc3382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="6f947-103">Esercitazione: Integrazione di Azure Active Directory con Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="6f947-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="6f947-104">In questa esercitazione, è illustrato come toointegrate Symantec Web Security Service (WSS) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f947-104">In this tutorial, you learn how toointegrate Symantec Web Security Service (WSS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f947-105">Integrazione del servizio di sicurezza Web Symantec (WSS) con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="6f947-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6f947-106">È possibile controllare in Azure AD che ha accesso tooSymantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="6f947-106">You can control in Azure AD who has access tooSymantec Web Security Service (WSS)</span></span>
- <span data-ttu-id="6f947-107">È possibile abilitare l'utenti tooautomatically get connesso tooSymantec Web Security Service (WSS) (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f947-107">You can enable your users tooautomatically get signed-on tooSymantec Web Security Service (WSS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f947-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6f947-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6f947-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f947-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f947-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6f947-110">Prerequisites</span></span>

<span data-ttu-id="6f947-111">tooconfigure integrazione di Azure AD con Symantec Web Security Service (WSS), è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6f947-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="6f947-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f947-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f947-113">Una sottoscrizione abilitata per il Single Sign-On di Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="6f947-113">A Symantec Web Security Service (WSS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f947-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6f947-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f947-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="6f947-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f947-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6f947-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f947-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f947-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f947-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6f947-118">Scenario description</span></span>
<span data-ttu-id="6f947-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6f947-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f947-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="6f947-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f947-121">Aggiunta del servizio di sicurezza Web Symantec (WSS) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6f947-121">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
2. <span data-ttu-id="6f947-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f947-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="6f947-123">Aggiunta del servizio di sicurezza Web Symantec (WSS) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6f947-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="6f947-124">integrazione di hello di tooconfigure Symantec Web Security Service (WSS) in Azure AD, è necessario tooadd Symantec Web Security Service (WSS) dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6f947-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6f947-125">**tooadd Symantec Web Security Service (WSS) dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f947-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f947-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6f947-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6f947-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6f947-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6f947-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f947-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6f947-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6f947-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6f947-133">Nella casella di ricerca hello, digitare **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="6f947-133">In hello search box, type **Symantec Web Security Service (WSS)**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. <span data-ttu-id="6f947-135">Nel riquadro dei risultati hello, selezionare **Symantec Web Security Service (WSS)**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6f947-135">In hello results panel, select **Symantec Web Security Service (WSS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6f947-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f947-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6f947-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Symantec Web Security Service (WSS) usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6f947-138">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f947-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello Symantec Web Security Service (WSS) è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f947-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="6f947-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello Symantec Web Security Service (WSS) richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="6f947-140">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="6f947-141">In Symantec Web Security Service (WSS), assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="6f947-141">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6f947-142">tooconfigure e test di Azure AD single sign-on con Symantec Web Security Service (WSS), è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="6f947-142">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6f947-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6f947-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6f947-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f947-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f947-145">**[Creazione di un utente di test del servizio di sicurezza Web Symantec (WSS)](#creating-a-symantec-web-security-service-wss-test-user)**  -toohave un equivalente di Britta Simon in Symantec Web Security Service (WSS) che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6f947-145">**[Creating a Symantec Web Security Service (WSS) test user](#creating-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f947-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6f947-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f947-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6f947-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6f947-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f947-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6f947-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione del servizio di sicurezza Web Symantec (WSS).</span><span class="sxs-lookup"><span data-stu-id="6f947-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="6f947-150">**tooconfigure AD Azure single sign-on con Symantec Web Security Service (WSS), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f947-150">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="6f947-151">Nel portale di Azure su hello hello **Symantec Web Security Service (WSS)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6f947-151">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6f947-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6f947-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="6f947-155">In hello **URL e dominio del servizio (WSS) sicurezza Web Symantec** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f947-155">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="6f947-157">a.</span><span class="sxs-lookup"><span data-stu-id="6f947-157">a.</span></span> <span data-ttu-id="6f947-158">In hello **Sign-on URL** casella menzione hello url, che si desidera tooblock in base a criteri di blocco toohello di hello Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="6f947-158">In hello **Sign-on URL** textbox, mention hello url, which you want tooblock according toohello blocking policy of hello Symantec Web Security Service (WSS).</span></span>  
    
    <span data-ttu-id="6f947-159">b.</span><span class="sxs-lookup"><span data-stu-id="6f947-159">b.</span></span> <span data-ttu-id="6f947-160">In hello **identificatore** casella di testo, digitare l'URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="6f947-160">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6f947-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="6f947-161">These values are not real.</span></span> <span data-ttu-id="6f947-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="6f947-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6f947-163">Contatto [team di supporto Client di servizio di sicurezza Web Symantec (WSS)](https://www.symantec.com/contact-us) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="6f947-163">Contact [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="6f947-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6f947-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="6f947-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6f947-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f947-168">tooconfigure single sign-on sul **Symantec Web Security Service (WSS)** lato, è necessario hello toosend scaricato **Metadata XML** troppo[teamdisupportodiSymantecWebSecurityService(WSS)](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="6f947-168">tooconfigure single sign-on on **Symantec Web Security Service (WSS)** side, you need toosend hello downloaded **Metadata XML** too[Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="6f947-169">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="6f947-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6f947-170">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="6f947-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6f947-171">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f947-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6f947-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f947-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="6f947-173">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6f947-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6f947-175">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f947-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f947-176">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6f947-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f947-178">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6f947-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f947-180">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="6f947-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f947-182">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f947-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f947-184">a.</span><span class="sxs-lookup"><span data-stu-id="6f947-184">a.</span></span> <span data-ttu-id="6f947-185">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f947-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f947-186">b.</span><span class="sxs-lookup"><span data-stu-id="6f947-186">b.</span></span> <span data-ttu-id="6f947-187">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6f947-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f947-188">c.</span><span class="sxs-lookup"><span data-stu-id="6f947-188">c.</span></span> <span data-ttu-id="6f947-189">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="6f947-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6f947-190">d.</span><span class="sxs-lookup"><span data-stu-id="6f947-190">d.</span></span> <span data-ttu-id="6f947-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6f947-191">Click **Create**.</span></span>
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="6f947-192">Creazione di un utente test di Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="6f947-192">Creating a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="6f947-193">In questa sezione viene creato un utente di nome Britta Simon in Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="6f947-193">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="6f947-194">Lavorare con [team di supporto del servizio di sicurezza Web Symantec (WSS)](https://www.symantec.com/contact-us) per aggiungere gli utenti di hello nella piattaforma di hello Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="6f947-194">Work with [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) to add hello users in hello Symantec Web Security Service (WSS) platform.</span></span> <span data-ttu-id="6f947-195">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6f947-195">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="6f947-196">Anche insieme hello dettagli utente è necessario toosend hello indirizzo IP pubblico del computer di hello da cui si sta tentando di un'applicazione hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="6f947-196">Also along with hello user details you need toosend hello public IPaddress of hello machine from which you are trying tooaccess hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="6f947-197">. [Fare clic qui](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget del computer pubblico IPaddress.</span><span class="sxs-lookup"><span data-stu-id="6f947-197">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6f947-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f947-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6f947-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSymantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="6f947-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Assegna utente][200] 

<span data-ttu-id="6f947-201">**tooassign Britta Simon tooSymantec Web Security Service (WSS), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f947-201">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="6f947-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f947-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6f947-204">Nell'elenco di applicazioni hello, selezionare **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="6f947-204">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. <span data-ttu-id="6f947-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6f947-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6f947-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6f947-208">Click **Add** button.</span></span> <span data-ttu-id="6f947-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f947-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6f947-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="6f947-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6f947-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6f947-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f947-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f947-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6f947-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6f947-214">Testing single sign-on</span></span>

<span data-ttu-id="6f947-215">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6f947-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6f947-216">Quando si fa clic su riquadro Symantec Web Security Service (WSS) nel Pannello di accesso hello hello, si ottiene toohello reindirizzato il blocco di pagina per cui è stato configurato hello criteri di blocco.</span><span class="sxs-lookup"><span data-stu-id="6f947-216">When you click hello Symantec Web Security Service (WSS) tile in hello Access Panel, you get redirected toohello blocking page for which hello blocking policy has been configured.</span></span>
<span data-ttu-id="6f947-217">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f947-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f947-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6f947-218">Additional resources</span></span>

* [<span data-ttu-id="6f947-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f947-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f947-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f947-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

