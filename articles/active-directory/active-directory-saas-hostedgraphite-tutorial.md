---
title: 'Esercitazione: Integrazione di Azure Active Directory con Hosted Graphite | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e grafite ospitato.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d8914f6417ba8fbdef1a48e1b36635200ba130d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="ba064-103">Esercitazione: Integrazione di Azure Active Directory con Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="ba064-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="ba064-104">In questa esercitazione, è illustrato come toointegrate grafite Hosted con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ba064-104">In this tutorial, you learn how toointegrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba064-105">Integrazione grafite ospitato con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ba064-105">Integrating Hosted Graphite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ba064-106">È possibile controllare in Azure AD che ha accesso tooHosted grafite</span><span class="sxs-lookup"><span data-stu-id="ba064-106">You can control in Azure AD who has access tooHosted Graphite</span></span>
- <span data-ttu-id="ba064-107">È possibile abilitare l'utenti tooautomatically get connesso tooHosted grafite (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba064-107">You can enable your users tooautomatically get signed-on tooHosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ba064-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ba064-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ba064-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ba064-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba064-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ba064-110">Prerequisites</span></span>

<span data-ttu-id="ba064-111">integrazione di Azure AD con ospitato grafite tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ba064-111">tooconfigure Azure AD integration with Hosted Graphite, you need hello following items:</span></span>

- <span data-ttu-id="ba064-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba064-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba064-113">Sottoscrizione di Hosted Graphite abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ba064-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba064-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ba064-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba064-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ba064-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba064-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ba064-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba064-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba064-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba064-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ba064-118">Scenario description</span></span>
<span data-ttu-id="ba064-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ba064-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba064-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ba064-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba064-121">Aggiunta di grafite ospitato dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ba064-121">Adding Hosted Graphite from hello gallery</span></span>
2. <span data-ttu-id="ba064-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba064-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-hello-gallery"></a><span data-ttu-id="ba064-123">Aggiunta di grafite ospitato dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ba064-123">Adding Hosted Graphite from hello gallery</span></span>
<span data-ttu-id="ba064-124">integrazione hello tooconfigure di grafite ospitato in Azure AD, è necessario tooadd grafite ospitato dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ba064-124">tooconfigure hello integration of Hosted Graphite into Azure AD, you need tooadd Hosted Graphite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ba064-125">**tooadd grafite ospitato dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba064-125">**tooadd Hosted Graphite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba064-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ba064-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ba064-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ba064-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ba064-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ba064-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ba064-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ba064-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ba064-133">Nella casella di ricerca hello, digitare **ospitato grafite**.</span><span class="sxs-lookup"><span data-stu-id="ba064-133">In hello search box, type **Hosted Graphite**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="ba064-135">Nel riquadro dei risultati hello, selezionare **ospitato grafite**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ba064-135">In hello results panel, select **Hosted Graphite**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ba064-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba064-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ba064-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Hosted Graphite mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ba064-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ba064-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in grafite ospitato è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba064-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hosted Graphite is tooa user in Azure AD.</span></span> <span data-ttu-id="ba064-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in grafite ospitato richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ba064-140">In other words, a link relationship between an Azure AD user and hello related user in Hosted Graphite needs toobe established.</span></span>

