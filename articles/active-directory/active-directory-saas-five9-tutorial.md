---
title: 'Esercitazione: integrazione di Azure Active Directory con Five9 Plus Adapter (CTI, Contact Center Agents) | Microsoft Docs'
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Five9 più Adapter (CTI, agenti di contatto Center)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="8ceb8-103">Esercitazione: integrazione di Azure Active Directory con Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="8ceb8-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="8ceb8-104">In questa esercitazione, è illustrato come toointegrate Five9 più Adapter (CTI, agenti Center contatti) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-104">In this tutorial, you learn how toointegrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ceb8-105">Integrazione Five9 più Adapter (CTI, agenti Center contatti) con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8ceb8-106">È possibile controllare in Azure AD che ha accesso tooFive9 più Adapter (CTI, agenti di contatto Center)</span><span class="sxs-lookup"><span data-stu-id="8ceb8-106">You can control in Azure AD who has access tooFive9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="8ceb8-107">È possibile abilitare le utenti tooautomatically get connesso tooFive9 Plus Adapter (CTI, contattare Center agenti) (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ceb8-107">You can enable your users tooautomatically get signed-on tooFive9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ceb8-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8ceb8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8ceb8-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ceb8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8ceb8-110">Prerequisites</span></span>

<span data-ttu-id="8ceb8-111">integrazione di tooconfigure Azure AD con Five9 più Adapter (CTI, agenti Center contatto), è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-111">tooconfigure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need hello following items:</span></span>

- <span data-ttu-id="8ceb8-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ceb8-113">Sottoscrizione abilitata all'accesso Single Sign-On per Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="8ceb8-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ceb8-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ceb8-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ceb8-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ceb8-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ceb8-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8ceb8-118">Scenario description</span></span>
<span data-ttu-id="8ceb8-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ceb8-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ceb8-121">Aggiunta di Five9 più Adapter (CTI, gli agenti di centro di contatto) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8ceb8-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
2. <span data-ttu-id="8ceb8-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ceb8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a><span data-ttu-id="8ceb8-123">Aggiunta di Five9 più Adapter (CTI, gli agenti di centro di contatto) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8ceb8-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
<span data-ttu-id="8ceb8-124">integrazione hello tooconfigure di Five9 più Adapter (CTI, gli agenti di centro di contatto) in Azure AD, è necessario tooadd Five9 più Adapter (CTI, gli agenti di centro di contatto) dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-124">tooconfigure hello integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8ceb8-125">**tooadd Five9 più Adapter (CTI, gli agenti di centro di contatto) dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ceb8-125">**tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ceb8-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8ceb8-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8ceb8-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8ceb8-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8ceb8-133">Nella casella di ricerca hello, digitare **Five9 più Adapter (CTI, gli agenti di centro di contatto)**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-133">In hello search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="8ceb8-135">Nel riquadro dei risultati hello, selezionare **Five9 più Adapter (CTI, gli agenti di centro di contatto)**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-135">In hello results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ceb8-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ceb8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ceb8-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Five9 Plus Adapter (CTI, Contact Center Agents) in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8ceb8-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ceb8-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Five9 più Adapter (CTI, gli agenti di centro di contatto) è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is tooa user in Azure AD.</span></span> <span data-ttu-id="8ceb8-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlati hello Five9 più Adapter (CTI, contattare Center agenti) deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-140">In other words, a link relationship between an Azure AD user and hello related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs toobe established.</span></span>

<span data-ttu-id="8ceb8-141">In Five9 più Adapter (CTI, agenti Center Contact), assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8ceb8-142">tooconfigure e test Azure single sign-on AD Five9 più adapter (CTI, contattare Center agenti), è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-142">tooconfigure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8ceb8-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8ceb8-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ceb8-145">**[Creazione di un utente test Five9 più Adapter (CTI, gli agenti di centro di contatto)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave un equivalente di Britta Simon Five9 più adapter (CTI, gli agenti di centro di contatto) che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - toohave a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ceb8-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ceb8-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ceb8-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ceb8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ceb8-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Five9 più Adapter (CTI, agenti di contatto Center).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="8ceb8-150">**tooconfigure Azure single sign-on AD Five9 più adapter (CTI, agenti Center Contact), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ceb8-150">**tooconfigure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="8ceb8-151">Nel portale di Azure su hello hello **Five9 più Adapter (CTI, gli agenti di centro di contatto)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-151">In hello Azure portal, on hello **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8ceb8-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="8ceb8-155">In hello **dominio Five9 più Adapter (CTI, contattare Center agenti) e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-155">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="8ceb8-157">a.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-157">a.</span></span> <span data-ttu-id="8ceb8-158">In hello **identificatore** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>

    |    <span data-ttu-id="8ceb8-159">Environment</span><span class="sxs-lookup"><span data-stu-id="8ceb8-159">Environment</span></span>      |       <span data-ttu-id="8ceb8-160">URL</span><span class="sxs-lookup"><span data-stu-id="8ceb8-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="8ceb8-161">Per "Five9 Plus Adapter for Microsoft Dynamics CRM"</span><span class="sxs-lookup"><span data-stu-id="8ceb8-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="8ceb8-162">Per "Five9 Plus Adapter for Zendesk"</span><span class="sxs-lookup"><span data-stu-id="8ceb8-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="8ceb8-163">Per "Five9 Plus Adapter for Agent Desktop Toolkit"</span><span class="sxs-lookup"><span data-stu-id="8ceb8-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="8ceb8-164">b.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-164">b.</span></span> <span data-ttu-id="8ceb8-165">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-165">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    |      <span data-ttu-id="8ceb8-166">Environment</span><span class="sxs-lookup"><span data-stu-id="8ceb8-166">Environment</span></span>     |      <span data-ttu-id="8ceb8-167">URL</span><span class="sxs-lookup"><span data-stu-id="8ceb8-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="8ceb8-168">Per "Five9 Plus Adapter for Microsoft Dynamics CRM"</span><span class="sxs-lookup"><span data-stu-id="8ceb8-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="8ceb8-169">Per "Five9 Plus Adapter for Zendesk"</span><span class="sxs-lookup"><span data-stu-id="8ceb8-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="8ceb8-170">Per "Five9 Plus Adapter for Agent Desktop Toolkit"</span><span class="sxs-lookup"><span data-stu-id="8ceb8-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="8ceb8-171">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-171">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="8ceb8-173">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8ceb8-173">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8ceb8-175">In hello **Five9 più Adapter (CTI, gli agenti di centro di contatto) configurazione** fare clic su **configurare Five9 più Adapter (CTI, gli agenti di centro di contatto)** tooopen **configurasign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-175">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8ceb8-176">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="8ceb8-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="8ceb8-178">tooconfigure single sign-on sul **Five9 più Adapter (CTI, gli agenti di centro di contatto)** lato, è necessario hello toosend scaricato **Certificate(Base64), Sign-Out URL, ID entità SAML e SAML Single Sign-On Service URL** troppo[team di supporto Five9 più Adapter (CTI, gli agenti di centro di contatto)](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-178">tooconfigure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="8ceb8-179">Inoltre, inoltre, per la configurazione di SSO ulteriormente seguire hello in base adapter toohello passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-179">Also additionally, for configuring SSO further please follow hello below steps according toohello adapter:</span></span>

    <span data-ttu-id="8ceb8-180">a.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-180">a.</span></span> <span data-ttu-id="8ceb8-181">Guida dell'amministratore per "Five9 Plus Adapter per Agent Desktop Toolkit": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="8ceb8-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="8ceb8-182">b.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-182">b.</span></span> <span data-ttu-id="8ceb8-183">Guida dell'amministratore per "Five9 Plus Adapter per Microsoft Dynamics CRM": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="8ceb8-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="8ceb8-184">c.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-184">c.</span></span> <span data-ttu-id="8ceb8-185">Guida dell'amministratore per "Five9 Plus Adapter per Zendesk": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="8ceb8-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="8ceb8-186">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8ceb8-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8ceb8-187">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8ceb8-188">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ceb8-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ceb8-189">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ceb8-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ceb8-190">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8ceb8-192">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ceb8-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ceb8-193">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ceb8-195">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ceb8-197">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ceb8-199">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ceb8-201">a.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-201">a.</span></span> <span data-ttu-id="8ceb8-202">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ceb8-203">b.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-203">b.</span></span> <span data-ttu-id="8ceb8-204">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ceb8-205">c.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-205">c.</span></span> <span data-ttu-id="8ceb8-206">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8ceb8-207">d.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-207">d.</span></span> <span data-ttu-id="8ceb8-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="8ceb8-209">Creazione dell'utente test di Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="8ceb8-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="8ceb8-210">In questa sezione si crea un utente chiamato Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="8ceb8-211">Lavorare con [team di supporto Five9 più Adapter (CTI, gli agenti di centro di contatto)](https://www.five9.com/about/contact) per aggiungere gli utenti di hello nella piattaforma di hello Five9 più Adapter (CTI, agenti di contatto Center).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add hello users in hello Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="8ceb8-212">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8ceb8-213">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ceb8-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8ceb8-214">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooFive9 più Adapter (CTI, agenti di contatto Center).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFive9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Assegna utente][200] 

<span data-ttu-id="8ceb8-216">**tooassign Britta Simon tooFive9 più Adapter (CTI, agenti Center Contact), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ceb8-216">**tooassign Britta Simon tooFive9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="8ceb8-217">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8ceb8-219">Nell'elenco di applicazioni hello, selezionare **Five9 più Adapter (CTI, gli agenti di centro di contatto)**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-219">In hello applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="8ceb8-221">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8ceb8-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-223">Click **Add** button.</span></span> <span data-ttu-id="8ceb8-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8ceb8-226">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8ceb8-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ceb8-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ceb8-229">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8ceb8-229">Testing single sign-on</span></span>

<span data-ttu-id="8ceb8-230">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8ceb8-231">Quando si fa clic su riquadro Five9 più Adapter (CTI, gli agenti di centro di contatto) hello in hello Pannello di accesso, è necessario ottenere applicazione Five9 più Adapter (CTI, agenti Center contattare) automaticamente firmato in tooyour.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-231">When you click hello Five9 Plus Adapter (CTI, Contact Center Agents) tile in hello Access Panel, you should get automatically signed-on tooyour Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="8ceb8-232">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-232">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ceb8-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8ceb8-233">Additional resources</span></span>

* [<span data-ttu-id="8ceb8-234">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ceb8-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ceb8-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ceb8-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

