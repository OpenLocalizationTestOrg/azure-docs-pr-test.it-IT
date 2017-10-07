---
title: 'Esercitazione: Integrazione di Azure Active Directory con 8x8 Virtual Office | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Office virtuale 8 x 8.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: df5c5de77285cd3912b68cc3b1e3eee274aa951c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="045bb-103">Esercitazione: Integrazione di Azure Active Directory con 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="045bb-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="045bb-104">In questa esercitazione, è illustrato come toointegrate 8x8 Office virtuale con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="045bb-104">In this tutorial, you learn how toointegrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="045bb-105">L'integrazione di 8 x 8 Office virtuale con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="045bb-105">Integrating 8x8 Virtual Office with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="045bb-106">È possibile controllare in Azure AD che ha accesso too8x8 Office virtuale</span><span class="sxs-lookup"><span data-stu-id="045bb-106">You can control in Azure AD who has access too8x8 Virtual Office</span></span>
- <span data-ttu-id="045bb-107">È possibile consentire agli utenti di ottenere tooautomatically firmato-on too8x8 Office virtuale (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="045bb-107">You can enable your users tooautomatically get signed-on too8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="045bb-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="045bb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="045bb-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="045bb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="045bb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="045bb-110">Prerequisites</span></span>

<span data-ttu-id="045bb-111">integrazione di Azure AD con 8 x 8 virtuali Office tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="045bb-111">tooconfigure Azure AD integration with 8x8 Virtual Office, you need hello following items:</span></span>

- <span data-ttu-id="045bb-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="045bb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="045bb-113">Sottoscrizione di 8x8 Virtual Office abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="045bb-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="045bb-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="045bb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="045bb-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="045bb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="045bb-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="045bb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="045bb-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="045bb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="045bb-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="045bb-118">Scenario description</span></span>
<span data-ttu-id="045bb-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="045bb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="045bb-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="045bb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="045bb-121">Aggiunta di 8 x 8 virtuali Office dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="045bb-121">Adding 8x8 Virtual Office from hello gallery</span></span>
2. <span data-ttu-id="045bb-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="045bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-hello-gallery"></a><span data-ttu-id="045bb-123">Aggiunta di 8 x 8 virtuali Office dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="045bb-123">Adding 8x8 Virtual Office from hello gallery</span></span>
<span data-ttu-id="045bb-124">integrazione hello tooconfigure di Office di 8 x 8 virtuali in Azure AD, è necessario tooadd 8x8 Office virtuale dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="045bb-124">tooconfigure hello integration of 8x8 Virtual Office into Azure AD, you need tooadd 8x8 Virtual Office from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="045bb-125">**eseguire Office virtuale dalla raccolta di hello, tooadd 8 x 8 hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="045bb-125">**tooadd 8x8 Virtual Office from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="045bb-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="045bb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="045bb-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="045bb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="045bb-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="045bb-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="045bb-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="045bb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="045bb-133">Nella casella di ricerca hello, digitare **8 x 8 virtuali Office**.</span><span class="sxs-lookup"><span data-stu-id="045bb-133">In hello search box, type **8x8 Virtual Office**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="045bb-135">Nel riquadro dei risultati hello, selezionare **8 x 8 virtuali Office**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="045bb-135">In hello results panel, select **8x8 Virtual Office**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="045bb-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="045bb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="045bb-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 8x8 Virtual Office mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="045bb-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="045bb-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Office virtuale 8 x 8 è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="045bb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 8x8 Virtual Office is tooa user in Azure AD.</span></span> <span data-ttu-id="045bb-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in 8 x 8 Office virtuale richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="045bb-140">In other words, a link relationship between an Azure AD user and hello related user in 8x8 Virtual Office needs toobe established.</span></span>

<span data-ttu-id="045bb-141">In Office virtuale 8 x 8, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="045bb-141">In 8x8 Virtual Office, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="045bb-142">tooconfigure e prova AD Azure single sign-on con 8 x 8 virtuali Office, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="045bb-142">tooconfigure and test Azure AD single sign-on with 8x8 Virtual Office, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="045bb-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="045bb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="045bb-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="045bb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="045bb-145">**[Creazione di un utente di prova di Office virtuale 8 x 8](#creating-a-8x8-virtual-office-test-user)**  -toohave un equivalente di Britta Simon 8 x 8 virtuali Office che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="045bb-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - toohave a counterpart of Britta Simon in 8x8 Virtual Office that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="045bb-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="045bb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="045bb-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="045bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="045bb-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="045bb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="045bb-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Office virtuale 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="045bb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="045bb-150">**tooconfigure AD Azure single sign-on con 8 x 8 virtuali Office, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="045bb-150">**tooconfigure Azure AD single sign-on with 8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="045bb-151">Nel portale di Azure su hello hello **8 x 8 virtuali Office** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="045bb-151">In hello Azure portal, on hello **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="045bb-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="045bb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="045bb-155">In hello **URL e dominio virtuale 8 x 8** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="045bb-155">On hello **8x8 Virtual Office Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="045bb-157">a.</span><span class="sxs-lookup"><span data-stu-id="045bb-157">a.</span></span> <span data-ttu-id="045bb-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="045bb-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="045bb-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="045bb-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="045bb-160">b.</span><span class="sxs-lookup"><span data-stu-id="045bb-160">b.</span></span> <span data-ttu-id="045bb-161">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="045bb-161">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="045bb-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="045bb-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="045bb-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="045bb-163">These values are not real.</span></span> <span data-ttu-id="045bb-164">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="045bb-164">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="045bb-165">Contatto [team di supporto Office virtuale 8 x 8](https://www.8x8.com/about-us/contact-us) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="045bb-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) tooget these values.</span></span>
 


4. <span data-ttu-id="045bb-166">In hello **certificato di firma SAML** fare clic su **certificato (Raw)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="045bb-166">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="045bb-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="045bb-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="045bb-170">In hello **8 x 8 virtuali Office configurazione** fare clic su **Office virtuale Configura 8 x 8** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="045bb-170">On hello **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="045bb-171">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="045bb-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="045bb-173">Tenant di Office virtuale Sign-on tooyour 8 x 8 come amministratore.</span><span class="sxs-lookup"><span data-stu-id="045bb-173">Sign-on tooyour 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="045bb-174">Selezionare **Virtual Office Account Mgr** (Account manager di Virtual Office) nel pannello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="045bb-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="045bb-176">Selezionare **Business** toomanage dell'account e fare clic su **Accedi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="045bb-176">Select **Business** account toomanage and click **Sign In** button.</span></span>
   
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="045bb-178">Fare clic su **account** hello menu elenco della scheda.</span><span class="sxs-lookup"><span data-stu-id="045bb-178">Click **Accounts** tab in hello menu list.</span></span>
   
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="045bb-180">Fare clic su **Single Sign-On** nell'elenco di hello degli account.</span><span class="sxs-lookup"><span data-stu-id="045bb-180">Click **Single Sign On** in hello list of Accounts.</span></span>
   
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="045bb-182">Selezionare **Single Sign-On** nel metodo di autenticazione e fare clic su **SAML**.</span><span class="sxs-lookup"><span data-stu-id="045bb-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="045bb-184">Copia **URL SSO SAML**, **Single Sign-Out URL del servizio** e **URL autorità di certificazione** da Azure AD troppo**Sign In URL**, **URL di disconnessione**  e **URL autorità di certificazione** in ufficio virtuale 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="045bb-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD too**Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Configurazione sul lato app](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="045bb-186">Fare clic su **Browser** pulsante certificato hello tooupload scaricato da Azure AD e fare clic su hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="045bb-186">Click **Browser** button tooupload hello certificate which you downloaded from Azure AD, and click hello **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="045bb-187">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="045bb-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="045bb-188">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="045bb-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="045bb-189">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="045bb-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="045bb-190">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="045bb-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="045bb-191">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="045bb-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="045bb-193">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="045bb-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="045bb-194">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="045bb-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="045bb-196">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="045bb-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="045bb-198">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="045bb-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="045bb-200">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="045bb-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="045bb-202">a.</span><span class="sxs-lookup"><span data-stu-id="045bb-202">a.</span></span> <span data-ttu-id="045bb-203">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="045bb-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="045bb-204">b.</span><span class="sxs-lookup"><span data-stu-id="045bb-204">b.</span></span> <span data-ttu-id="045bb-205">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="045bb-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="045bb-206">c.</span><span class="sxs-lookup"><span data-stu-id="045bb-206">c.</span></span> <span data-ttu-id="045bb-207">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="045bb-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="045bb-208">d.</span><span class="sxs-lookup"><span data-stu-id="045bb-208">d.</span></span> <span data-ttu-id="045bb-209">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="045bb-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="045bb-210">Creazione di un utente test di 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="045bb-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="045bb-211">obiettivo di Hello di questa sezione è un utente denominato Britta Simon 8 x 8 virtuali Office toocreate.</span><span class="sxs-lookup"><span data-stu-id="045bb-211">hello objective of this section is toocreate a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="045bb-212">8x8 Virtual Office supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="045bb-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="045bb-213">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="045bb-213">There is no action item for you in this section.</span></span> <span data-ttu-id="045bb-214">Un nuovo utente viene creato durante un tooaccess tentativo 8 x 8 Office virtuale se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="045bb-214">A new user is created during an attempt tooaccess 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="045bb-215">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto Office virtuale 8 x 8](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="045bb-215">If you need toocreate a user manually, you need toocontact hello [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="045bb-216">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="045bb-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="045bb-217">In questa sezione, si abilita Britta Simon toouse single sign-on Azure tramite la concessione di accesso too8x8 virtuale Office.</span><span class="sxs-lookup"><span data-stu-id="045bb-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too8x8 Virtual Office.</span></span>

![Assegna utente][200] 

<span data-ttu-id="045bb-219">**tooassign Britta Simon too8x8 virtuale Office, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="045bb-219">**tooassign Britta Simon too8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="045bb-220">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="045bb-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="045bb-222">Nell'elenco di applicazioni hello, selezionare **8 x 8 virtuali Office**.</span><span class="sxs-lookup"><span data-stu-id="045bb-222">In hello applications list, select **8x8 Virtual Office**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="045bb-224">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="045bb-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="045bb-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="045bb-226">Click **Add** button.</span></span> <span data-ttu-id="045bb-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="045bb-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="045bb-229">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="045bb-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="045bb-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="045bb-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="045bb-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="045bb-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="045bb-232">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="045bb-232">Testing single sign-on</span></span>

<span data-ttu-id="045bb-233">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="045bb-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="045bb-234">Quando si fa clic su riquadro Office virtuale hello 8 x 8 nel Pannello di accesso hello, è necessario ottenere l'applicazione di Office virtuale tooyour automaticamente firmato in 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="045bb-234">When you click hello 8x8 Virtual Office tile in hello Access Panel, you should get automatically signed-on tooyour 8x8 Virtual Office application.</span></span>
<span data-ttu-id="045bb-235">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="045bb-235">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="045bb-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="045bb-236">Additional resources</span></span>

* [<span data-ttu-id="045bb-237">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="045bb-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="045bb-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="045bb-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

