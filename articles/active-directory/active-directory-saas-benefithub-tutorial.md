---
title: 'Esercitazione: Integrazione di Azure Active Directory con BenefitHub | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e BenefitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: c07d6e44e8cbc79afd79c900664011b059206b56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="67973-103">Esercitazione: Integrazione di Azure Active Directory con BenefitHub</span><span class="sxs-lookup"><span data-stu-id="67973-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="67973-104">In questa esercitazione, è illustrato come toointegrate BenefitHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67973-104">In this tutorial, you learn how toointegrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67973-105">Integrazione BenefitHub con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="67973-105">Integrating BenefitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="67973-106">È possibile controllare in Azure AD che ha accesso tooBenefitHub</span><span class="sxs-lookup"><span data-stu-id="67973-106">You can control in Azure AD who has access tooBenefitHub</span></span>
- <span data-ttu-id="67973-107">È possibile abilitare l'utenti tooautomatically get connesso tooBenefitHub (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="67973-107">You can enable your users tooautomatically get signed-on tooBenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67973-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="67973-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="67973-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="67973-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67973-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="67973-110">Prerequisites</span></span>

<span data-ttu-id="67973-111">integrazione di Azure AD con BenefitHub tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="67973-111">tooconfigure Azure AD integration with BenefitHub, you need hello following items:</span></span>

- <span data-ttu-id="67973-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67973-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67973-113">Sottoscrizione di BenefitHub abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="67973-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67973-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="67973-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67973-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="67973-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67973-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="67973-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67973-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67973-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67973-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="67973-118">Scenario description</span></span>
<span data-ttu-id="67973-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="67973-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67973-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="67973-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67973-121">Aggiunta di BenefitHub dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="67973-121">Adding BenefitHub from hello gallery</span></span>
2. <span data-ttu-id="67973-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67973-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-hello-gallery"></a><span data-ttu-id="67973-123">Aggiunta di BenefitHub dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="67973-123">Adding BenefitHub from hello gallery</span></span>
<span data-ttu-id="67973-124">integrazione hello tooconfigure di BenefitHub in Azure AD, è necessario tooadd BenefitHub dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="67973-124">tooconfigure hello integration of BenefitHub into Azure AD, you need tooadd BenefitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="67973-125">**tooadd BenefitHub dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="67973-125">**tooadd BenefitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="67973-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="67973-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="67973-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="67973-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="67973-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="67973-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="67973-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="67973-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="67973-133">Nella casella di ricerca hello, digitare **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="67973-133">In hello search box, type **BenefitHub**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="67973-135">Nel riquadro dei risultati hello, selezionare **BenefitHub**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="67973-135">In hello results panel, select **BenefitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="67973-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67973-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="67973-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BenefitHub usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="67973-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="67973-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in BenefitHub è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67973-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenefitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="67973-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in BenefitHub deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="67973-140">In other words, a link relationship between an Azure AD user and hello related user in BenefitHub needs toobe established.</span></span>

