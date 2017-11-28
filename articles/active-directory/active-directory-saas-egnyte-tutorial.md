---
title: 'Esercitazione: Integrazione di Azure Active Directory con Egnyte | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed Egnyte.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="1881b-103">Esercitazione: Integrazione di Azure Active Directory con Egnyte</span><span class="sxs-lookup"><span data-stu-id="1881b-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="1881b-104">In questa esercitazione, è illustrato come toointegrate Egnyte con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1881b-104">In this tutorial, you learn how toointegrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1881b-105">Integrazione di Egnyte con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1881b-105">Integrating Egnyte with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1881b-106">È possibile controllare in Azure AD che ha accesso tooEgnyte</span><span class="sxs-lookup"><span data-stu-id="1881b-106">You can control in Azure AD who has access tooEgnyte</span></span>
- <span data-ttu-id="1881b-107">È possibile abilitare l'utenti tooautomatically get connesso tooEgnyte (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1881b-107">You can enable your users tooautomatically get signed-on tooEgnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1881b-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1881b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1881b-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1881b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1881b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1881b-110">Prerequisites</span></span>

<span data-ttu-id="1881b-111">integrazione di Azure AD con Egnyte tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1881b-111">tooconfigure Azure AD integration with Egnyte, you need hello following items:</span></span>

- <span data-ttu-id="1881b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1881b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1881b-113">Sottoscrizione di Egnyte abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1881b-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1881b-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1881b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1881b-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1881b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1881b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1881b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1881b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1881b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1881b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1881b-118">Scenario description</span></span>
<span data-ttu-id="1881b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1881b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1881b-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1881b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1881b-121">Aggiunta di Egnyte dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1881b-121">Adding Egnyte from hello gallery</span></span>
2. <span data-ttu-id="1881b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1881b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-hello-gallery"></a><span data-ttu-id="1881b-123">Aggiunta di Egnyte dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1881b-123">Adding Egnyte from hello gallery</span></span>
<span data-ttu-id="1881b-124">integrazione hello tooconfigure di Egnyte in Azure AD, è necessario tooadd Egnyte dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1881b-124">tooconfigure hello integration of Egnyte into Azure AD, you need tooadd Egnyte from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1881b-125">**tooadd Egnyte dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1881b-125">**tooadd Egnyte from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1881b-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1881b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1881b-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1881b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1881b-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1881b-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1881b-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1881b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1881b-133">Nella casella di ricerca hello, digitare **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="1881b-133">In hello search box, type **Egnyte**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="1881b-135">Nel riquadro dei risultati hello, selezionare **Egnyte**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1881b-135">In hello results panel, select **Egnyte**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1881b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1881b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1881b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Egnyte mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1881b-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1881b-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Egnyte è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1881b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Egnyte is tooa user in Azure AD.</span></span> <span data-ttu-id="1881b-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Egnyte deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1881b-140">In other words, a link relationship between an Azure AD user and hello related user in Egnyte needs toobe established.</span></span>

