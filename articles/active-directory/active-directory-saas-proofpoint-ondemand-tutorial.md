---
title: 'Esercitazione: Integrazione di Azure Active Directory con Proofpoint on Demand | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Proofpoint su richiesta.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="49b34-103">Esercitazione: Integrazione di Azure Active Directory con Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="49b34-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="49b34-104">In questa esercitazione, è illustrato come toointegrate Proofpoint su richiesta con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49b34-104">In this tutorial, you learn how toointegrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49b34-105">Integrazione Proofpoint su richiesta con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="49b34-105">Integrating Proofpoint on Demand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="49b34-106">È possibile controllare in Azure AD che ha accesso tooProofpoint su richiesta</span><span class="sxs-lookup"><span data-stu-id="49b34-106">You can control in Azure AD who has access tooProofpoint on Demand</span></span>
- <span data-ttu-id="49b34-107">È possibile abilitare l'utenti tooautomatically get connesso tooProofpoint su richiesta (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="49b34-107">You can enable your users tooautomatically get signed-on tooProofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49b34-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="49b34-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="49b34-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49b34-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49b34-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="49b34-110">Prerequisites</span></span>

<span data-ttu-id="49b34-111">integrazione di Azure AD tooconfigure con Proofpoint su richiesta, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="49b34-111">tooconfigure Azure AD integration with Proofpoint on Demand, you need hello following items:</span></span>

- <span data-ttu-id="49b34-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49b34-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49b34-113">Sottoscrizione di Proofpoint on Demand abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="49b34-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49b34-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="49b34-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="49b34-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="49b34-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49b34-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="49b34-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49b34-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49b34-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49b34-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="49b34-118">Scenario description</span></span>
<span data-ttu-id="49b34-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="49b34-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49b34-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="49b34-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49b34-121">Aggiunta di Proofpoint su richiesta dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="49b34-121">Adding Proofpoint on Demand from hello gallery</span></span>
2. <span data-ttu-id="49b34-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="49b34-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a><span data-ttu-id="49b34-123">Aggiunta di Proofpoint su richiesta dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="49b34-123">Adding Proofpoint on Demand from hello gallery</span></span>
<span data-ttu-id="49b34-124">integrazione hello tooconfigure di Proofpoint su richiesta in Azure AD, è necessario tooadd Proofpoint su richiesta dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="49b34-124">tooconfigure hello integration of Proofpoint on Demand into Azure AD, you need tooadd Proofpoint on Demand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="49b34-125">**tooadd Proofpoint su richiesta dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="49b34-125">**tooadd Proofpoint on Demand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="49b34-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="49b34-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="49b34-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="49b34-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="49b34-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="49b34-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="49b34-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="49b34-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="49b34-133">Nella casella di ricerca hello, digitare **Proofpoint su richiesta**.</span><span class="sxs-lookup"><span data-stu-id="49b34-133">In hello search box, type **Proofpoint on Demand**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="49b34-135">Nel riquadro dei risultati hello, selezionare **Proofpoint su richiesta**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="49b34-135">In hello results panel, select **Proofpoint on Demand**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="49b34-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="49b34-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="49b34-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Proofpoint on Demand usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="49b34-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="49b34-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Proofpoint su richiesta è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49b34-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Proofpoint on Demand is tooa user in Azure AD.</span></span> <span data-ttu-id="49b34-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Proofpoint su richiesta richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="49b34-140">In other words, a link relationship between an Azure AD user and hello related user in Proofpoint on Demand needs toobe established.</span></span>

