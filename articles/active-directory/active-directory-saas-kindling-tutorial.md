---
title: 'Esercitazione: integrazione di Azure Active Directory con Kindling | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Kindling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 32ad6116c2690aea2060a2dd56e052f233ad7ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="f5a76-103">Esercitazione: integrazione di Azure Active Directory con Kindling</span><span class="sxs-lookup"><span data-stu-id="f5a76-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="f5a76-104">In questa esercitazione, è illustrato come toointegrate Kindling con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5a76-104">In this tutorial, you learn how toointegrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5a76-105">Integrazione Kindling con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f5a76-105">Integrating Kindling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f5a76-106">È possibile controllare in Azure AD che ha accesso tooKindling</span><span class="sxs-lookup"><span data-stu-id="f5a76-106">You can control in Azure AD who has access tooKindling</span></span>
- <span data-ttu-id="f5a76-107">È possibile abilitare l'utenti tooautomatically get connesso tooKindling (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a76-107">You can enable your users tooautomatically get signed-on tooKindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5a76-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f5a76-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f5a76-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere.</span><span class="sxs-lookup"><span data-stu-id="f5a76-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="f5a76-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5a76-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5a76-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f5a76-111">Prerequisites</span></span>

<span data-ttu-id="f5a76-112">integrazione di Azure AD tooconfigure con Kindling, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f5a76-112">tooconfigure Azure AD integration with Kindling, you need hello following items:</span></span>

- <span data-ttu-id="f5a76-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5a76-113">An Azure AD subscription</span></span>
- <span data-ttu-id="f5a76-114">Sottoscrizione di Kindling abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f5a76-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5a76-115">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f5a76-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5a76-116">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f5a76-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5a76-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f5a76-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5a76-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5a76-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5a76-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f5a76-119">Scenario description</span></span>
<span data-ttu-id="f5a76-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f5a76-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5a76-121">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f5a76-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5a76-122">Aggiunta di Kindling dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f5a76-122">Adding Kindling from hello gallery</span></span>
2. <span data-ttu-id="f5a76-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a76-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-hello-gallery"></a><span data-ttu-id="f5a76-124">Aggiunta di Kindling dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f5a76-124">Adding Kindling from hello gallery</span></span>
<span data-ttu-id="f5a76-125">integrazione di hello tooconfigure di Kindling in Azure AD, è necessario tooadd Kindling dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f5a76-125">tooconfigure hello integration of Kindling into Azure AD, you need tooadd Kindling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f5a76-126">**tooadd Kindling dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f5a76-126">**tooadd Kindling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5a76-127">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f5a76-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5a76-129">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f5a76-130">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-130">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f5a76-132">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f5a76-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f5a76-134">Nella casella di ricerca hello, digitare **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-134">In hello search box, type **Kindling**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="f5a76-136">Nel riquadro dei risultati hello, selezionare **Kindling**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f5a76-136">In hello results panel, select **Kindling**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5a76-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a76-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5a76-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kindling mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f5a76-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f5a76-140">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Kindling è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5a76-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kindling is tooa user in Azure AD.</span></span> <span data-ttu-id="f5a76-141">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Kindling esigenze toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f5a76-141">In other words, a link relationship between an Azure AD user and hello related user in Kindling needs toobe established.</span></span>

<span data-ttu-id="f5a76-142">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Kindling.</span><span class="sxs-lookup"><span data-stu-id="f5a76-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Kindling.</span></span>