<span data-ttu-id="1881b-141">In Egnyte, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1881b-141">In Egnyte, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1881b-142">tooconfigure e prova AD Azure single sign-on con Egnyte, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1881b-142">tooconfigure and test Azure AD single sign-on with Egnyte, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1881b-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1881b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1881b-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1881b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1881b-145">**[Creazione di un utente test Egnyte](#creating-an-egnyte-test-user)**  -toohave un equivalente di Britta Simon in Egnyte che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1881b-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - toohave a counterpart of Britta Simon in Egnyte that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1881b-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1881b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1881b-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1881b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1881b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1881b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1881b-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Egnyte.</span><span class="sxs-lookup"><span data-stu-id="1881b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="1881b-150">**Azure AD tooconfigure single sign-on con Egnyte, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1881b-150">**tooconfigure Azure AD single sign-on with Egnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="1881b-151">Nel portale di Azure su hello hello **Egnyte** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1881b-151">In hello Azure portal, on hello **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1881b-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1881b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="1881b-155">In hello **Egnyte dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1881b-155">On hello **Egnyte Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="1881b-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="1881b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1881b-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="1881b-158">This value is not real.</span></span> <span data-ttu-id="1881b-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1881b-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1881b-160">Contatto [team di supporto Client di Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="1881b-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="1881b-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1881b-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="1881b-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1881b-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1881b-165">In hello **Egnyte configurazione** fare clic su **configurare Egnyte** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="1881b-165">On hello **Egnyte Configuration** section, click **Configure Egnyte** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1881b-166">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1881b-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="1881b-168">In una finestra del web browser, accedere come amministratore nel sito della società Egnyte di tooyour.</span><span class="sxs-lookup"><span data-stu-id="1881b-168">In a different web browser window, log in tooyour Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="1881b-169">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="1881b-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="1881b-170">![Impostazioni](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="1881b-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="1881b-171">Scegliere dal menu hello **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="1881b-171">In hello menu, click **Settings**.</span></span>

   <span data-ttu-id="1881b-172">![Impostazioni](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="1881b-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="1881b-173">Fare clic su hello **configurazione** scheda e quindi fare clic su **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="1881b-173">Click hello **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="1881b-174">![Sicurezza](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="1881b-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="1881b-175">In hello **autenticazione Single Sign-On** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1881b-175">In hello **Single Sign-On Authentication** section, perform hello following steps:</span></span>

    <span data-ttu-id="1881b-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span><span class="sxs-lookup"><span data-stu-id="1881b-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="1881b-177">a.</span><span class="sxs-lookup"><span data-stu-id="1881b-177">a.</span></span> <span data-ttu-id="1881b-178">In **Single sign-on authentication** (Autenticazione Single Sign-On) selezionare **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="1881b-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="1881b-179">b.</span><span class="sxs-lookup"><span data-stu-id="1881b-179">b.</span></span> <span data-ttu-id="1881b-180">In **Identity provider** (Provider di identità) selezionare **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="1881b-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="1881b-181">c.</span><span class="sxs-lookup"><span data-stu-id="1881b-181">c.</span></span> <span data-ttu-id="1881b-182">Incolla **SAML Single Sign-On Service URL** copiato dal portale Azure hello **Identity provider login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="1881b-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into hello **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="1881b-183">d.</span><span class="sxs-lookup"><span data-stu-id="1881b-183">d.</span></span> <span data-ttu-id="1881b-184">Incolla **ID entità SAML** che è stato copiato dal portale di Azure in hello **ID entità di provider di identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="1881b-184">Paste **SAML Entity ID** which you have copied from Azure portal into hello **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="1881b-185">e.</span><span class="sxs-lookup"><span data-stu-id="1881b-185">e.</span></span> <span data-ttu-id="1881b-186">Aprire il certificato con codifica base 64 nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato provider di identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="1881b-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="1881b-187">f.</span><span class="sxs-lookup"><span data-stu-id="1881b-187">f.</span></span> <span data-ttu-id="1881b-188">In **Default user mapping** (Mapping utente predefinito) selezionare **Email address** (Indirizzo posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="1881b-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="1881b-189">g.</span><span class="sxs-lookup"><span data-stu-id="1881b-189">g.</span></span> <span data-ttu-id="1881b-190">In **Use domain-specific issuer value** (Usa valore autorità emittente specifica del dominio) selezionare **disabled** (disabilitato).</span><span class="sxs-lookup"><span data-stu-id="1881b-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="1881b-191">h.</span><span class="sxs-lookup"><span data-stu-id="1881b-191">h.</span></span> <span data-ttu-id="1881b-192">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1881b-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1881b-193">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1881b-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1881b-194">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1881b-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1881b-195">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1881b-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1881b-196">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1881b-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="1881b-197">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1881b-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1881b-199">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1881b-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1881b-200">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1881b-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1881b-202">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1881b-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1881b-204">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1881b-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1881b-206">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1881b-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1881b-208">a.</span><span class="sxs-lookup"><span data-stu-id="1881b-208">a.</span></span> <span data-ttu-id="1881b-209">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1881b-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1881b-210">b.</span><span class="sxs-lookup"><span data-stu-id="1881b-210">b.</span></span> <span data-ttu-id="1881b-211">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1881b-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1881b-212">c.</span><span class="sxs-lookup"><span data-stu-id="1881b-212">c.</span></span> <span data-ttu-id="1881b-213">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1881b-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1881b-214">d.</span><span class="sxs-lookup"><span data-stu-id="1881b-214">d.</span></span> <span data-ttu-id="1881b-215">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1881b-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="1881b-216">Creazione di un utente test di Egnyte</span><span class="sxs-lookup"><span data-stu-id="1881b-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="1881b-217">toolog agli utenti di Azure AD tooenable in tooEgnyte, è necessario eseguirne il provisioning in Egnyte.</span><span class="sxs-lookup"><span data-stu-id="1881b-217">tooenable Azure AD users toolog in tooEgnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="1881b-218">Nel caso di hello di Egnyte, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="1881b-218">In hello case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="1881b-219">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="1881b-219">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="1881b-220">Accedi tooyour **Egnyte** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1881b-220">Log in tooyour **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="1881b-221">Andare troppo**impostazioni \> utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1881b-221">Go too**Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="1881b-222">Fare clic su **Add New User**, quindi selezionare il tipo di hello dell'utente desiderato tooadd.</span><span class="sxs-lookup"><span data-stu-id="1881b-222">Click **Add New User**, and then select hello type of user you want tooadd.</span></span>
   
   <span data-ttu-id="1881b-223">![Utenti](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="1881b-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="1881b-224">In hello **New Standard User** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1881b-224">In hello **New Standard User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="1881b-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span><span class="sxs-lookup"><span data-stu-id="1881b-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="1881b-226">a.</span><span class="sxs-lookup"><span data-stu-id="1881b-226">a.</span></span> <span data-ttu-id="1881b-227">Hello tipo **posta elettronica**, **Username**e altri dettagli di un account di Azure Active Directory valido, si vuole tooprovision.</span><span class="sxs-lookup"><span data-stu-id="1881b-227">Type hello **Email**, **Username**, and other details of a valid Azure Active Directory account you want tooprovision.</span></span>
   
   <span data-ttu-id="1881b-228">b.</span><span class="sxs-lookup"><span data-stu-id="1881b-228">b.</span></span> <span data-ttu-id="1881b-229">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1881b-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="1881b-230">titolare dell'account di Azure Active Directory Hello riceverà una notifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="1881b-230">hello Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="1881b-231">È possibile usare qualsiasi altro Egnyte utente account strumento di creazione o le API fornite da Egnyte tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="1881b-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1881b-232">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1881b-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1881b-233">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooEgnyte.</span><span class="sxs-lookup"><span data-stu-id="1881b-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEgnyte.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1881b-235">**tooassign Britta Simon tooEgnyte, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1881b-235">**tooassign Britta Simon tooEgnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="1881b-236">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1881b-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1881b-238">Nell'elenco di applicazioni hello, selezionare **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="1881b-238">In hello applications list, select **Egnyte**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="1881b-240">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1881b-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1881b-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1881b-242">Click **Add** button.</span></span> <span data-ttu-id="1881b-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1881b-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1881b-245">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1881b-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1881b-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1881b-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1881b-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1881b-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1881b-248">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1881b-248">Testing single sign-on</span></span>

<span data-ttu-id="1881b-249">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1881b-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1881b-250">Quando si fa clic su riquadro Egnyte hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Egnyte applicazione.</span><span class="sxs-lookup"><span data-stu-id="1881b-250">When you click hello Egnyte tile in hello Access Panel, you should get automatically signed-on tooyour Egnyte application.</span></span>
<span data-ttu-id="1881b-251">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1881b-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1881b-252">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1881b-252">Additional resources</span></span>

* [<span data-ttu-id="1881b-253">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1881b-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1881b-254">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1881b-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

