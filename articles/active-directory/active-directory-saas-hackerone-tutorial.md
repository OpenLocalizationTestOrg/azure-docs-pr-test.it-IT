---
title: 'Esercitazione: Integrazione di Azure Active Directory con HackerOne | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Hackerone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: c9dc033e26e79a7233dcfb3899c62684d4a19652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="af185-103">Esercitazione: Integrazione di Azure Active Directory con HackerOne</span><span class="sxs-lookup"><span data-stu-id="af185-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="af185-104">In questa esercitazione, è illustrato come toointegrate HackerOne con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af185-104">In this tutorial, you learn how toointegrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="af185-105">Integrazione HackerOne con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="af185-105">Integrating HackerOne with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="af185-106">È possibile controllare in Azure AD che ha accesso tooHackerOne</span><span class="sxs-lookup"><span data-stu-id="af185-106">You can control in Azure AD who has access tooHackerOne</span></span>
- <span data-ttu-id="af185-107">È possibile abilitare l'utenti tooautomatically get connesso tooHackerOne (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="af185-107">You can enable your users tooautomatically get signed-on tooHackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="af185-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="af185-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="af185-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="af185-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af185-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="af185-110">Prerequisites</span></span>

<span data-ttu-id="af185-111">integrazione di Azure AD con HackerOne tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="af185-111">tooconfigure Azure AD integration with HackerOne, you need hello following items:</span></span>

- <span data-ttu-id="af185-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af185-112">An Azure AD subscription</span></span>
- <span data-ttu-id="af185-113">Sottoscrizione di HackerOne abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="af185-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="af185-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="af185-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="af185-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="af185-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="af185-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="af185-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="af185-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="af185-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="af185-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="af185-118">Scenario description</span></span>
<span data-ttu-id="af185-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="af185-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="af185-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="af185-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="af185-121">Aggiunta di HackerOne dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="af185-121">Adding HackerOne from hello gallery</span></span>
2. <span data-ttu-id="af185-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af185-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-hello-gallery"></a><span data-ttu-id="af185-123">Aggiunta di HackerOne dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="af185-123">Adding HackerOne from hello gallery</span></span>
<span data-ttu-id="af185-124">integrazione hello tooconfigure di HackerOne in Azure AD, è necessario tooadd HackerOne dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="af185-124">tooconfigure hello integration of HackerOne into Azure AD, you need tooadd HackerOne from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="af185-125">**tooadd HackerOne dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af185-125">**tooadd HackerOne from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="af185-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="af185-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="af185-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="af185-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="af185-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="af185-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="af185-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="af185-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="af185-133">Nella casella di ricerca hello, digitare **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="af185-133">In hello search box, type **HackerOne**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="af185-135">Nel riquadro dei risultati hello, selezionare **HackerOne**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="af185-135">In hello results panel, select **HackerOne**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="af185-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af185-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="af185-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con HackerOne usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="af185-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="af185-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in HackerOne è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af185-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HackerOne is tooa user in Azure AD.</span></span> <span data-ttu-id="af185-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in HackerOne deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="af185-140">In other words, a link relationship between an Azure AD user and hello related user in HackerOne needs toobe established.</span></span>

<span data-ttu-id="af185-141">In HackerOne, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="af185-141">In HackerOne, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="af185-142">tooconfigure e prova AD Azure single sign-on con HackerOne, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="af185-142">tooconfigure and test Azure AD single sign-on with HackerOne, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="af185-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="af185-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="af185-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af185-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="af185-145">**[Creazione di un utente test HackerOne](#creating-a-hackerone-test-user)**  -toohave un equivalente di Britta Simon in HackerOne che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="af185-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - toohave a counterpart of Britta Simon in HackerOne that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="af185-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="af185-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="af185-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="af185-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="af185-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af185-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="af185-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione HackerOne.</span><span class="sxs-lookup"><span data-stu-id="af185-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="af185-150">**Azure AD tooconfigure single sign-on con HackerOne, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af185-150">**tooconfigure Azure AD single sign-on with HackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="af185-151">Nel portale di Azure su hello hello **HackerOne** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="af185-151">In hello Azure portal, on hello **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="af185-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="af185-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="af185-155">In hello **HackerOne Single sign-on URL e l'identificatore** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af185-155">On hello **HackerOne Single sign-on URL and Identifier** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="af185-157">a.</span><span class="sxs-lookup"><span data-stu-id="af185-157">a.</span></span> <span data-ttu-id="af185-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="af185-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="af185-159">b.</span><span class="sxs-lookup"><span data-stu-id="af185-159">b.</span></span> <span data-ttu-id="af185-160">In hello **identificatore** casella di testo, digitare un URL come:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="af185-160">In hello **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="af185-161">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="af185-161">This value is not real.</span></span> <span data-ttu-id="af185-162">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="af185-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="af185-163">Contatto [team di supporto HackerOne](mailto:support@hackerone.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="af185-163">Contact [HackerOne support team](mailto:support@hackerone.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="af185-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="af185-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="af185-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="af185-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="af185-168">In hello **HackerOne configurazione** fare clic su **configurare HackerOne** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="af185-168">On hello **HackerOne Configuration** section, click **Configure HackerOne** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="af185-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="af185-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="af185-171">Sign On tooyour HackerOne tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="af185-171">Sign On tooyour HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="af185-172">Scegliere hello hello menu in alto hello "**impostazioni**."</span><span class="sxs-lookup"><span data-stu-id="af185-172">In hello menu on hello top, click hello "**Settings**."</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="af185-174">Passare troppo"**autenticazione**"e fare clic su"**aggiungere impostazioni di SAML**."</span><span class="sxs-lookup"><span data-stu-id="af185-174">Navigate too"**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="af185-176">In hello **impostazioni SAML** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af185-176">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="af185-178">a.</span><span class="sxs-lookup"><span data-stu-id="af185-178">a.</span></span> <span data-ttu-id="af185-179">In hello **dominio di posta elettronica** casella di testo, digitare un dominio registrato.</span><span class="sxs-lookup"><span data-stu-id="af185-179">In hello **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="af185-180">b.</span><span class="sxs-lookup"><span data-stu-id="af185-180">b.</span></span> <span data-ttu-id="af185-181">In **Single Sign On URL** nelle caselle di testo, incollare il valore di hello di **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="af185-181">In  **Single Sign On URL** textboxes, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="af185-182">c.</span><span class="sxs-lookup"><span data-stu-id="af185-182">c.</span></span> <span data-ttu-id="af185-183">Aprire il **file di certificato** nel blocco note scaricato dal portale di Azure, copiarne contenuto hello negli Appunti e quindi incollarlo toohello **certificato X509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="af185-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="af185-184">d.</span><span class="sxs-lookup"><span data-stu-id="af185-184">d.</span></span> <span data-ttu-id="af185-185">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="af185-185">Click **Save**.</span></span>

