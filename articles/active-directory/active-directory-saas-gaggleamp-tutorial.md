---
title: 'Esercitazione: Integrazione di Azure Active Directory con GaggleAMP | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e GaggleAMP.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9761019a79f935b6695a5ae1214c256c887df457
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="4eba2-103">Esercitazione: Integrazione di Azure Active Directory con GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="4eba2-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="4eba2-104">In questa esercitazione, è illustrato come toointegrate GaggleAMP con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4eba2-104">In this tutorial, you learn how toointegrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4eba2-105">Integrazione GaggleAMP con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4eba2-105">Integrating GaggleAMP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4eba2-106">È possibile controllare in Azure AD che ha accesso tooGaggleAMP</span><span class="sxs-lookup"><span data-stu-id="4eba2-106">You can control in Azure AD who has access tooGaggleAMP</span></span>
- <span data-ttu-id="4eba2-107">È possibile abilitare l'utenti tooautomatically get connesso tooGaggleAMP (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4eba2-107">You can enable your users tooautomatically get signed-on tooGaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4eba2-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4eba2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4eba2-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4eba2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4eba2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4eba2-110">Prerequisites</span></span>

<span data-ttu-id="4eba2-111">integrazione di Azure AD con GaggleAMP tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4eba2-111">tooconfigure Azure AD integration with GaggleAMP, you need hello following items:</span></span>

- <span data-ttu-id="4eba2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4eba2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4eba2-113">Sottoscrizione di GaggleAMP abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4eba2-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4eba2-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4eba2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4eba2-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4eba2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4eba2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4eba2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4eba2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4eba2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4eba2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4eba2-118">Scenario description</span></span>
<span data-ttu-id="4eba2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4eba2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4eba2-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4eba2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4eba2-121">Aggiunta di GaggleAMP dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4eba2-121">Adding GaggleAMP from hello gallery</span></span>
2. <span data-ttu-id="4eba2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4eba2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-hello-gallery"></a><span data-ttu-id="4eba2-123">Aggiunta di GaggleAMP dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4eba2-123">Adding GaggleAMP from hello gallery</span></span>
<span data-ttu-id="4eba2-124">integrazione hello tooconfigure di GaggleAMP in Azure AD, è necessario tooadd GaggleAMP dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4eba2-124">tooconfigure hello integration of GaggleAMP into Azure AD, you need tooadd GaggleAMP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4eba2-125">**tooadd GaggleAMP dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4eba2-125">**tooadd GaggleAMP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4eba2-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4eba2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4eba2-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4eba2-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4eba2-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4eba2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4eba2-133">Nella casella di ricerca hello, digitare **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-133">In hello search box, type **GaggleAMP**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="4eba2-135">Nel riquadro dei risultati hello, selezionare **GaggleAMP**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4eba2-135">In hello results panel, select **GaggleAMP**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4eba2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4eba2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4eba2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con GaggleAMP mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4eba2-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4eba2-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in GaggleAMP è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4eba2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GaggleAMP is tooa user in Azure AD.</span></span> <span data-ttu-id="4eba2-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in GaggleAMP deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4eba2-140">In other words, a link relationship between an Azure AD user and hello related user in GaggleAMP needs toobe established.</span></span>