<span data-ttu-id="ba064-141">In grafite ospitato, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="ba064-141">In Hosted Graphite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ba064-142">tooconfigure e prova AD Azure single sign-on con grafite ospitato, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ba064-142">tooconfigure and test Azure AD single sign-on with Hosted Graphite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ba064-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ba064-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ba064-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba064-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba064-145">**[Creazione di un utente di test ospitati grafite](#creating-a-hosted-graphite-test-user)**  -toohave un equivalente di Britta Simon in grafite ospitato che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ba064-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - toohave a counterpart of Britta Simon in Hosted Graphite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ba064-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ba064-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba064-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ba064-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ba064-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba064-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ba064-149">In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione grafite ospitato.</span><span class="sxs-lookup"><span data-stu-id="ba064-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="ba064-150">**Azure AD tooconfigure single sign-on con grafite ospitato, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba064-150">**tooconfigure Azure AD single sign-on with Hosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba064-151">Nel portale di Azure su hello hello **ospitato grafite** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ba064-151">In hello Azure portal, on hello **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ba064-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ba064-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="ba064-155">In hello **ospitato grafite dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ba064-155">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="ba064-157">a.</span><span class="sxs-lookup"><span data-stu-id="ba064-157">a.</span></span> <span data-ttu-id="ba064-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.hostedgraphite.com/metadata/<user id>`</span><span class="sxs-lookup"><span data-stu-id="ba064-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="ba064-159">b.</span><span class="sxs-lookup"><span data-stu-id="ba064-159">b.</span></span> <span data-ttu-id="ba064-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="ba064-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="ba064-161">In hello **ospitato grafite dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ba064-161">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="ba064-163">a.</span><span class="sxs-lookup"><span data-stu-id="ba064-163">a.</span></span> <span data-ttu-id="ba064-164">Fare clic su hello **Mostra URL impostazioni avanzate** opzione</span><span class="sxs-lookup"><span data-stu-id="ba064-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="ba064-165">b.</span><span class="sxs-lookup"><span data-stu-id="ba064-165">b.</span></span> <span data-ttu-id="ba064-166">In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.hostedgraphite.com/login/saml/<user id>/`</span><span class="sxs-lookup"><span data-stu-id="ba064-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="ba064-167">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="ba064-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="ba064-168">Hai tooupdate questi valori con hello effettivo identificatore, un URL di risposta e un URL di accesso.</span><span class="sxs-lookup"><span data-stu-id="ba064-168">You have tooupdate these values with hello actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="ba064-169">tooget questi valori, è possibile passare tooAccess -> configurazione SAML sul lato applicazione o contatto [team di supporto ospitato grafite](mailto:help@hostedgraphite.com).</span><span class="sxs-lookup"><span data-stu-id="ba064-169">tooget these values, you can go tooAccess->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="ba064-170">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ba064-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="ba064-172">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ba064-172">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ba064-174">In hello **ospitato configurazione grafite** fare clic su **configurare grafite ospitato** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="ba064-174">On hello **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ba064-175">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ba064-175">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="ba064-177">Tenant di grafite ospitato tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ba064-177">Sign-on tooyour Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="ba064-178">Passare toohello **pagina SAML Setup** nell'intestazione laterale hello (**accesso -> configurazione SAML**).</span><span class="sxs-lookup"><span data-stu-id="ba064-178">Go toohello **SAML Setup page** in hello sidebar (**Access -> SAML Setup**).</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="ba064-180">Verificare gli URL corrispondano alla configurazione eseguita su hello **ospitato grafite dominio e gli URL** sezione di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba064-180">Confirm these URls match your configuration done on hello **Hosted Graphite Domain and URLs** section of hello Azure portal.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="ba064-182">In **entità o ID autorità di certificazione** e **URL di accesso SSO** nelle caselle di testo, incollare il valore di hello di **ID entità SAML** e **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba064-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste hello value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="ba064-184">Selezionare "**Sola lettura**" come **ruolo utente predefinito**.</span><span class="sxs-lookup"><span data-stu-id="ba064-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="ba064-186">Aprire il certificato con codifica base 64 nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ba064-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="ba064-188">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ba064-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="ba064-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ba064-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ba064-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ba064-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ba064-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ba064-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ba064-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba064-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="ba064-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ba064-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ba064-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba064-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba064-196">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ba064-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ba064-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ba064-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ba064-200">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="ba064-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ba064-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ba064-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ba064-204">a.</span><span class="sxs-lookup"><span data-stu-id="ba064-204">a.</span></span> <span data-ttu-id="ba064-205">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ba064-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba064-206">b.</span><span class="sxs-lookup"><span data-stu-id="ba064-206">b.</span></span> <span data-ttu-id="ba064-207">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ba064-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ba064-208">c.</span><span class="sxs-lookup"><span data-stu-id="ba064-208">c.</span></span> <span data-ttu-id="ba064-209">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="ba064-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ba064-210">d.</span><span class="sxs-lookup"><span data-stu-id="ba064-210">d.</span></span> <span data-ttu-id="ba064-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ba064-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="ba064-212">Creazione di un utente test di Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="ba064-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="ba064-213">obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon in grafite ospitato.</span><span class="sxs-lookup"><span data-stu-id="ba064-213">hello objective of this section is toocreate a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="ba064-214">Hosted Graphite supporta il provisioning JIT, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ba064-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ba064-215">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="ba064-215">There is no action item for you in this section.</span></span> <span data-ttu-id="ba064-216">Verrà creato un nuovo utente durante una tooaccess tentativo grafite ospitato se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="ba064-216">A new user will be created during an attempt tooaccess Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="ba064-217">Se è necessario un utente toocreate manualmente, è necessario team di supporto toocontact hello grafite ospitato tramite < mailto:help@hostedgraphite.com >.</span><span class="sxs-lookup"><span data-stu-id="ba064-217">If you need toocreate a user manually, you need toocontact hello Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ba064-218">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba064-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ba064-219">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHosted grafite.</span><span class="sxs-lookup"><span data-stu-id="ba064-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHosted Graphite.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ba064-221">**tooassign Britta Simon tooHosted grafite, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba064-221">**tooassign Britta Simon tooHosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba064-222">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ba064-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ba064-224">Nell'elenco di applicazioni hello, selezionare **ospitato grafite**.</span><span class="sxs-lookup"><span data-stu-id="ba064-224">In hello applications list, select **Hosted Graphite**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="ba064-226">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ba064-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ba064-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ba064-228">Click **Add** button.</span></span> <span data-ttu-id="ba064-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ba064-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ba064-231">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ba064-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ba064-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ba064-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba064-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ba064-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ba064-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ba064-234">Testing single sign-on</span></span>

<span data-ttu-id="ba064-235">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ba064-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ba064-236">Quando si fa clic su riquadro ospitato grafite hello in hello Pannello di accesso, è necessario ottenere l'applicazione ospitata grafite tooyour automaticamente firmato in.</span><span class="sxs-lookup"><span data-stu-id="ba064-236">When you click hello Hosted Graphite tile in hello Access Panel, you should get automatically signed-on tooyour Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba064-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ba064-237">Additional resources</span></span>

* [<span data-ttu-id="ba064-238">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba064-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba064-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba064-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

