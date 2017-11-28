---
title: 'Esercitazione: Integrazione di Azure Active Directory con FreshGrade | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e FreshGrade.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2fe7cedd45290945ec5624453a9675abdd7726d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="47fd6-103">Esercitazione: Integrazione di Azure Active Directory con FreshGrade</span><span class="sxs-lookup"><span data-stu-id="47fd6-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="47fd6-104">In questa esercitazione, è illustrato come toointegrate FreshGrade con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47fd6-104">In this tutorial, you learn how toointegrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47fd6-105">Integrazione FreshGrade con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="47fd6-105">Integrating FreshGrade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="47fd6-106">È possibile controllare in Azure AD che ha accesso tooFreshGrade</span><span class="sxs-lookup"><span data-stu-id="47fd6-106">You can control in Azure AD who has access tooFreshGrade</span></span>
- <span data-ttu-id="47fd6-107">È possibile abilitare l'utenti tooautomatically get connesso tooFreshGrade (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="47fd6-107">You can enable your users tooautomatically get signed-on tooFreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="47fd6-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="47fd6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="47fd6-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47fd6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47fd6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="47fd6-110">Prerequisites</span></span>

<span data-ttu-id="47fd6-111">integrazione di Azure AD con FreshGrade tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="47fd6-111">tooconfigure Azure AD integration with FreshGrade, you need hello following items:</span></span>

- <span data-ttu-id="47fd6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47fd6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47fd6-113">Sottoscrizione di FreshGrade abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="47fd6-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="47fd6-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="47fd6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47fd6-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="47fd6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47fd6-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="47fd6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47fd6-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47fd6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47fd6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="47fd6-118">Scenario description</span></span>
<span data-ttu-id="47fd6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="47fd6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47fd6-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="47fd6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47fd6-121">Aggiunta di FreshGrade dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="47fd6-121">Adding FreshGrade from hello gallery</span></span>
2. <span data-ttu-id="47fd6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47fd6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-hello-gallery"></a><span data-ttu-id="47fd6-123">Aggiunta di FreshGrade dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="47fd6-123">Adding FreshGrade from hello gallery</span></span>
<span data-ttu-id="47fd6-124">integrazione hello tooconfigure di FreshGrade in Azure AD, è necessario tooadd FreshGrade dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="47fd6-124">tooconfigure hello integration of FreshGrade into Azure AD, you need tooadd FreshGrade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="47fd6-125">**tooadd FreshGrade dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47fd6-125">**tooadd FreshGrade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="47fd6-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="47fd6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="47fd6-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="47fd6-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="47fd6-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="47fd6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="47fd6-133">Nella casella di ricerca hello, digitare **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-133">In hello search box, type **FreshGrade**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="47fd6-135">Nel riquadro dei risultati hello, selezionare **FreshGrade**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="47fd6-135">In hello results panel, select **FreshGrade**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="47fd6-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47fd6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="47fd6-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FreshGrade in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="47fd6-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="47fd6-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in FreshGrade è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47fd6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshGrade is tooa user in Azure AD.</span></span> <span data-ttu-id="47fd6-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in FreshGrade deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="47fd6-140">In other words, a link relationship between an Azure AD user and hello related user in FreshGrade needs toobe established.</span></span>