<span data-ttu-id="4eba2-141">In GaggleAMP, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4eba2-141">In GaggleAMP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4eba2-142">tooconfigure e prova AD Azure single sign-on con GaggleAMP, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4eba2-142">tooconfigure and test Azure AD single sign-on with GaggleAMP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4eba2-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4eba2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4eba2-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4eba2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4eba2-145">**[Creazione di un utente test GaggleAMP](#creating-a-gaggleamp-test-user)**  -toohave un equivalente di Britta Simon in GaggleAMP che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4eba2-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - toohave a counterpart of Britta Simon in GaggleAMP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4eba2-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4eba2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4eba2-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4eba2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4eba2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4eba2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4eba2-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="4eba2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="4eba2-150">**Azure AD tooconfigure single sign-on con GaggleAMP, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4eba2-150">**tooconfigure Azure AD single sign-on with GaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="4eba2-151">Nel portale di Azure su hello hello **GaggleAMP** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-151">In hello Azure portal, on hello **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4eba2-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4eba2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="4eba2-155">In hello **GaggleAMP dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4eba2-155">On hello **GaggleAMP Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="4eba2-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="4eba2-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4eba2-158">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="4eba2-158">hello value is not real.</span></span> <span data-ttu-id="4eba2-159">Il valore di hello aggiornamento con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4eba2-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4eba2-160">Contatto [team di supporto GaggleAMP Client](mailto:sales@gaggleamp.com) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="4eba2-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="4eba2-161">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4eba2-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="4eba2-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4eba2-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4eba2-165">In hello **GaggleAMP configurazione** fare clic su **configurare GaggleAMP** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="4eba2-165">On hello **GaggleAMP Configuration** section, click **Configure GaggleAMP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4eba2-166">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4eba2-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="4eba2-168">In un'altra istanza del browser, passare toohello pagina SAML SSO creato per team di supporto dal hello ad (ad esempio: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="4eba2-168">In another browser instance, navigate toohello SAML SSO page created for you by hello Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="4eba2-169">Nel **SAML SSO** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4eba2-169">On your **SAML SSO** page, perform hello following steps:</span></span>  
   
    ![Accesso Single Sign-On di GaggleAMP](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="4eba2-171">a.</span><span class="sxs-lookup"><span data-stu-id="4eba2-171">a.</span></span> <span data-ttu-id="4eba2-172">In hello **Identity Provider Issuer** casella di testo, hello Incolla valore **URL autorità di certificazione** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4eba2-172">In hello **Identity Provider Issuer** textbox, paste hello value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="4eba2-173">b.</span><span class="sxs-lookup"><span data-stu-id="4eba2-173">b.</span></span> <span data-ttu-id="4eba2-174">In hello **Identity Provider Single Sign-On URL** casella di testo, hello Incolla valore **URL servizio Single Sign-On** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4eba2-174">In hello **Identity Provider Single Sign-On URL** textbox, paste hello  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4eba2-175">c.</span><span class="sxs-lookup"><span data-stu-id="4eba2-175">c.</span></span> <span data-ttu-id="4eba2-176">Fare clic su **Save**</span><span class="sxs-lookup"><span data-stu-id="4eba2-176">Click **Save**</span></span>      

    <span data-ttu-id="4eba2-177">d.</span><span class="sxs-lookup"><span data-stu-id="4eba2-177">d.</span></span> <span data-ttu-id="4eba2-178">Inviare hello **certificato (Base64)** certificato tooyour [team di supporto GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="4eba2-178">Send hello **Certificate (Base64)** certificate tooyour [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="4eba2-179">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4eba2-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4eba2-180">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4eba2-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4eba2-181">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4eba2-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4eba2-182">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4eba2-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="4eba2-183">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4eba2-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4eba2-185">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4eba2-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4eba2-186">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4eba2-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4eba2-188">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4eba2-190">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4eba2-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4eba2-192">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4eba2-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4eba2-194">a.</span><span class="sxs-lookup"><span data-stu-id="4eba2-194">a.</span></span> <span data-ttu-id="4eba2-195">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4eba2-196">b.</span><span class="sxs-lookup"><span data-stu-id="4eba2-196">b.</span></span> <span data-ttu-id="4eba2-197">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4eba2-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4eba2-198">c.</span><span class="sxs-lookup"><span data-stu-id="4eba2-198">c.</span></span> <span data-ttu-id="4eba2-199">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4eba2-200">d.</span><span class="sxs-lookup"><span data-stu-id="4eba2-200">d.</span></span> <span data-ttu-id="4eba2-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="4eba2-202">Creazione di un utente di test di GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="4eba2-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="4eba2-203">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in GaggleAMP toocreate.</span><span class="sxs-lookup"><span data-stu-id="4eba2-203">hello objective of this section is toocreate a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="4eba2-204">GaggleAMP supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4eba2-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4eba2-205">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="4eba2-205">There is no action item for you in this section.</span></span> <span data-ttu-id="4eba2-206">Se non esiste ancora, durante un tooaccess tentativo GaggleAMP viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="4eba2-206">A new user is created during an attempt tooaccess GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4eba2-207">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4eba2-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4eba2-208">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooGaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="4eba2-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGaggleAMP.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4eba2-210">**tooassign Britta Simon tooGaggleAMP, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4eba2-210">**tooassign Britta Simon tooGaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="4eba2-211">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4eba2-213">Nell'elenco di applicazioni hello, selezionare **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-213">In hello applications list, select **GaggleAMP**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="4eba2-215">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4eba2-217">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-217">Click **Add** button.</span></span> <span data-ttu-id="4eba2-218">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4eba2-220">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4eba2-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4eba2-221">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4eba2-222">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4eba2-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4eba2-223">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4eba2-223">Testing single sign-on</span></span>

<span data-ttu-id="4eba2-224">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4eba2-224">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4eba2-225">Quando si fa clic su riquadro GaggleAMP hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour GaggleAMP applicazione.</span><span class="sxs-lookup"><span data-stu-id="4eba2-225">When you click hello GaggleAMP tile in hello Access Panel, you should get automatically signed-on tooyour GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4eba2-226">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4eba2-226">Additional resources</span></span>

* [<span data-ttu-id="4eba2-227">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4eba2-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4eba2-228">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4eba2-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

