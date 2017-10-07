---
title: 'Esercitazione: Integrazione di Azure Active Directory con MaxxPoint | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e MaxxPoint.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 03b13908add8d8c62f1d1480ed2288658fce14d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="5b5e2-103">Esercitazione: Integrazione di Azure Active Directory con MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="5b5e2-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="5b5e2-104">In questa esercitazione, è illustrato come toointegrate MaxxPoint con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b5e2-104">In this tutorial, you learn how toointegrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b5e2-105">Integrazione MaxxPoint con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5b5e2-105">Integrating MaxxPoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b5e2-106">È possibile controllare in Azure AD che ha accesso tooMaxxPoint</span><span class="sxs-lookup"><span data-stu-id="5b5e2-106">You can control in Azure AD who has access tooMaxxPoint</span></span>
- <span data-ttu-id="5b5e2-107">È possibile abilitare l'utenti tooautomatically get connesso tooMaxxPoint (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b5e2-107">You can enable your users tooautomatically get signed-on tooMaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b5e2-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5b5e2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b5e2-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b5e2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b5e2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5b5e2-110">Prerequisites</span></span>

<span data-ttu-id="5b5e2-111">integrazione di Azure AD con MaxxPoint tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5b5e2-111">tooconfigure Azure AD integration with MaxxPoint, you need hello following items:</span></span>

- <span data-ttu-id="5b5e2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b5e2-113">Sottoscrizione di MaxxPoint abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5b5e2-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b5e2-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b5e2-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5b5e2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b5e2-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5b5e2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b5e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b5e2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5b5e2-118">Scenario description</span></span>
<span data-ttu-id="5b5e2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b5e2-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5b5e2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b5e2-121">Aggiunta di MaxxPoint dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5b5e2-121">Adding MaxxPoint from hello gallery</span></span>
2. <span data-ttu-id="5b5e2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b5e2-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-hello-gallery"></a><span data-ttu-id="5b5e2-123">Aggiunta di MaxxPoint dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5b5e2-123">Adding MaxxPoint from hello gallery</span></span>
<span data-ttu-id="5b5e2-124">integrazione hello tooconfigure di MaxxPoint in Azure AD, è necessario tooadd MaxxPoint dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-124">tooconfigure hello integration of MaxxPoint into Azure AD, you need tooadd MaxxPoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b5e2-125">**tooadd MaxxPoint dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5b5e2-125">**tooadd MaxxPoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b5e2-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b5e2-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b5e2-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5b5e2-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della nuova applicazione di finestra di dialogo tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-131">Click **New application** button on hello top of dialog tooadd new application.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5b5e2-133">Nella casella di ricerca hello, digitare **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-133">In hello search box, type **MaxxPoint**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="5b5e2-135">Nel riquadro dei risultati hello, selezionare **MaxxPoint**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-135">In hello results panel, select **MaxxPoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b5e2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b5e2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b5e2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con MaxxPoint in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5b5e2-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b5e2-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in MaxxPoint è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MaxxPoint is tooa user in Azure AD.</span></span> <span data-ttu-id="5b5e2-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in MaxxPoint deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-140">In other words, a link relationship between an Azure AD user and hello related user in MaxxPoint needs toobe established.</span></span>

<span data-ttu-id="5b5e2-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in MaxxPoint.</span></span>

<span data-ttu-id="5b5e2-142">tooconfigure e prova AD Azure single sign-on con MaxxPoint, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5b5e2-142">tooconfigure and test Azure AD single sign-on with MaxxPoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b5e2-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b5e2-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b5e2-145">**[Creazione di un utente test MaxxPoint](#creating-a-maxxpoint-test-user)**  -toohave un equivalente di Britta Simon in MaxxPoint toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - toohave a counterpart of Britta Simon in MaxxPoint that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="5b5e2-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b5e2-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b5e2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b5e2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b5e2-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="5b5e2-150">**Azure AD tooconfigure single sign-on con MaxxPoint, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5b5e2-150">**tooconfigure Azure AD single sign-on with MaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b5e2-151">Nel portale di Azure su hello hello **MaxxPoint** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-151">In hello Azure portal, on hello **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5b5e2-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="5b5e2-155">In hello **MaxxPoint dominio e gli URL** sezione, se si desidera un'applicazione hello tooconfigure in **modalità avviata da IDP**, non necessario tooperform tutte le operazioni.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-155">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, no need tooperform any steps.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="5b5e2-157">In hello **MaxxPoint dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5b5e2-157">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="5b5e2-159">a.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-159">a.</span></span> <span data-ttu-id="5b5e2-160">Fare clic sull'opzione **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="5b5e2-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="5b5e2-161">b.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-161">b.</span></span> <span data-ttu-id="5b5e2-162">In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="5b5e2-162">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b5e2-163">Si noti che questo non è il valore reale hello.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="5b5e2-164">È necessario tooupdate URL di accesso questo valore con hello effettivo.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="5b5e2-165">Chiamare team MaxxPoint su **888-728-0950** tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-165">Call MaxxPoint team on **888-728-0950** tooget this value.</span></span>

5. <span data-ttu-id="5b5e2-166">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="5b5e2-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5b5e2-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5b5e2-170">tooget SSO è configurato per l'applicazione, chiamare il team di supporto MaxxPoint su **888-728-0950** e sarà assistenza per ulteriormente in modalità di download tooprovide li hello **Metadata XML** file.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-170">tooget SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how tooprovide them hello downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="5b5e2-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5b5e2-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b5e2-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b5e2-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b5e2-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b5e2-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b5e2-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b5e2-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5b5e2-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5b5e2-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b5e2-178">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b5e2-180">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b5e2-182">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-182">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b5e2-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5b5e2-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b5e2-186">a.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-186">a.</span></span> <span data-ttu-id="5b5e2-187">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b5e2-188">b.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-188">b.</span></span> <span data-ttu-id="5b5e2-189">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b5e2-190">c.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-190">c.</span></span> <span data-ttu-id="5b5e2-191">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b5e2-192">d.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-192">d.</span></span> <span data-ttu-id="5b5e2-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="5b5e2-194">Creazione di un utente test MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="5b5e2-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="5b5e2-195">In questa sezione viene creato un utente di nome Britta Simon in MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="5b5e2-196">Contattare il team di supporto MaxxPoint su **888-728-0950** tooadd utenti hello hello MaxxPoint applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-196">Please call MaxxPoint support team on **888-728-0950** tooadd hello users in hello MaxxPoint application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b5e2-197">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b5e2-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b5e2-198">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooMaxxPoint proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooMaxxPoint.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5b5e2-200">**tooassign Britta Simon tooMaxxPoint, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5b5e2-200">**tooassign Britta Simon tooMaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b5e2-201">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5b5e2-203">Nell'elenco di applicazioni hello, selezionare **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-203">In hello applications list, select **MaxxPoint**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="5b5e2-205">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5b5e2-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-207">Click **Add** button.</span></span> <span data-ttu-id="5b5e2-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5b5e2-210">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b5e2-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b5e2-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b5e2-213">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5b5e2-213">Testing single sign-on</span></span>

<span data-ttu-id="5b5e2-214">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5b5e2-215">Quando si fa clic su riquadro MaxxPoint hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour MaxxPoint applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-215">When you click hello MaxxPoint tile in hello Access Panel, you should get automatically signed-on tooyour MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5b5e2-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5b5e2-216">Additional resources</span></span>

* [<span data-ttu-id="5b5e2-217">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b5e2-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b5e2-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b5e2-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png