<span data-ttu-id="47fd6-141">In FreshGrade, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="47fd6-141">In FreshGrade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="47fd6-142">tooconfigure e prova AD Azure single sign-on con FreshGrade, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="47fd6-142">tooconfigure and test Azure AD single sign-on with FreshGrade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="47fd6-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="47fd6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="47fd6-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47fd6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47fd6-145">**[Creazione di un utente test FreshGrade](#creating-a-freshgrade-test-user)**  -toohave un equivalente di Britta Simon in FreshGrade che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="47fd6-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - toohave a counterpart of Britta Simon in FreshGrade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="47fd6-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="47fd6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47fd6-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="47fd6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="47fd6-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47fd6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="47fd6-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="47fd6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="47fd6-150">**Azure AD tooconfigure single sign-on con FreshGrade, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47fd6-150">**tooconfigure Azure AD single sign-on with FreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="47fd6-151">Nel portale di Azure su hello hello **FreshGrade** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-151">In hello Azure portal, on hello **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="47fd6-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="47fd6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="47fd6-155">In hello **FreshGrade dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47fd6-155">On hello **FreshGrade Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="47fd6-157">a.</span><span class="sxs-lookup"><span data-stu-id="47fd6-157">a.</span></span> <span data-ttu-id="47fd6-158">In hello **Sign-on URL** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="47fd6-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="47fd6-159">b.</span><span class="sxs-lookup"><span data-stu-id="47fd6-159">b.</span></span> <span data-ttu-id="47fd6-160">In hello **identificatore** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="47fd6-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="47fd6-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="47fd6-161">These values are not real.</span></span> <span data-ttu-id="47fd6-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="47fd6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="47fd6-163">Contatto [team di supporto FreshGrade Client](mailTo:support@freshgrade.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="47fd6-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="47fd6-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="47fd6-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="47fd6-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="47fd6-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="47fd6-168">In hello **FreshGrade configurazione** fare clic su **configurare FreshGrade** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="47fd6-168">On hello **FreshGrade Configuration** section, click **Configure FreshGrade** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="47fd6-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="47fd6-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="47fd6-171">hello toogenerate **metadati** url, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47fd6-171">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="47fd6-172">a.</span><span class="sxs-lookup"><span data-stu-id="47fd6-172">a.</span></span> <span data-ttu-id="47fd6-173">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-173">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="47fd6-175">b.</span><span class="sxs-lookup"><span data-stu-id="47fd6-175">b.</span></span> <span data-ttu-id="47fd6-176">Fare clic su **endpoint** tooopen **endpoint** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="47fd6-176">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="47fd6-178">c.</span><span class="sxs-lookup"><span data-stu-id="47fd6-178">c.</span></span> <span data-ttu-id="47fd6-179">Fare clic su hello copia pulsante toocopy **documento metadati federazione** url e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="47fd6-179">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="47fd6-181">d.</span><span class="sxs-lookup"><span data-stu-id="47fd6-181">d.</span></span> <span data-ttu-id="47fd6-182">Ora passare pagina delle proprietà toohello **FreshGrade** e hello copia **Id applicazione** utilizzando **copia** pulsante e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="47fd6-182">Now go toohello property page of **FreshGrade** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="47fd6-184">e.</span><span class="sxs-lookup"><span data-stu-id="47fd6-184">e.</span></span> <span data-ttu-id="47fd6-185">Generare hello **URL dei metadati** utilizzando hello seguente motivo:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="47fd6-185">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="47fd6-186">tooconfigure single sign-on sul **FreshGrade** lato, è necessario hello toosend **URL dei metadati** e **SAML Single Sign-On Service URL** troppo[FreshGrade team di supporto](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="47fd6-186">tooconfigure single sign-on on **FreshGrade** side, you need toosend hello **Metadata URL** and **SAML Single Sign-On Service URL** too[FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="47fd6-187">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="47fd6-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="47fd6-188">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="47fd6-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="47fd6-189">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="47fd6-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="47fd6-190">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="47fd6-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="47fd6-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47fd6-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="47fd6-192">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="47fd6-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="47fd6-194">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47fd6-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="47fd6-195">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="47fd6-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="47fd6-197">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="47fd6-199">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="47fd6-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="47fd6-201">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47fd6-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="47fd6-203">a.</span><span class="sxs-lookup"><span data-stu-id="47fd6-203">a.</span></span> <span data-ttu-id="47fd6-204">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="47fd6-205">b.</span><span class="sxs-lookup"><span data-stu-id="47fd6-205">b.</span></span> <span data-ttu-id="47fd6-206">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="47fd6-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="47fd6-207">c.</span><span class="sxs-lookup"><span data-stu-id="47fd6-207">c.</span></span> <span data-ttu-id="47fd6-208">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="47fd6-209">d.</span><span class="sxs-lookup"><span data-stu-id="47fd6-209">d.</span></span> <span data-ttu-id="47fd6-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="47fd6-211">Creazione di un utente test di FreshGrade</span><span class="sxs-lookup"><span data-stu-id="47fd6-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="47fd6-212">In questa sezione viene creato un utente chiamato Britta Simon in FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="47fd6-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="47fd6-213">Rivolgersi [team di supporto FreshGrade](mailTo:support@freshgrade.com) utenti hello tooadd nella piattaforma FreshGrade hello.</span><span class="sxs-lookup"><span data-stu-id="47fd6-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) tooadd hello users in hello FreshGrade platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="47fd6-214">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="47fd6-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="47fd6-215">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooFreshGrade.</span><span class="sxs-lookup"><span data-stu-id="47fd6-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFreshGrade.</span></span>

![Assegna utente][200] 

<span data-ttu-id="47fd6-217">**tooassign Britta Simon tooFreshGrade, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47fd6-217">**tooassign Britta Simon tooFreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="47fd6-218">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="47fd6-220">Nell'elenco di applicazioni hello, selezionare **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-220">In hello applications list, select **FreshGrade**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="47fd6-222">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="47fd6-224">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-224">Click **Add** button.</span></span> <span data-ttu-id="47fd6-225">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="47fd6-227">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="47fd6-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="47fd6-228">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47fd6-229">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="47fd6-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="47fd6-230">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="47fd6-230">Testing single sign-on</span></span>

<span data-ttu-id="47fd6-231">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="47fd6-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="47fd6-232">Quando si fa clic su riquadro FreshGrade hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour FreshGrade applicazione.</span><span class="sxs-lookup"><span data-stu-id="47fd6-232">When you click hello FreshGrade tile in hello Access Panel, you should get automatically signed-on tooyour FreshGrade application.</span></span>
<span data-ttu-id="47fd6-233">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47fd6-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="47fd6-234">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="47fd6-234">Additional resources</span></span>

* [<span data-ttu-id="47fd6-235">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47fd6-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47fd6-236">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47fd6-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

