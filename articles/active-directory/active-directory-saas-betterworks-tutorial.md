---
title: 'Esercitazione: Integrazione di Azure Active Directory con BetterWorks | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e BetterWorks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 9803593124318ea82e5a8888cc5a95b5da84472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="75472-103">Esercitazione: Integrazione di Azure Active Directory con BetterWorks</span><span class="sxs-lookup"><span data-stu-id="75472-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="75472-104">In questa esercitazione, è illustrato come toointegrate BetterWorks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75472-104">In this tutorial, you learn how toointegrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75472-105">Integrazione BetterWorks con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="75472-105">Integrating BetterWorks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="75472-106">È possibile controllare in Azure AD che ha accesso tooBetterWorks</span><span class="sxs-lookup"><span data-stu-id="75472-106">You can control in Azure AD who has access tooBetterWorks</span></span>
- <span data-ttu-id="75472-107">È possibile abilitare l'utenti tooautomatically get connesso tooBetterWorks (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="75472-107">You can enable your users tooautomatically get signed-on tooBetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="75472-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="75472-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="75472-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="75472-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75472-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="75472-110">Prerequisites</span></span>

<span data-ttu-id="75472-111">integrazione di Azure AD con BetterWorks tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="75472-111">tooconfigure Azure AD integration with BetterWorks, you need hello following items:</span></span>

- <span data-ttu-id="75472-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75472-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75472-113">Sottoscrizione di BetterWorks abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="75472-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75472-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="75472-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75472-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="75472-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75472-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="75472-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75472-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75472-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75472-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="75472-118">Scenario description</span></span>
<span data-ttu-id="75472-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="75472-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75472-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="75472-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75472-121">Aggiunta di BetterWorks dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="75472-121">Adding BetterWorks from hello gallery</span></span>
2. <span data-ttu-id="75472-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="75472-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-hello-gallery"></a><span data-ttu-id="75472-123">Aggiunta di BetterWorks dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="75472-123">Adding BetterWorks from hello gallery</span></span>
<span data-ttu-id="75472-124">integrazione hello tooconfigure di BetterWorks in Azure AD, è necessario tooadd BetterWorks dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="75472-124">tooconfigure hello integration of BetterWorks into Azure AD, you need tooadd BetterWorks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="75472-125">**tooadd BetterWorks dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="75472-125">**tooadd BetterWorks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="75472-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="75472-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="75472-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="75472-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="75472-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="75472-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="75472-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="75472-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="75472-133">Nella casella di ricerca hello, digitare **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="75472-133">In hello search box, type **BetterWorks**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="75472-135">Nel riquadro dei risultati hello, selezionare **BetterWorks**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="75472-135">In hello results panel, select **BetterWorks**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="75472-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="75472-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="75472-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BetterWorks usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="75472-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="75472-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in BetterWorks è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75472-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BetterWorks is tooa user in Azure AD.</span></span> <span data-ttu-id="75472-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in BetterWorks deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="75472-140">In other words, a link relationship between an Azure AD user and hello related user in BetterWorks needs toobe established.</span></span>

