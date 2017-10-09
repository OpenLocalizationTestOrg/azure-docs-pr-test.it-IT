---
title: 'Esercitazione: Integrazione di Azure Active Directory con IdeaScale | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e IdeaScale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="cc1da-103">Esercitazione: Integrazione di Azure Active Directory con IdeaScale</span><span class="sxs-lookup"><span data-stu-id="cc1da-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="cc1da-104">In questa esercitazione, è illustrato come toointegrate IdeaScale con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc1da-104">In this tutorial, you learn how toointegrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc1da-105">Integrazione di IdeaScale con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="cc1da-105">Integrating IdeaScale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc1da-106">È possibile controllare in Azure AD che ha accesso tooIdeaScale</span><span class="sxs-lookup"><span data-stu-id="cc1da-106">You can control in Azure AD who has access tooIdeaScale</span></span>
- <span data-ttu-id="cc1da-107">È possibile abilitare l'utenti tooautomatically get connesso tooIdeaScale (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1da-107">You can enable your users tooautomatically get signed-on tooIdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc1da-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cc1da-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cc1da-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc1da-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc1da-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cc1da-110">Prerequisites</span></span>

<span data-ttu-id="cc1da-111">integrazione di Azure AD con IdeaScale tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="cc1da-111">tooconfigure Azure AD integration with IdeaScale, you need hello following items:</span></span>

- <span data-ttu-id="cc1da-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc1da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc1da-113">Sottoscrizione di IdeaScale abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cc1da-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc1da-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="cc1da-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc1da-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="cc1da-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc1da-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cc1da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc1da-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc1da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc1da-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cc1da-118">Scenario description</span></span>
<span data-ttu-id="cc1da-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cc1da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc1da-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="cc1da-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc1da-121">Aggiunta di IdeaScale dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cc1da-121">Adding IdeaScale from hello gallery</span></span>
2. <span data-ttu-id="cc1da-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-hello-gallery"></a><span data-ttu-id="cc1da-123">Aggiunta di IdeaScale dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cc1da-123">Adding IdeaScale from hello gallery</span></span>
<span data-ttu-id="cc1da-124">integrazione hello tooconfigure di IdeaScale in Azure AD, è necessario tooadd IdeaScale dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cc1da-124">tooconfigure hello integration of IdeaScale into Azure AD, you need tooadd IdeaScale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc1da-125">**tooadd IdeaScale dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc1da-125">**tooadd IdeaScale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc1da-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cc1da-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc1da-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc1da-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="cc1da-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cc1da-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="cc1da-133">Nella casella di ricerca hello, digitare **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-133">In hello search box, type **IdeaScale**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="cc1da-135">Nel riquadro dei risultati hello, selezionare **IdeaScale**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cc1da-135">In hello results panel, select **IdeaScale**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc1da-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc1da-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con IdeaScale mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc1da-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cc1da-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in IdeaScale è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc1da-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IdeaScale is tooa user in Azure AD.</span></span> <span data-ttu-id="cc1da-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in IdeaScale richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="cc1da-140">In other words, a link relationship between an Azure AD user and hello related user in IdeaScale needs toobe established.</span></span>

