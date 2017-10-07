---
title: 'Esercitazione: Integrazione di Azure Active Directory con 123ContactForm | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e 123ContactForm.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="0041a-103">Esercitazione: Integrazione di Azure Active Directory con 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="0041a-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="0041a-104">In questa esercitazione, è illustrato come 123ContactForm toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0041a-104">In this tutorial, you learn how toointegrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0041a-105">Integrazione 123ContactForm con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0041a-105">Integrating 123ContactForm with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0041a-106">È possibile controllare in Azure AD che ha accesso too123ContactForm</span><span class="sxs-lookup"><span data-stu-id="0041a-106">You can control in Azure AD who has access too123ContactForm</span></span>
- <span data-ttu-id="0041a-107">È possibile abilitare il get tooautomatically utenti connesso too123ContactForm (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0041a-107">You can enable your users tooautomatically get signed-on too123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0041a-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0041a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0041a-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0041a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0041a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0041a-110">Prerequisites</span></span>

<span data-ttu-id="0041a-111">integrazione di Azure AD con 123ContactForm tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0041a-111">tooconfigure Azure AD integration with 123ContactForm, you need hello following items:</span></span>

- <span data-ttu-id="0041a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0041a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0041a-113">Sottoscrizione di 123ContactForm abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0041a-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0041a-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0041a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0041a-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="0041a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0041a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0041a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0041a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0041a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0041a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0041a-118">Scenario description</span></span>
<span data-ttu-id="0041a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0041a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0041a-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="0041a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0041a-121">Aggiunta di 123ContactForm dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0041a-121">Adding 123ContactForm from hello gallery</span></span>
2. <span data-ttu-id="0041a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0041a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-hello-gallery"></a><span data-ttu-id="0041a-123">Aggiunta di 123ContactForm dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0041a-123">Adding 123ContactForm from hello gallery</span></span>
<span data-ttu-id="0041a-124">integrazione hello tooconfigure di 123ContactForm in Azure AD, è necessario 123ContactForm tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0041a-124">tooconfigure hello integration of 123ContactForm into Azure AD, you need tooadd 123ContactForm from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0041a-125">**123ContactForm tooadd dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0041a-125">**tooadd 123ContactForm from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0041a-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0041a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0041a-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0041a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0041a-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0041a-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0041a-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0041a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0041a-133">Nella casella di ricerca hello, digitare **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="0041a-133">In hello search box, type **123ContactForm**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="0041a-135">Nel riquadro dei risultati hello, selezionare **123ContactForm**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0041a-135">In hello results panel, select **123ContactForm**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0041a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0041a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0041a-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 123ContactForm mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0041a-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0041a-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in 123ContactForm è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0041a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 123ContactForm is tooa user in Azure AD.</span></span> <span data-ttu-id="0041a-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in 123ContactForm deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="0041a-140">In other words, a link relationship between an Azure AD user and hello related user in 123ContactForm needs toobe established.</span></span>

<span data-ttu-id="0041a-141">In 123ContactForm, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="0041a-141">In 123ContactForm, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0041a-142">tooconfigure e prova AD Azure single sign-on con 123ContactForm, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="0041a-142">tooconfigure and test Azure AD single sign-on with 123ContactForm, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0041a-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0041a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0041a-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0041a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0041a-145">**[Creazione di un utente test 123ContactForm](#creating-a-123contactform-test-user)**  -toohave un equivalente di Britta Simon in 123ContactForm che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0041a-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - toohave a counterpart of Britta Simon in 123ContactForm that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0041a-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0041a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0041a-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="0041a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0041a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0041a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0041a-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="0041a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="0041a-150">**Azure AD tooconfigure single sign-on con 123ContactForm, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0041a-150">**tooconfigure Azure AD single sign-on with 123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="0041a-151">Nel portale di Azure su hello hello **123ContactForm** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0041a-151">In hello Azure portal, on hello **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0041a-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0041a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="0041a-155">In hello **123ContactForm dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0041a-155">On hello **123ContactForm Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="0041a-157">a.</span><span class="sxs-lookup"><span data-stu-id="0041a-157">a.</span></span> <span data-ttu-id="0041a-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="0041a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="0041a-159">b.</span><span class="sxs-lookup"><span data-stu-id="0041a-159">b.</span></span> <span data-ttu-id="0041a-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="0041a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="0041a-161">Se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0041a-161">If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="0041a-163">a.</span><span class="sxs-lookup"><span data-stu-id="0041a-163">a.</span></span> <span data-ttu-id="0041a-164">Fare clic su hello **Mostra URL impostazioni avanzate** opzione</span><span class="sxs-lookup"><span data-stu-id="0041a-164">Click hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="0041a-165">b.</span><span class="sxs-lookup"><span data-stu-id="0041a-165">b.</span></span> <span data-ttu-id="0041a-166">In hello **URL di accesso** casella di testo, digitare un URL come:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="0041a-166">In hello **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0041a-167">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0041a-167">These values are not real.</span></span> <span data-ttu-id="0041a-168">È necessario tooupdate questi valore effettivo URL e l'identificatore di cui è illustrato più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="0041a-168">You'll need tooupdate these value from actual URLs and Identifier which is explained later in hello tutorial.</span></span>
    
5. <span data-ttu-id="0041a-169">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0041a-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="0041a-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0041a-171">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0041a-173">tooconfigure single sign-on sul **123ContactForm** sul lato, andare troppo[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0041a-173">tooconfigure single sign-on on **123ContactForm** side, go too[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="0041a-175">a.</span><span class="sxs-lookup"><span data-stu-id="0041a-175">a.</span></span> <span data-ttu-id="0041a-176">In hello **posta elettronica** casella di testo, posta elettronica hello tipo di nome utente hello</span><span class="sxs-lookup"><span data-stu-id="0041a-176">In hello **Email** textbox, type hello email of hello user i.e</span></span> <span data-ttu-id="0041a-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="0041a-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="0041a-178">b.</span><span class="sxs-lookup"><span data-stu-id="0041a-178">b.</span></span> <span data-ttu-id="0041a-179">Fare clic su **caricare** ed esplorare hello file Metadata XML, che è stato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0041a-179">Click **Upload** and browse hello Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="0041a-180">c.</span><span class="sxs-lookup"><span data-stu-id="0041a-180">c.</span></span> <span data-ttu-id="0041a-181">Fare clic su **SUBMIT FORM** (Invia modulo).</span><span class="sxs-lookup"><span data-stu-id="0041a-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="0041a-182">In hello **AD-Single sign on a Microsoft Azure Configura impostazioni App** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0041a-182">On hello **Microsoft Azure AD - Single sign-on - Configure App Settings** perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="0041a-184">a.</span><span class="sxs-lookup"><span data-stu-id="0041a-184">a.</span></span> <span data-ttu-id="0041a-185">Se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**, hello copia **identificatore** valore per l'istanza e incollarlo in **identificatore** casella di testo in **123ContactForm dominio e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0041a-185">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="0041a-186">b.</span><span class="sxs-lookup"><span data-stu-id="0041a-186">b.</span></span> <span data-ttu-id="0041a-187">Se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**, hello copia **URL di risposta** valore per l'istanza e incollarlo in **URL di risposta** casella di testo in **123ContactForm dominio e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0041a-187">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="0041a-188">c.</span><span class="sxs-lookup"><span data-stu-id="0041a-188">c.</span></span> <span data-ttu-id="0041a-189">Se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, hello copia **SIGN ON URL** valore per l'istanza e incollarlo in **URL di accesso** casella di testo in **123ContactForm dominio e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0041a-189">If you wish tooconfigure hello application in **SP initiated mode**, copy hello **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="0041a-190">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="0041a-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0041a-191">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="0041a-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0041a-192">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0041a-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0041a-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0041a-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="0041a-194">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0041a-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0041a-196">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0041a-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0041a-197">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0041a-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0041a-199">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0041a-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0041a-201">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="0041a-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0041a-203">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0041a-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0041a-205">a.</span><span class="sxs-lookup"><span data-stu-id="0041a-205">a.</span></span> <span data-ttu-id="0041a-206">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0041a-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0041a-207">b.</span><span class="sxs-lookup"><span data-stu-id="0041a-207">b.</span></span> <span data-ttu-id="0041a-208">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0041a-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0041a-209">c.</span><span class="sxs-lookup"><span data-stu-id="0041a-209">c.</span></span> <span data-ttu-id="0041a-210">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="0041a-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0041a-211">d.</span><span class="sxs-lookup"><span data-stu-id="0041a-211">d.</span></span> <span data-ttu-id="0041a-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0041a-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="0041a-213">Creazione di un utente test di 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="0041a-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="0041a-214">L'applicazione supporta solo in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti verrà creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0041a-214">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0041a-215">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0041a-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0041a-216">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso too123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="0041a-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too123ContactForm.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0041a-218">**tooassign Britta Simon too123ContactForm, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0041a-218">**tooassign Britta Simon too123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="0041a-219">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0041a-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0041a-221">Nell'elenco di applicazioni hello, selezionare **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="0041a-221">In hello applications list, select **123ContactForm**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="0041a-223">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0041a-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0041a-225">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0041a-225">Click **Add** button.</span></span> <span data-ttu-id="0041a-226">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0041a-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0041a-228">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="0041a-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0041a-229">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0041a-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0041a-230">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0041a-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0041a-231">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0041a-231">Testing single sign-on</span></span>

<span data-ttu-id="0041a-232">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0041a-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0041a-233">Quando si fa clic su riquadro 123ContactForm hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour 123ContactForm applicazione.</span><span class="sxs-lookup"><span data-stu-id="0041a-233">When you click hello 123ContactForm tile in hello Access Panel, you should get automatically signed-on tooyour 123ContactForm application.</span></span>
<span data-ttu-id="0041a-234">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0041a-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0041a-235">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0041a-235">Additional resources</span></span>

* [<span data-ttu-id="0041a-236">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0041a-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0041a-237">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0041a-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