<span data-ttu-id="75472-141">In BetterWorks, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="75472-141">In BetterWorks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="75472-142">tooconfigure e prova AD Azure single sign-on con BetterWorks, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="75472-142">tooconfigure and test Azure AD single sign-on with BetterWorks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="75472-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="75472-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="75472-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="75472-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75472-145">**[Creazione di un utente test BetterWorks](#creating-a-betterworks-test-user)**  -toohave un equivalente di Britta Simon in BetterWorks che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="75472-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - toohave a counterpart of Britta Simon in BetterWorks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="75472-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="75472-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75472-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="75472-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="75472-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="75472-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="75472-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="75472-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="75472-150">**Azure AD tooconfigure single sign-on con BetterWorks, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="75472-150">**tooconfigure Azure AD single sign-on with BetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="75472-151">Nel portale di Azure su hello hello **BetterWorks** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="75472-151">In hello Azure portal, on hello **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="75472-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="75472-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="75472-155">In hello **BetterWorks dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**:</span><span class="sxs-lookup"><span data-stu-id="75472-155">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="75472-157">a.</span><span class="sxs-lookup"><span data-stu-id="75472-157">a.</span></span> <span data-ttu-id="75472-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="75472-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="75472-159">b.</span><span class="sxs-lookup"><span data-stu-id="75472-159">b.</span></span> <span data-ttu-id="75472-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="75472-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="75472-161">In hello **BetterWorks dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="75472-161">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="75472-163">a.</span><span class="sxs-lookup"><span data-stu-id="75472-163">a.</span></span> <span data-ttu-id="75472-164">Fare clic su hello **Mostra URL impostazioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="75472-164">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="75472-165">b.</span><span class="sxs-lookup"><span data-stu-id="75472-165">b.</span></span> <span data-ttu-id="75472-166">In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="75472-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="75472-167">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="75472-167">These are not real values.</span></span> <span data-ttu-id="75472-168">Aggiornare questi valori con hello URL di risposta effettivo URL di accesso e di identificatore.</span><span class="sxs-lookup"><span data-stu-id="75472-168">Update these values with hello Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="75472-169">Contatto [team di supporto BetterWorks](mailto:support@betterworks.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="75472-169">Contact [BetterWorks support team](mailto:support@betterworks.com) tooget these values.</span></span>
 
4. <span data-ttu-id="75472-170">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="75472-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="75472-172">Applicazione di BetterWorks prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="75472-172">BetterWorks application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="75472-173">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="75472-173">Configure hello following claims for this application.</span></span> <span data-ttu-id="75472-174">È possibile gestire i valori hello di questi attributi da hello "**attributo**" scheda di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="75472-174">You can manage hello values of these attributes from hello "**Attribute**" tab of hello application.</span></span> <span data-ttu-id="75472-175">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="75472-175">hello following screenshot shows an example for this.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="75472-177">In hello **attributi token SAML** finestra di dialogo, per ogni riga nella tabella hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="75472-177">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
   | <span data-ttu-id="75472-178">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="75472-178">Attribute Name</span></span> | <span data-ttu-id="75472-179">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="75472-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="75472-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="75472-180">saml_token</span></span>     | <span data-ttu-id="75472-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="75472-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="75472-182">a.</span><span class="sxs-lookup"><span data-stu-id="75472-182">a.</span></span> <span data-ttu-id="75472-183">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="75472-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="75472-186">b.</span><span class="sxs-lookup"><span data-stu-id="75472-186">b.</span></span> <span data-ttu-id="75472-187">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="75472-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

   <span data-ttu-id="75472-188">c.</span><span class="sxs-lookup"><span data-stu-id="75472-188">c.</span></span> <span data-ttu-id="75472-189">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="75472-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
   <span data-ttu-id="75472-190">d.</span><span class="sxs-lookup"><span data-stu-id="75472-190">d.</span></span> <span data-ttu-id="75472-191">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="75472-191">Click **Ok**.</span></span>

7. <span data-ttu-id="75472-192">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="75472-192">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="75472-194">tooconfigure single sign-on sul **BetterWorks** lato, è necessario hello toosend scaricato **Metadata XML** troppo[BetterWorks team di supporto](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="75472-194">tooconfigure single sign-on on **BetterWorks** side, you need toosend hello downloaded **Metadata XML** too[BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="75472-195">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="75472-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="75472-196">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="75472-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="75472-197">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="75472-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="75472-198">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="75472-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="75472-199">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="75472-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="75472-201">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="75472-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="75472-202">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="75472-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="75472-204">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="75472-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="75472-206">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="75472-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="75472-208">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="75472-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="75472-210">a.</span><span class="sxs-lookup"><span data-stu-id="75472-210">a.</span></span> <span data-ttu-id="75472-211">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="75472-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75472-212">b.</span><span class="sxs-lookup"><span data-stu-id="75472-212">b.</span></span> <span data-ttu-id="75472-213">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="75472-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="75472-214">c.</span><span class="sxs-lookup"><span data-stu-id="75472-214">c.</span></span> <span data-ttu-id="75472-215">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="75472-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="75472-216">d.</span><span class="sxs-lookup"><span data-stu-id="75472-216">d.</span></span> <span data-ttu-id="75472-217">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="75472-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="75472-218">Creazione di un utente di test per BetterWorks</span><span class="sxs-lookup"><span data-stu-id="75472-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="75472-219">In questa sezione viene creato un utente di nome Britta Simon in BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="75472-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="75472-220">Lavorare con [BetterWorks team di supporto](mailto:support@betterworks.com) utenti hello tooadd nella piattaforma BetterWorks hello.</span><span class="sxs-lookup"><span data-stu-id="75472-220">Work with [BetterWorks support team](mailto:support@betterworks.com) tooadd hello users in hello BetterWorks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="75472-221">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="75472-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="75472-222">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBetterWorks.</span><span class="sxs-lookup"><span data-stu-id="75472-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBetterWorks.</span></span>

![Assegna utente][200] 

<span data-ttu-id="75472-224">**tooassign Britta Simon tooBetterWorks, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="75472-224">**tooassign Britta Simon tooBetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="75472-225">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="75472-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="75472-227">Nell'elenco di applicazioni hello, selezionare **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="75472-227">In hello applications list, select **BetterWorks**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="75472-229">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="75472-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="75472-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="75472-231">Click **Add** button.</span></span> <span data-ttu-id="75472-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="75472-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="75472-234">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="75472-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="75472-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="75472-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75472-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="75472-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="75472-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="75472-237">Testing single sign-on</span></span>

<span data-ttu-id="75472-238">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="75472-238">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="75472-239">Quando si fa clic hello BetterWorks riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour BetterWorks applicazione.</span><span class="sxs-lookup"><span data-stu-id="75472-239">When you click hello BetterWorks tile in hello Access Panel, you should get automatically signed-on tooyour BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="75472-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="75472-240">Additional resources</span></span>

* [<span data-ttu-id="75472-241">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75472-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75472-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75472-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

