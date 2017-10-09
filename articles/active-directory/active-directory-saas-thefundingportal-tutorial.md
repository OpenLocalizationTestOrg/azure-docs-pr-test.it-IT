---
title: 'Esercitazione: Integrazione di Azure Active Directory con hello finanziamento portale | Documenti Microsoft'
description: Scopri tooconfigure single sign-on tra Azure Active Directory e hello finanziamento portale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9f4329e02f91eb6d8034f17646ac7d15afe503e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hello-funding-portal"></a><span data-ttu-id="04b50-103">Esercitazione: Integrazione di Azure Active Directory con hello finanziamento portale</span><span class="sxs-lookup"><span data-stu-id="04b50-103">Tutorial: Azure Active Directory integration with hello Funding Portal</span></span>

<span data-ttu-id="04b50-104">In questa esercitazione viene illustrato come toointegrate hello finanziamento portale con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="04b50-104">In this tutorial, you learn how toointegrate hello Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="04b50-105">L'integrazione di hello finanziamento portale con Azure AD offre hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="04b50-105">Integrating hello Funding Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="04b50-106">È possibile controllare in Azure AD che ha accesso toohello Funding portale</span><span class="sxs-lookup"><span data-stu-id="04b50-106">You can control in Azure AD who has access toohello Funding Portal</span></span>
- <span data-ttu-id="04b50-107">È possibile abilitare l'utenti tooautomatically get connesso toohello portale Funding (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b50-107">You can enable your users tooautomatically get signed-on toohello Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="04b50-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="04b50-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="04b50-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="04b50-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04b50-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="04b50-110">Prerequisites</span></span>

<span data-ttu-id="04b50-111">integrazione tooconfigure Azure AD con hello Funding portale, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="04b50-111">tooconfigure Azure AD integration with hello Funding Portal, you need hello following items:</span></span>

- <span data-ttu-id="04b50-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04b50-112">An Azure AD subscription</span></span>
- <span data-ttu-id="04b50-113">Sottoscrizione di un hello finanziamento single sign-on Portal abilitata</span><span class="sxs-lookup"><span data-stu-id="04b50-113">A hello Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="04b50-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="04b50-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="04b50-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="04b50-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="04b50-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="04b50-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="04b50-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="04b50-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="04b50-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="04b50-118">Scenario description</span></span>
<span data-ttu-id="04b50-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="04b50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="04b50-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="04b50-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="04b50-121">Aggiunta di hello portale Funding dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="04b50-121">Adding hello Funding Portal from hello gallery</span></span>
2. <span data-ttu-id="04b50-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b50-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hello-funding-portal-from-hello-gallery"></a><span data-ttu-id="04b50-123">Aggiunta di hello portale Funding dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="04b50-123">Adding hello Funding Portal from hello gallery</span></span>
<span data-ttu-id="04b50-124">integrazione hello tooconfigure di hello Funding portale in Azure AD, è necessario tooadd hello portale Funding dall'elenco di tooyour hello della raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="04b50-124">tooconfigure hello integration of hello Funding Portal into Azure AD, you need tooadd hello Funding Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="04b50-125">**tooadd hello finanziamento portale dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="04b50-125">**tooadd hello Funding Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="04b50-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="04b50-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="04b50-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="04b50-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="04b50-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="04b50-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="04b50-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="04b50-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="04b50-133">Nella casella di ricerca hello, digitare **hello finanziamento portale**.</span><span class="sxs-lookup"><span data-stu-id="04b50-133">In hello search box, type **hello Funding Portal**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="04b50-135">Nel riquadro dei risultati hello, selezionare **hello finanziamento portale**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="04b50-135">In hello results panel, select **hello Funding Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="04b50-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b50-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="04b50-138">In questa sezione, configurare e testare Azure AD single sign-on con hello che finanziamento portale basato su un utente di test denominato "Laura Giussani".</span><span class="sxs-lookup"><span data-stu-id="04b50-138">In this section, you configure and test Azure AD single sign-on with hello Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="04b50-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in hello finanziamento portale è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04b50-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in hello Funding Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="04b50-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in hello finanziamento portale richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="04b50-140">In other words, a link relationship between an Azure AD user and hello related user in hello Funding Portal needs toobe established.</span></span>

