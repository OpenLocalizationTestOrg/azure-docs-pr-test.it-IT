---
title: 'Esercitazione: Integrazione di Azure Active Directory con CA PPM | Documentazione Microsoft'
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e PPM autorità di certificazione."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 571130f3be0529c986aa0d8a08e4172015cd0b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="a2ac2-103">Esercitazione: Integrazione di Azure Active Directory con CA PPM</span><span class="sxs-lookup"><span data-stu-id="a2ac2-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>

<span data-ttu-id="a2ac2-104">In questa esercitazione, è illustrato come toointegrate PPM CA con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2ac2-104">In this tutorial, you learn how toointegrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2ac2-105">Integrazione di PPM CA con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="a2ac2-105">Integrating CA PPM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2ac2-106">È possibile controllare in Azure AD che ha accesso tooCA PPM</span><span class="sxs-lookup"><span data-stu-id="a2ac2-106">You can control in Azure AD who has access tooCA PPM</span></span>
- <span data-ttu-id="a2ac2-107">È possibile abilitare l'utenti tooautomatically get connesso tooCA PPM (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2ac2-107">You can enable your users tooautomatically get signed-on tooCA PPM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2ac2-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a2ac2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2ac2-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2ac2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2ac2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a2ac2-110">Prerequisites</span></span>

<span data-ttu-id="a2ac2-111">integrazione di Azure AD con autorità di certificazione PPM tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="a2ac2-111">tooconfigure Azure AD integration with CA PPM, you need hello following items:</span></span>

- <span data-ttu-id="a2ac2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2ac2-113">Sottoscrizione di CA PPM abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a2ac2-113">A CA PPM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2ac2-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2ac2-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="a2ac2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2ac2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2ac2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2ac2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2ac2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a2ac2-118">Scenario description</span></span>
<span data-ttu-id="a2ac2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2ac2-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="a2ac2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2ac2-121">Aggiunta di PPM CA dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a2ac2-121">Adding CA PPM from hello gallery</span></span>
2. <span data-ttu-id="a2ac2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2ac2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ca-ppm-from-hello-gallery"></a><span data-ttu-id="a2ac2-123">Aggiunta di PPM CA dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a2ac2-123">Adding CA PPM from hello gallery</span></span>
<span data-ttu-id="a2ac2-124">integrazione hello tooconfigure di PPM CA in Azure AD, è necessario tooadd PPM autorità di certificazione dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-124">tooconfigure hello integration of CA PPM into Azure AD, you need tooadd CA PPM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2ac2-125">**tooadd PPM CA dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a2ac2-125">**tooadd CA PPM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2ac2-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2ac2-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2ac2-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a2ac2-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a2ac2-133">Nella casella di ricerca hello, digitare **PPM CA**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-133">In hello search box, type **CA PPM**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. <span data-ttu-id="a2ac2-135">Nel riquadro dei risultati hello, selezionare **PPM CA**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-135">In hello results panel, select **CA PPM**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2ac2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2ac2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2ac2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con CA PPM usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a2ac2-138">In this section, you configure and test Azure AD single sign-on with CA PPM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2ac2-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Autorità di certificazione PPM è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CA PPM is tooa user in Azure AD.</span></span> <span data-ttu-id="a2ac2-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Autorità di certificazione PPM deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-140">In other words, a link relationship between an Azure AD user and hello related user in CA PPM needs toobe established.</span></span>