<span data-ttu-id="f5a76-143">tooconfigure e prova AD Azure single sign-on con Kindling, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f5a76-143">tooconfigure and test Azure AD single sign-on with Kindling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f5a76-144">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f5a76-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f5a76-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5a76-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5a76-146">**[Creazione di un utente test Kindling](#creating-a-kindling-test-user)**  -toohave un equivalente di Britta Simon in Kindling che è collegato AD Azure toohello rappresentazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f5a76-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - toohave a counterpart of Britta Simon in Kindling that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5a76-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f5a76-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5a76-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f5a76-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5a76-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a76-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5a76-150">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Kindling.</span><span class="sxs-lookup"><span data-stu-id="f5a76-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="f5a76-151">**tooconfigure AD Azure single sign-on con Kindling, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f5a76-151">**tooconfigure Azure AD single sign-on with Kindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5a76-152">Nel portale di Azure su hello hello **Kindling** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-152">In hello Azure portal, on hello **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f5a76-154">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f5a76-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="f5a76-156">In hello **Kindling dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f5a76-156">On hello **Kindling Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="f5a76-158">a.</span><span class="sxs-lookup"><span data-stu-id="f5a76-158">a.</span></span> <span data-ttu-id="f5a76-159">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="f5a76-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="f5a76-160">b.</span><span class="sxs-lookup"><span data-stu-id="f5a76-160">b.</span></span>  <span data-ttu-id="f5a76-161">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="f5a76-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5a76-162">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="f5a76-162">These values are not hello real.</span></span> <span data-ttu-id="f5a76-163">Aggiornare questi valori con URL hello effettivo Sign-on e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="f5a76-163">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="f5a76-164">Contatto [team di supporto Kindling](mailto:support@kindlingapp.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="f5a76-164">Contact [Kindling support team](mailto:support@kindlingapp.com) tooget these values.</span></span>
 
4. <span data-ttu-id="f5a76-165">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f5a76-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="f5a76-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f5a76-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f5a76-169">In hello **Kindling configurazione** fare clic su **configurare Kindling** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="f5a76-169">On hello **Kindling Configuration** section, click **Configure Kindling** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f5a76-170">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f5a76-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="f5a76-172">tooconfigure single sign-on sul **Kindling** lato, è necessario hello toosend scaricato **certificato (Base64)**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL**troppo[team di supporto Kindling](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="f5a76-172">tooconfigure single sign-on on **Kindling** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="f5a76-173">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="f5a76-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f5a76-174">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="f5a76-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f5a76-175">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f5a76-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5a76-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a76-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5a76-177">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f5a76-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f5a76-179">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f5a76-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5a76-180">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f5a76-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5a76-182">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5a76-184">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f5a76-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5a76-186">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f5a76-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5a76-188">a.</span><span class="sxs-lookup"><span data-stu-id="f5a76-188">a.</span></span> <span data-ttu-id="f5a76-189">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5a76-190">b.</span><span class="sxs-lookup"><span data-stu-id="f5a76-190">b.</span></span> <span data-ttu-id="f5a76-191">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f5a76-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5a76-192">c.</span><span class="sxs-lookup"><span data-stu-id="f5a76-192">c.</span></span> <span data-ttu-id="f5a76-193">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f5a76-194">d.</span><span class="sxs-lookup"><span data-stu-id="f5a76-194">d.</span></span> <span data-ttu-id="f5a76-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="f5a76-196">Creazione di un utente test di Kindling</span><span class="sxs-lookup"><span data-stu-id="f5a76-196">Creating a Kindling test user</span></span>

<span data-ttu-id="f5a76-197">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Kindling toocreate.</span><span class="sxs-lookup"><span data-stu-id="f5a76-197">hello objective of this section is toocreate a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="f5a76-198">Kindling supporta il provisioning just-in-time.</span><span class="sxs-lookup"><span data-stu-id="f5a76-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="f5a76-199">È già stato abilitato in [Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="f5a76-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="f5a76-200">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="f5a76-200">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f5a76-201">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a76-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f5a76-202">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooKindling.</span><span class="sxs-lookup"><span data-stu-id="f5a76-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKindling.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f5a76-204">**tooassign Britta Simon tooKindling, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f5a76-204">**tooassign Britta Simon tooKindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5a76-205">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f5a76-207">Nell'elenco di applicazioni hello, selezionare **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-207">In hello applications list, select **Kindling**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="f5a76-209">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f5a76-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-211">Click **Add** button.</span></span> <span data-ttu-id="f5a76-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f5a76-214">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f5a76-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f5a76-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5a76-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f5a76-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5a76-217">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f5a76-217">Testing single sign-on</span></span>

<span data-ttu-id="f5a76-218">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f5a76-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f5a76-219">Quando si fa clic su riquadro Kindling hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Kindling applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5a76-219">When you click hello Kindling tile in hello Access Panel, you should get automatically signed-on tooyour Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f5a76-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f5a76-220">Additional resources</span></span>

* [<span data-ttu-id="f5a76-221">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5a76-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5a76-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5a76-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