<span data-ttu-id="49b34-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Proofpoint su richiesta.</span><span class="sxs-lookup"><span data-stu-id="49b34-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="49b34-142">tooconfigure e test di Azure AD accesso single sign-on con Proofpoint su richiesta, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="49b34-142">tooconfigure and test Azure AD single sign-on with Proofpoint on Demand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="49b34-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="49b34-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="49b34-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49b34-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49b34-145">**[Creazione di un Proofpoint utente test richiesta](#creating-a-proofpoint-on-demand-test-user)**  -toohave un equivalente di Britta Simon in Proofpoint su richiesta che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="49b34-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - toohave a counterpart of Britta Simon in Proofpoint on Demand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="49b34-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="49b34-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49b34-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="49b34-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="49b34-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="49b34-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="49b34-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nel Proofpoint sull'applicazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="49b34-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="49b34-150">**Azure AD tooconfigure single sign-on con Proofpoint su richiesta, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="49b34-150">**tooconfigure Azure AD single sign-on with Proofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="49b34-151">Nel portale di Azure su hello hello **Proofpoint su richiesta** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="49b34-151">In hello Azure portal, on hello **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="49b34-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="49b34-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
  
    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="49b34-155">In hello **Proofpoint nel dominio di richiesta e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="49b34-155">On hello **Proofpoint on Demand Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="49b34-157">hello a.In **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="49b34-157">a.In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="49b34-158">b.</span><span class="sxs-lookup"><span data-stu-id="49b34-158">b.</span></span> <span data-ttu-id="49b34-159">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="49b34-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="49b34-160">c.</span><span class="sxs-lookup"><span data-stu-id="49b34-160">c.</span></span>  <span data-ttu-id="49b34-161">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="49b34-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="49b34-162">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="49b34-162">These values are not hello real.</span></span> <span data-ttu-id="49b34-163">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="49b34-163">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="49b34-164">Contatto [Proofpoint team di supporto di richiesta Client](https://www.proofpoint.com/us/support-services) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="49b34-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooget these values.</span></span> 

4. <span data-ttu-id="49b34-165">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="49b34-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="49b34-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="49b34-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="49b34-169">In hello **Proofpoint configurazione richiesta** fare clic su **configurare Proofpoint su richiesta** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="49b34-169">On hello **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="49b34-170">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="49b34-170">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="49b34-172">tooconfigure single sign-on sul **Proofpoint su richiesta** lato, è necessario hello toosend scaricato **Certificate(Base64)**,**ID entità SAML**, e **SAML Single Sign-On Service URL** troppo[Proofpoint team di supporto di richiesta Client](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="49b34-172">tooconfigure single sign-on on **Proofpoint on Demand** side, you need toosend hello downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="49b34-173">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="49b34-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="49b34-174">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="49b34-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="49b34-175">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="49b34-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="49b34-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="49b34-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="49b34-177">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="49b34-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="49b34-179">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="49b34-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="49b34-180">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="49b34-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49b34-182">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="49b34-182">These values are not hello real.</span></span> <span data-ttu-id="49b34-183">Aggiornare questi valori con hello effettivo</span><span class="sxs-lookup"><span data-stu-id="49b34-183">Update these values with hello actual</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49b34-185">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="49b34-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49b34-187">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="49b34-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49b34-189">a.</span><span class="sxs-lookup"><span data-stu-id="49b34-189">a.</span></span> <span data-ttu-id="49b34-190">In hello **nome** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="49b34-190">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="49b34-191">b.</span><span class="sxs-lookup"><span data-stu-id="49b34-191">b.</span></span> <span data-ttu-id="49b34-192">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49b34-192">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="49b34-193">c.</span><span class="sxs-lookup"><span data-stu-id="49b34-193">c.</span></span> <span data-ttu-id="49b34-194">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="49b34-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="49b34-195">d.</span><span class="sxs-lookup"><span data-stu-id="49b34-195">d.</span></span> <span data-ttu-id="49b34-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="49b34-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="49b34-197">Creazione di un utente di test di Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="49b34-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="49b34-198">In questa sezione viene creato un utente di nome Britta Simon in Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="49b34-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="49b34-199">Lavorare con [Proofpoint team di supporto di richiesta Client](https://www.proofpoint.com/us/support-services) utenti tooadd hello Proofpoint sulla piattaforma richiesta.</span><span class="sxs-lookup"><span data-stu-id="49b34-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooadd users in hello Proofpoint on Demand platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="49b34-200">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="49b34-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="49b34-201">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooProofpoint su richiesta.</span><span class="sxs-lookup"><span data-stu-id="49b34-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProofpoint on Demand.</span></span>

![Assegna utente][200] 

<span data-ttu-id="49b34-203">**tooassign tooProofpoint Britta Simon su richiesta, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="49b34-203">**tooassign Britta Simon tooProofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="49b34-204">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="49b34-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="49b34-206">Nell'elenco di applicazioni hello, selezionare **Proofpoint su richiesta**.</span><span class="sxs-lookup"><span data-stu-id="49b34-206">In hello applications list, select **Proofpoint on Demand**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="49b34-208">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="49b34-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="49b34-210">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="49b34-210">Click **Add** button.</span></span> <span data-ttu-id="49b34-211">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="49b34-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="49b34-213">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="49b34-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="49b34-214">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="49b34-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49b34-215">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="49b34-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="49b34-216">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="49b34-216">Testing single sign-on</span></span>

<span data-ttu-id="49b34-217">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="49b34-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="49b34-218">Quando si fa clic su hello **Proofpoint su richiesta** riquadro hello Pannello di accesso, è necessario eseguire automaticamente l'accesso tooyour Proofpoint sull'applicazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="49b34-218">When you click hello **Proofpoint on Demand** tile on hello Access Panel, you should be automatically signed on tooyour Proofpoint on Demand application.</span></span>
<span data-ttu-id="49b34-219">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="49b34-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="49b34-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="49b34-220">Additional resources</span></span>

* [<span data-ttu-id="49b34-221">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49b34-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49b34-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49b34-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