<span data-ttu-id="04b50-141">Nel portale finanziamento di hello, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="04b50-141">In hello Funding Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="04b50-142">tooconfigure e prova AD Azure single sign-on con hello Funding portale, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="04b50-142">tooconfigure and test Azure AD single sign-on with hello Funding Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="04b50-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="04b50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="04b50-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04b50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="04b50-145">**[La creazione dell'utente di test finanziamento portale hello](#creating-the-funding-portal-test-user)**  -toohave un equivalente di Britta Simon in hello portale Funding rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="04b50-145">**[Creating hello Funding Portal test user](#creating-the-funding-portal-test-user)** - toohave a counterpart of Britta Simon in hello Funding Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="04b50-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="04b50-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="04b50-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="04b50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="04b50-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b50-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="04b50-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione del portale finanziamento hello.</span><span class="sxs-lookup"><span data-stu-id="04b50-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your hello Funding Portal application.</span></span>

<span data-ttu-id="04b50-150">**tooconfigure AD Azure single sign-on con hello finanziamento Portal, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="04b50-150">**tooconfigure Azure AD single sign-on with hello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="04b50-151">Nel portale di Azure su hello hello **hello finanziamento portale** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="04b50-151">In hello Azure portal, on hello **hello Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="04b50-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="04b50-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="04b50-155">In hello **hello finanziamento dominio portale e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="04b50-155">On hello **hello Funding Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="04b50-157">a.</span><span class="sxs-lookup"><span data-stu-id="04b50-157">a.</span></span> <span data-ttu-id="04b50-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="04b50-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="04b50-159">b.</span><span class="sxs-lookup"><span data-stu-id="04b50-159">b.</span></span> <span data-ttu-id="04b50-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="04b50-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="04b50-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="04b50-161">These values are not real.</span></span> <span data-ttu-id="04b50-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="04b50-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="04b50-163">Contatto [salve team di supporto Client di portale finanziamento](mailto:info@regenteducation.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="04b50-163">Contact [hello Funding Portal Client support team](mailto:info@regenteducation.com) tooget these values.</span></span> 