<span data-ttu-id="cc1da-141">In IdeaScale, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="cc1da-141">In IdeaScale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cc1da-142">tooconfigure e prova AD Azure single sign-on con IdeaScale, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="cc1da-142">tooconfigure and test Azure AD single sign-on with IdeaScale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc1da-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cc1da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc1da-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc1da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc1da-145">**[Creazione di un utente test IdeaScale](#creating-an-ideascale-test-user)**  -toohave un equivalente di Britta Simon in IdeaScale che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cc1da-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - toohave a counterpart of Britta Simon in IdeaScale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc1da-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc1da-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc1da-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="cc1da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc1da-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc1da-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="cc1da-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="cc1da-150">**Azure AD tooconfigure single sign-on con IdeaScale, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc1da-150">**tooconfigure Azure AD single sign-on with IdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc1da-151">Nel portale di Azure su hello hello **IdeaScale** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-151">In hello Azure portal, on hello **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="cc1da-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc1da-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="cc1da-155">In hello **IdeaScale dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cc1da-155">On hello **IdeaScale Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="cc1da-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc1da-157">a.</span></span> <span data-ttu-id="cc1da-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="cc1da-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="cc1da-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc1da-159">b.</span></span> <span data-ttu-id="cc1da-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="cc1da-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="cc1da-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="cc1da-161">These values are not real.</span></span> <span data-ttu-id="cc1da-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="cc1da-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cc1da-163">Contatto [team di supporto Client di IdeaScale](http://support.ideascale.com/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="cc1da-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="cc1da-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="cc1da-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="cc1da-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cc1da-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cc1da-168">In hello **IdeaScale configurazione** fare clic su **configurare IdeaScale** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="cc1da-168">On hello **IdeaScale Configuration** section, click **Configure IdeaScale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cc1da-169">Hello copia **Sign-Out URL e l'ID entità SAML** da hello **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="cc1da-171">In una finestra del web browser, accedere come amministratore nel sito della società IdeaScale di tooyour.</span><span class="sxs-lookup"><span data-stu-id="cc1da-171">In a different web browser window, log in tooyour IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="cc1da-172">Andare troppo**Community Settings**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-172">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="cc1da-173">![Impostazioni Community](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Impostazioni Community")</span><span class="sxs-lookup"><span data-stu-id="cc1da-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="cc1da-174">Andare troppo**sicurezza \> Single Sign-on Settings**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-174">Go too**Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="cc1da-175">![Impostazioni di Single Sign-On](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Impostazioni di Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cc1da-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="cc1da-176">In **Single-Signon Type** (Tipo di accesso Single Sign-On) selezionare **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="cc1da-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span><span class="sxs-lookup"><span data-stu-id="cc1da-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="cc1da-178">In hello **Single Sign-on Settings** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cc1da-178">On hello **Single Signon Settings** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="cc1da-179">![Impostazioni di Single Sign-On](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Impostazioni di Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="cc1da-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="cc1da-180">a.</span><span class="sxs-lookup"><span data-stu-id="cc1da-180">a.</span></span> <span data-ttu-id="cc1da-181">In **SAML IdP Entity ID** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc1da-181">In **SAML IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cc1da-182">b.</span><span class="sxs-lookup"><span data-stu-id="cc1da-182">b.</span></span> <span data-ttu-id="cc1da-183">Copiare il contenuto di hello del file di metadati scaricato dal portale di Azure e incollarlo in hello **SAML IdP Metadata** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="cc1da-183">Copy hello content of your downloaded metadata file from Azure portal, and paste it into hello **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="cc1da-184">c.</span><span class="sxs-lookup"><span data-stu-id="cc1da-184">c.</span></span> <span data-ttu-id="cc1da-185">In **Logout Success URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc1da-185">In **Logout Success URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cc1da-186">d.</span><span class="sxs-lookup"><span data-stu-id="cc1da-186">d.</span></span> <span data-ttu-id="cc1da-187">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="cc1da-188">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="cc1da-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc1da-189">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="cc1da-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc1da-190">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc1da-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc1da-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1da-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc1da-192">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="cc1da-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="cc1da-194">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc1da-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc1da-195">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cc1da-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc1da-197">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc1da-199">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="cc1da-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc1da-201">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cc1da-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc1da-203">a.</span><span class="sxs-lookup"><span data-stu-id="cc1da-203">a.</span></span> <span data-ttu-id="cc1da-204">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc1da-205">b.</span><span class="sxs-lookup"><span data-stu-id="cc1da-205">b.</span></span> <span data-ttu-id="cc1da-206">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc1da-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc1da-207">c.</span><span class="sxs-lookup"><span data-stu-id="cc1da-207">c.</span></span> <span data-ttu-id="cc1da-208">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cc1da-209">d.</span><span class="sxs-lookup"><span data-stu-id="cc1da-209">d.</span></span> <span data-ttu-id="cc1da-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="cc1da-211">Creazione di un utente test di IdeaScale</span><span class="sxs-lookup"><span data-stu-id="cc1da-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="cc1da-212">toolog agli utenti di Azure AD tooenable a IdeaScale, è necessario eseguirne il provisioning in tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="cc1da-212">tooenable Azure AD users toolog into IdeaScale, they must be provisioned in tooIdeaScale.</span></span> <span data-ttu-id="cc1da-213">Nel caso di hello di IdeaScale, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="cc1da-213">In hello case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="cc1da-214">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc1da-214">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc1da-215">Accedi tooyour **IdeaScale** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="cc1da-215">Log in tooyour **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="cc1da-216">Andare troppo**Community Settings**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-216">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="cc1da-217">![Impostazioni Community](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Impostazioni Community")</span><span class="sxs-lookup"><span data-stu-id="cc1da-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="cc1da-218">Andare troppo**le impostazioni di base \> Gestione membri**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-218">Go too**Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="cc1da-219">Fare clic su **Aggiungi membro**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="cc1da-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span><span class="sxs-lookup"><span data-stu-id="cc1da-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="cc1da-221">Nella sezione Add New Member hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cc1da-221">In hello Add New Member section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cc1da-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span><span class="sxs-lookup"><span data-stu-id="cc1da-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="cc1da-223">a.</span><span class="sxs-lookup"><span data-stu-id="cc1da-223">a.</span></span> <span data-ttu-id="cc1da-224">In hello **indirizzi di posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica di un account aAd di cui si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="cc1da-224">In hello **Email Addresses** textbox, type hello email address of a valid AAD account you want tooprovision.</span></span>
   
    <span data-ttu-id="cc1da-225">b.</span><span class="sxs-lookup"><span data-stu-id="cc1da-225">b.</span></span> <span data-ttu-id="cc1da-226">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="cc1da-227">titolare dell'account di Azure Active Directory Hello Ottiene un messaggio di posta elettronica con un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="cc1da-227">hello Azure Active Directory account holder gets an email with a link tooconfirm hello account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="cc1da-228">È possibile usare qualsiasi altro IdeaScale utente account strumento di creazione o le API fornite da IdeaScale tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="cc1da-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cc1da-229">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1da-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cc1da-230">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="cc1da-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIdeaScale.</span></span>

![Assegna utente][200] 

<span data-ttu-id="cc1da-232">**tooassign Britta Simon tooIdeaScale, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc1da-232">**tooassign Britta Simon tooIdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc1da-233">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cc1da-235">Nell'elenco di applicazioni hello, selezionare **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-235">In hello applications list, select **IdeaScale**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="cc1da-237">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="cc1da-239">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-239">Click **Add** button.</span></span> <span data-ttu-id="cc1da-240">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="cc1da-242">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="cc1da-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc1da-243">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc1da-244">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cc1da-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc1da-245">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cc1da-245">Testing single sign-on</span></span>


<span data-ttu-id="cc1da-246">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cc1da-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cc1da-247">Quando si fa clic su riquadro IdeaScale hello in hello Pannello di accesso, è necessario ottenere applicazione IdeaScale tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="cc1da-247">When you click hello IdeaScale tile in hello Access Panel, you should get automatically signed-on tooyour IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc1da-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cc1da-248">Additional resources</span></span>

* [<span data-ttu-id="cc1da-249">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc1da-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc1da-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc1da-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