11. <span data-ttu-id="af185-186">Nella finestra di dialogo Impostazioni di autenticazione hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af185-186">On hello Authentication Settings dialog, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="af185-188">a.</span><span class="sxs-lookup"><span data-stu-id="af185-188">a.</span></span> <span data-ttu-id="af185-189">Fare clic su **Run test**(Esegui test).</span><span class="sxs-lookup"><span data-stu-id="af185-189">Click **Run test**.</span></span>

    <span data-ttu-id="af185-190">b.</span><span class="sxs-lookup"><span data-stu-id="af185-190">b.</span></span> <span data-ttu-id="af185-191">Se hello valore hello **stato** campo uguale a **ultimo stato di test: creato**, contattare il [team di supporto HackerOne](mailto:support@hackerone.com) toorequest una revisione della configurazione.</span><span class="sxs-lookup"><span data-stu-id="af185-191">If hello value of hello **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) toorequest a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="af185-192">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="af185-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="af185-193">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="af185-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="af185-194">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="af185-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="af185-195">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af185-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="af185-196">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="af185-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="af185-198">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af185-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="af185-199">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="af185-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="af185-201">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="af185-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="af185-203">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="af185-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="af185-205">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af185-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="af185-207">a.</span><span class="sxs-lookup"><span data-stu-id="af185-207">a.</span></span> <span data-ttu-id="af185-208">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="af185-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="af185-209">b.</span><span class="sxs-lookup"><span data-stu-id="af185-209">b.</span></span> <span data-ttu-id="af185-210">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="af185-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="af185-211">c.</span><span class="sxs-lookup"><span data-stu-id="af185-211">c.</span></span> <span data-ttu-id="af185-212">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="af185-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="af185-213">d.</span><span class="sxs-lookup"><span data-stu-id="af185-213">d.</span></span> <span data-ttu-id="af185-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="af185-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="af185-215">Creazione di un utente test di HackerOne</span><span class="sxs-lookup"><span data-stu-id="af185-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="af185-216">Successivamente, viene creato un utente chiamato Britta Simon in HackerOne.</span><span class="sxs-lookup"><span data-stu-id="af185-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="af185-217">HackerOne supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="af185-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="af185-218">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="af185-218">There is no action item for you in this section.</span></span> <span data-ttu-id="af185-219">Quando si accede a HackerOne, viene creato un nuovo utente se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="af185-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="af185-220">Se è necessario un utente toocreate manualmente, è necessario team di supporto Certify toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="af185-220">If you need toocreate a user manually, you need toocontact hello Certify support team.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="af185-221">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="af185-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="af185-222">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHackerOne.</span><span class="sxs-lookup"><span data-stu-id="af185-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHackerOne.</span></span>

![Assegna utente][200] 

<span data-ttu-id="af185-224">**tooassign Britta Simon tooHackerOne, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af185-224">**tooassign Britta Simon tooHackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="af185-225">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="af185-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="af185-227">Nell'elenco di applicazioni hello, selezionare **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="af185-227">In hello applications list, select **HackerOne**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="af185-229">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="af185-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="af185-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="af185-231">Click **Add** button.</span></span> <span data-ttu-id="af185-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="af185-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="af185-234">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="af185-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="af185-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="af185-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="af185-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="af185-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="af185-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="af185-237">Testing single sign-on</span></span>

<span data-ttu-id="af185-238">Infine, test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="af185-238">Finally, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="af185-239">Quando si fa clic su riquadro HackerOne hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour HackerOne applicazione.</span><span class="sxs-lookup"><span data-stu-id="af185-239">When you click hello HackerOne tile in hello Access Panel, you should get automatically signed-on tooyour HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af185-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="af185-240">Additional resources</span></span>

* [<span data-ttu-id="af185-241">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af185-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="af185-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af185-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