4. <span data-ttu-id="04b50-164">applicazione del portale finanziamento Hello prevede toocontain di asserzioni SAML hello un attributo denominato "externalId1".</span><span class="sxs-lookup"><span data-stu-id="04b50-164">hello Funding Portal application expects hello SAML assertions toocontain an attribute named "externalId1".</span></span> <span data-ttu-id="04b50-165">il valore di Hello di "externalId1" deve essere un studentID riconosciuto.</span><span class="sxs-lookup"><span data-stu-id="04b50-165">hello value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="04b50-166">Configurare attestazioni hello "externalId1" per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="04b50-166">Configure hello "externalId1" claim for this application.</span></span> <span data-ttu-id="04b50-167">È possibile gestire i valori hello di questi attributi da hello **gli attributi utente** di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="04b50-167">You can manage hello values of these attributes from hello **User Attributes** of hello application.</span></span> <span data-ttu-id="04b50-168">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="04b50-168">hello following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="04b50-170">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="04b50-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>

    | <span data-ttu-id="04b50-171">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="04b50-171">Attribute Name</span></span> | <span data-ttu-id="04b50-172">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="04b50-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="04b50-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="04b50-173">externalId1</span></span> | <span data-ttu-id="04b50-174">user.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="04b50-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="04b50-175">a.</span><span class="sxs-lookup"><span data-stu-id="04b50-175">a.</span></span> <span data-ttu-id="04b50-176">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="04b50-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="04b50-179">b.</span><span class="sxs-lookup"><span data-stu-id="04b50-179">b.</span></span> <span data-ttu-id="04b50-180">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="04b50-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="04b50-181">c.</span><span class="sxs-lookup"><span data-stu-id="04b50-181">c.</span></span> <span data-ttu-id="04b50-182">Da hello **valore dell'attributo** elenco, attributo hello selezionare da toouse per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="04b50-182">From hello **Attribute Value** list, select hello attribute you want toouse for your implementation.</span></span> <span data-ttu-id="04b50-183">Ad esempio, se è stato archiviato il valore StudentID hello in hello ExtensionAttribute1, quindi selezionare user.extensionattribute1.</span><span class="sxs-lookup"><span data-stu-id="04b50-183">For example, if you have stored hello StudentID value in hello ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="04b50-184">d.</span><span class="sxs-lookup"><span data-stu-id="04b50-184">d.</span></span> <span data-ttu-id="04b50-185">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="04b50-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="04b50-186">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="04b50-186">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="04b50-188">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="04b50-188">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="04b50-190">tooconfigure single sign-on sul **hello finanziamento portale** lato, è necessario hello toosend scaricato **Metadata XML** troppo[salve team di supporto finanziamento portale](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="04b50-190">tooconfigure single sign-on on **hello Funding Portal** side, you need toosend hello downloaded **Metadata XML** too[hello Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="04b50-191">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="04b50-191">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="04b50-192">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="04b50-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="04b50-193">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="04b50-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="04b50-194">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="04b50-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="04b50-195">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b50-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="04b50-196">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="04b50-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="04b50-198">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="04b50-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="04b50-199">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="04b50-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="04b50-201">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="04b50-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="04b50-203">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="04b50-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="04b50-205">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="04b50-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="04b50-207">a.</span><span class="sxs-lookup"><span data-stu-id="04b50-207">a.</span></span> <span data-ttu-id="04b50-208">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="04b50-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="04b50-209">b.</span><span class="sxs-lookup"><span data-stu-id="04b50-209">b.</span></span> <span data-ttu-id="04b50-210">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="04b50-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="04b50-211">c.</span><span class="sxs-lookup"><span data-stu-id="04b50-211">c.</span></span> <span data-ttu-id="04b50-212">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="04b50-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="04b50-213">d.</span><span class="sxs-lookup"><span data-stu-id="04b50-213">d.</span></span> <span data-ttu-id="04b50-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="04b50-214">Click **Create**.</span></span>
 
### <a name="creating-hello-funding-portal-test-user"></a><span data-ttu-id="04b50-215">Creazione utente test portale finanziamento di hello</span><span class="sxs-lookup"><span data-stu-id="04b50-215">Creating hello Funding Portal test user</span></span>

<span data-ttu-id="04b50-216">In questa sezione si crea un utente denominato Britta Simon in hello Funding portale.</span><span class="sxs-lookup"><span data-stu-id="04b50-216">In this section, you create a user called Britta Simon in hello Funding Portal.</span></span> <span data-ttu-id="04b50-217">Lavorare con [salve team di supporto finanziamento portale](mailto:info@regenteducation.com) tooadd hello utente test e abilitare SSO.</span><span class="sxs-lookup"><span data-stu-id="04b50-217">Work with [hello Funding Portal support team](mailto:info@regenteducation.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="04b50-218">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b50-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="04b50-219">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso toohello Funding portale.</span><span class="sxs-lookup"><span data-stu-id="04b50-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toohello Funding Portal.</span></span>

![Assegna utente][200] 

<span data-ttu-id="04b50-221">**tooassign Britta Simon toohello Funding Portal, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="04b50-221">**tooassign Britta Simon toohello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="04b50-222">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="04b50-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="04b50-224">Nell'elenco di applicazioni hello, selezionare **hello finanziamento portale**.</span><span class="sxs-lookup"><span data-stu-id="04b50-224">In hello applications list, select **hello Funding Portal**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="04b50-226">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="04b50-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="04b50-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="04b50-228">Click **Add** button.</span></span> <span data-ttu-id="04b50-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="04b50-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="04b50-231">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="04b50-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="04b50-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="04b50-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="04b50-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="04b50-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="04b50-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="04b50-234">Testing single sign-on</span></span>

<span data-ttu-id="04b50-235">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="04b50-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="04b50-236">Quando si fa clic su riquadro portale finanziamento di hello hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in un'applicazione hello finanziamento portale.</span><span class="sxs-lookup"><span data-stu-id="04b50-236">When you click hello hello Funding Portal tile in hello Access Panel, you should get automatically signed-on tooyour hello Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="04b50-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="04b50-237">Additional resources</span></span>

* [<span data-ttu-id="04b50-238">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04b50-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="04b50-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04b50-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