<span data-ttu-id="67973-141">In BenefitHub, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="67973-141">In BenefitHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="67973-142">tooconfigure e prova AD Azure single sign-on con BenefitHub, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="67973-142">tooconfigure and test Azure AD single sign-on with BenefitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="67973-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="67973-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="67973-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67973-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67973-145">**[Creazione di un utente test BenefitHub](#creating-a-benefithub-test-user)**  -toohave un equivalente di Britta Simon in BenefitHub che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="67973-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - toohave a counterpart of Britta Simon in BenefitHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="67973-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="67973-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67973-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="67973-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="67973-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67973-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="67973-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="67973-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="67973-150">**Azure AD tooconfigure single sign-on con BenefitHub, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="67973-150">**tooconfigure Azure AD single sign-on with BenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="67973-151">Nel portale di Azure su hello hello **BenefitHub** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="67973-151">In hello Azure portal, on hello **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="67973-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="67973-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="67973-155">In hello **BenefitHub dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="67973-155">On hello **BenefitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="67973-157">a.</span><span class="sxs-lookup"><span data-stu-id="67973-157">a.</span></span> <span data-ttu-id="67973-158">In hello **identificatore** casella di testo, tipo:`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="67973-158">In hello **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="67973-159">b.</span><span class="sxs-lookup"><span data-stu-id="67973-159">b.</span></span> <span data-ttu-id="67973-160">In hello **URL di risposta** casella di testo, tipo:`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="67973-160">In hello **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="67973-161">Hello BenefitHub applicazione prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="67973-161">hello BenefitHub application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="67973-162">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="67973-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="67973-163">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67973-163">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="67973-165">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine precedente hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="67973-165">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="67973-166">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="67973-166">Attribute Name</span></span> | <span data-ttu-id="67973-167">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="67973-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="67973-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="67973-168">organizationid</span></span> | <span data-ttu-id="67973-169">< id organizzazione ></span><span class="sxs-lookup"><span data-stu-id="67973-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="67973-170">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="67973-170">This attribute value is not real.</span></span> <span data-ttu-id="67973-171">è necessario aggiornare questo valore con l'ID organizzazione effettivo.</span><span class="sxs-lookup"><span data-stu-id="67973-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="67973-172">Contatto [team di supporto BenefitHub](https://www.benefithub.com/Home/ContactUs) tooget hello effettivo OrganizationId valido.</span><span class="sxs-lookup"><span data-stu-id="67973-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) tooget hello actual organizationid.</span></span>
    
    <span data-ttu-id="67973-173">a.</span><span class="sxs-lookup"><span data-stu-id="67973-173">a.</span></span> <span data-ttu-id="67973-174">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="67973-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="67973-177">b.</span><span class="sxs-lookup"><span data-stu-id="67973-177">b.</span></span> <span data-ttu-id="67973-178">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="67973-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="67973-179">c.</span><span class="sxs-lookup"><span data-stu-id="67973-179">c.</span></span> <span data-ttu-id="67973-180">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="67973-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="67973-181">d.</span><span class="sxs-lookup"><span data-stu-id="67973-181">d.</span></span> <span data-ttu-id="67973-182">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="67973-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67973-183">Prima di poter configurare l'asserzione SAML hello, è necessario toocontact il [BenefitHub supporto](https://www.benefithub.com/Home/ContactUs) e valore hello dell'attributo dell'identificatore univoco hello per le richieste per il tenant.</span><span class="sxs-lookup"><span data-stu-id="67973-183">Before you can configure hello SAML assertion, you need toocontact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="67973-184">È necessario l'attestazione personalizzata di hello tooconfigure valore per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67973-184">You need this value tooconfigure hello custom claim for your application.</span></span>

6. <span data-ttu-id="67973-185">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="67973-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="67973-187">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="67973-187">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="67973-189">tooconfigure single sign-on sul **BenefitHub** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="67973-189">tooconfigure single sign-on on **BenefitHub** side, you need toosend hello downloaded **Metadata XML** too[BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="67973-190">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="67973-190">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="67973-191">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="67973-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="67973-192">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="67973-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="67973-193">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="67973-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="67973-194">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67973-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="67973-195">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="67973-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="67973-197">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="67973-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="67973-198">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="67973-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="67973-200">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="67973-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67973-202">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="67973-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67973-204">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="67973-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67973-206">a.</span><span class="sxs-lookup"><span data-stu-id="67973-206">a.</span></span> <span data-ttu-id="67973-207">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="67973-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67973-208">b.</span><span class="sxs-lookup"><span data-stu-id="67973-208">b.</span></span> <span data-ttu-id="67973-209">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="67973-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67973-210">c.</span><span class="sxs-lookup"><span data-stu-id="67973-210">c.</span></span> <span data-ttu-id="67973-211">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="67973-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="67973-212">d.</span><span class="sxs-lookup"><span data-stu-id="67973-212">d.</span></span> <span data-ttu-id="67973-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="67973-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="67973-214">Creazione di un utente di test di BenefitHub</span><span class="sxs-lookup"><span data-stu-id="67973-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="67973-215">In questa sezione viene creato un utente di nome Britta Simon in BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="67973-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="67973-216">Lavorare con [team di supporto BenefitHub](https://www.benefithub.com/Home/ContactUs) per aggiungere gli utenti di hello nella piattaforma BenefitHub hello.</span><span class="sxs-lookup"><span data-stu-id="67973-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add hello users in hello BenefitHub platform.</span></span> <span data-ttu-id="67973-217">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="67973-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="67973-218">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="67973-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="67973-219">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBenefitHub.</span><span class="sxs-lookup"><span data-stu-id="67973-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenefitHub.</span></span>

![Assegna utente][200] 

<span data-ttu-id="67973-221">**tooassign Britta Simon tooBenefitHub, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="67973-221">**tooassign Britta Simon tooBenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="67973-222">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="67973-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="67973-224">Nell'elenco di applicazioni hello, selezionare **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="67973-224">In hello applications list, select **BenefitHub**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="67973-226">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="67973-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="67973-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="67973-228">Click **Add** button.</span></span> <span data-ttu-id="67973-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="67973-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="67973-231">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="67973-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="67973-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="67973-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67973-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="67973-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="67973-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="67973-234">Testing single sign-on</span></span>

<span data-ttu-id="67973-235">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="67973-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="67973-236">Quando si fa clic su riquadro BenefitHub hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour BenefitHub applicazione.</span><span class="sxs-lookup"><span data-stu-id="67973-236">When you click hello BenefitHub tile in hello Access Panel, you should get automatically signed-on tooyour BenefitHub application.</span></span>
<span data-ttu-id="67973-237">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="67973-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="67973-238">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="67973-238">Additional resources</span></span>

* [<span data-ttu-id="67973-239">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67973-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67973-240">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67973-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