<span data-ttu-id="a2ac2-141">In Canada PPM, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-141">In CA PPM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a2ac2-142">tooconfigure e prova AD Azure single sign-on con PPM CA, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="a2ac2-142">tooconfigure and test Azure AD single sign-on with CA PPM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2ac2-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2ac2-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2ac2-145">**[Creazione di un utente test PPM CA](#creating-a-ca-ppm-test-user)**  -toohave un equivalente di Britta Simon in PPM autorità di certificazione che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-145">**[Creating a CA PPM test user](#creating-a-ca-ppm-test-user)** - toohave a counterpart of Britta Simon in CA PPM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2ac2-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2ac2-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2ac2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2ac2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2ac2-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione PPM autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CA PPM application.</span></span>

<span data-ttu-id="a2ac2-150">**Azure AD tooconfigure single sign-on con PPM CA, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a2ac2-150">**tooconfigure Azure AD single sign-on with CA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2ac2-151">Nel portale di Azure su hello hello **PPM CA** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-151">In hello Azure portal, on hello **CA PPM** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a2ac2-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. <span data-ttu-id="a2ac2-155">In hello **dominio PPM Canada e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a2ac2-155">On hello **CA PPM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    <span data-ttu-id="a2ac2-157">a.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-157">a.</span></span> <span data-ttu-id="a2ac2-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://ca.ondemand.saml.20.post.<companyname>`</span><span class="sxs-lookup"><span data-stu-id="a2ac2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://ca.ondemand.saml.20.post.<companyname>`</span></span>
    
    <span data-ttu-id="a2ac2-159">b.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-159">b.</span></span> <span data-ttu-id="a2ac2-160">In hello **URL di risposta** casella di testo, tipo:`https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="a2ac2-160">In hello **Reply URL** textbox, type as: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2ac2-161">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="a2ac2-161">This value is not real.</span></span> <span data-ttu-id="a2ac2-162">Aggiorna il valore con hello identificatore effettivo.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="a2ac2-163">Contatto [team di supporto CA PPM](mailto:catechnicalsupport@ca.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-163">Contact [CA PPM support team](mailto:catechnicalsupport@ca.com) tooget this value.</span></span>
 
4. <span data-ttu-id="a2ac2-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. <span data-ttu-id="a2ac2-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a2ac2-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2ac2-168">In hello **configurazione PPM CA** fare clic su **configurare CA PPM** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-168">On hello **CA PPM Configuration** section, click **Configure CA PPM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a2ac2-169">Hello copia **ID entità SAML** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="a2ac2-169">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. <span data-ttu-id="a2ac2-171">tooconfigure single sign-on sul **PPM CA** lato, è necessario hello toosend scaricato **Certificate(Base64)** e **ID entità SAML** troppo[team di supporto PPM CA ](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="a2ac2-171">tooconfigure single sign-on on **CA PPM** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Entity ID** too[CA PPM support team](mailto:catechnicalsupport@ca.com).</span></span>

> [!TIP]
> <span data-ttu-id="a2ac2-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="a2ac2-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a2ac2-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a2ac2-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2ac2-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2ac2-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2ac2-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2ac2-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a2ac2-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a2ac2-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2ac2-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2ac2-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2ac2-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2ac2-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a2ac2-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2ac2-187">a.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-187">a.</span></span> <span data-ttu-id="a2ac2-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2ac2-189">b.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-189">b.</span></span> <span data-ttu-id="a2ac2-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2ac2-191">c.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-191">c.</span></span> <span data-ttu-id="a2ac2-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2ac2-193">d.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-193">d.</span></span> <span data-ttu-id="a2ac2-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-194">Click **Create**.</span></span>
 
### <a name="creating-a-ca-ppm-test-user"></a><span data-ttu-id="a2ac2-195">Creazione di un utente di test di CA PPM</span><span class="sxs-lookup"><span data-stu-id="a2ac2-195">Creating a CA PPM test user</span></span>

<span data-ttu-id="a2ac2-196">In questa sezione viene creato un utente di nome Britta Simon in CA PPM.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-196">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="a2ac2-197">Lavorare con [team di supporto CA PPM](mailto:catechnicalsupport@ca.com) utenti hello tooadd nella piattaforma di autorità di certificazione PPM hello.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-197">Work with [CA PPM support team](mailto:catechnicalsupport@ca.com) tooadd hello users in hello CA PPM platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2ac2-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2ac2-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2ac2-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCA PPM.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCA PPM.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a2ac2-201">**tooassign Britta Simon tooCA PPM, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a2ac2-201">**tooassign Britta Simon tooCA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2ac2-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a2ac2-204">Nell'elenco di applicazioni hello, selezionare **PPM CA**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-204">In hello applications list, select **CA PPM**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. <span data-ttu-id="a2ac2-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a2ac2-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-208">Click **Add** button.</span></span> <span data-ttu-id="a2ac2-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a2ac2-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2ac2-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2ac2-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2ac2-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a2ac2-214">Testing single sign-on</span></span>

<span data-ttu-id="a2ac2-215">In questa sezione è verificare la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-215">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a2ac2-216">Quando si fa clic su riquadro CA PPM hello in hello Pannello di accesso, è necessario ottenere applicazione PPM CA tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="a2ac2-216">When you click hello CA PPM tile in hello Access Panel, you should get automatically signed-on tooyour CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2ac2-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a2ac2-217">Additional resources</span></span>

* [<span data-ttu-id="a2ac2-218">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2ac2-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2ac2-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2ac2-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png

