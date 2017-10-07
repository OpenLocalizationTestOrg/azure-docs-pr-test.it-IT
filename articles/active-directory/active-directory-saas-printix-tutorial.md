---
title: 'Esercitazione: Integrazione di Azure Active Directory con Printix | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Printix.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 654810116091eb52912b377cc97afef803ee816e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="eb118-103">Esercitazione: Integrazione di Azure Active Directory con Printix</span><span class="sxs-lookup"><span data-stu-id="eb118-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="eb118-104">In questa esercitazione, è illustrato come toointegrate Printix con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb118-104">In this tutorial, you learn how toointegrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb118-105">Integrazione Printix con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="eb118-105">Integrating Printix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb118-106">È possibile controllare in Azure AD che ha accesso tooPrintix</span><span class="sxs-lookup"><span data-stu-id="eb118-106">You can control in Azure AD who has access tooPrintix</span></span>
- <span data-ttu-id="eb118-107">È possibile abilitare l'utenti tooautomatically get connesso tooPrintix (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb118-107">You can enable your users tooautomatically get signed-on tooPrintix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb118-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eb118-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eb118-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb118-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb118-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eb118-110">Prerequisites</span></span>

<span data-ttu-id="eb118-111">integrazione di Azure AD con Printix tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="eb118-111">tooconfigure Azure AD integration with Printix, you need hello following items:</span></span>

- <span data-ttu-id="eb118-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb118-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb118-113">Sottoscrizione di Printix abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="eb118-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb118-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="eb118-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb118-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="eb118-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb118-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="eb118-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb118-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb118-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb118-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="eb118-118">Scenario description</span></span>
<span data-ttu-id="eb118-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="eb118-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb118-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="eb118-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb118-121">Aggiunta di Printix dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="eb118-121">Adding Printix from hello gallery</span></span>
2. <span data-ttu-id="eb118-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb118-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-hello-gallery"></a><span data-ttu-id="eb118-123">Aggiunta di Printix dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="eb118-123">Adding Printix from hello gallery</span></span>
<span data-ttu-id="eb118-124">integrazione hello tooconfigure di Printix in Azure AD, è necessario tooadd Printix dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="eb118-124">tooconfigure hello integration of Printix into Azure AD, you need tooadd Printix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb118-125">**tooadd Printix dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eb118-125">**tooadd Printix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb118-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="eb118-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eb118-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="eb118-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eb118-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="eb118-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="eb118-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="eb118-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="eb118-133">Nella casella di ricerca hello, digitare **Printix**.</span><span class="sxs-lookup"><span data-stu-id="eb118-133">In hello search box, type **Printix**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="eb118-135">Nel riquadro dei risultati hello, selezionare **Printix**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="eb118-135">In hello results panel, select **Printix**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb118-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb118-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb118-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Printix con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="eb118-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eb118-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Printix è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb118-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Printix is tooa user in Azure AD.</span></span> <span data-ttu-id="eb118-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Printix deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="eb118-140">In other words, a link relationship between an Azure AD user and hello related user in Printix needs toobe established.</span></span>

<span data-ttu-id="eb118-141">In Printix, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="eb118-141">In Printix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eb118-142">tooconfigure e prova AD Azure single sign-on con Printix, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="eb118-142">tooconfigure and test Azure AD single sign-on with Printix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb118-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="eb118-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb118-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb118-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb118-145">**[Creazione di un utente test Printix](#creating-a-printix-test-user)**  -toohave un equivalente di Britta Simon in Printix che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="eb118-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - toohave a counterpart of Britta Simon in Printix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb118-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="eb118-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb118-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="eb118-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb118-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb118-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb118-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Printix.</span><span class="sxs-lookup"><span data-stu-id="eb118-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="eb118-150">**Azure AD tooconfigure single sign-on con Printix, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eb118-150">**tooconfigure Azure AD single sign-on with Printix, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb118-151">Nel portale di Azure su hello hello **Printix** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="eb118-151">In hello Azure portal, on hello **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="eb118-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="eb118-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="eb118-155">In hello **Printix dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="eb118-155">On hello **Printix Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="eb118-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="eb118-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eb118-158">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="eb118-158">hello value is not real.</span></span> <span data-ttu-id="eb118-159">Il valore di hello aggiornamento con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="eb118-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="eb118-160">Contatto [team di supporto Printix Client](mailto:support@printix.net) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="eb118-160">Contact [Printix Client support team](mailto:support@printix.net) tooget hello value.</span></span> 
 
4. <span data-ttu-id="eb118-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="eb118-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="eb118-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="eb118-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eb118-165">Sign-on tooyour Printix tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="eb118-165">Sign-on tooyour Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="eb118-166">Nel menu di hello in primo piano hello, fare clic sull'icona hello hello angolo superiore destro e selezionare "**autenticazione**".</span><span class="sxs-lookup"><span data-stu-id="eb118-166">In hello menu on hello top, click hello icon at hello upper right corner and select "**Authentication**".</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="eb118-168">In hello **installazione** , selezionare **autenticazione attiva di Azure o Office 365**</span><span class="sxs-lookup"><span data-stu-id="eb118-168">On hello **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="eb118-170">In hello **Azure** scheda Federazione input metadati toohello casella di testo URL di "**documento metadati federazione**".</span><span class="sxs-lookup"><span data-stu-id="eb118-170">On hello **Azure** tab, input federation metadata URL toohello textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="eb118-171">Allegare il file xml di metadati hello che è stato scaricato da Azure AD troppo[team di supporto Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="eb118-171">Attach hello metadata xml file which you downloaded from Azure AD too[Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="eb118-172">Vengono quindi caricare file xml di hello e specificare un URL di metadati di federazione.</span><span class="sxs-lookup"><span data-stu-id="eb118-172">Then they upload hello xml file and provide a federation metadata URL.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="eb118-174">Fare clic su hello "**Test**"pulsante e fare clic su"**OK**" se hello è stata stabilita.</span><span class="sxs-lookup"><span data-stu-id="eb118-174">Click hello "**Test**" button and click "**OK**" button if hello test was successful.</span></span>
   
     <span data-ttu-id="eb118-175">Pagina di Azure active directory verrà visualizzato dopo aver fatto clic hello **test** pulsante.</span><span class="sxs-lookup"><span data-stu-id="eb118-175">Azure active directory page will show after clicking hello **test** button.</span></span> <span data-ttu-id="eb118-176">"hello è stata stabilita" qui significa che dopo aver immesso hello credenziali dell'account di Azure di test che verrà visualizzato un messaggio "le impostazioni di verifica OK". Quindi fare clic su hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="eb118-176">"hello test was successful" here means after entering hello credentials of your Azure test account it will pop up a message "Settings tested OK".Then click hello **OK** button.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="eb118-178">Fare clic su hello **salvare** pulsante "**autenticazione**" pagina.</span><span class="sxs-lookup"><span data-stu-id="eb118-178">Click hello **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="eb118-179">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="eb118-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eb118-180">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="eb118-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eb118-181">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb118-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb118-182">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb118-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb118-183">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="eb118-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="eb118-185">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eb118-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb118-186">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="eb118-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb118-188">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="eb118-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb118-190">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="eb118-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb118-192">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="eb118-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb118-194">a.</span><span class="sxs-lookup"><span data-stu-id="eb118-194">a.</span></span> <span data-ttu-id="eb118-195">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb118-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb118-196">b.</span><span class="sxs-lookup"><span data-stu-id="eb118-196">b.</span></span> <span data-ttu-id="eb118-197">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb118-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb118-198">c.</span><span class="sxs-lookup"><span data-stu-id="eb118-198">c.</span></span> <span data-ttu-id="eb118-199">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="eb118-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eb118-200">d.</span><span class="sxs-lookup"><span data-stu-id="eb118-200">d.</span></span> <span data-ttu-id="eb118-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="eb118-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="eb118-202">Creazione di un utente test di Printix</span><span class="sxs-lookup"><span data-stu-id="eb118-202">Creating a Printix test user</span></span>

<span data-ttu-id="eb118-203">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Printix toocreate.</span><span class="sxs-lookup"><span data-stu-id="eb118-203">hello objective of this section is toocreate a user called Britta Simon in Printix.</span></span> <span data-ttu-id="eb118-204">Printix supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eb118-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="eb118-205">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="eb118-205">There is no action item for you in this section.</span></span> <span data-ttu-id="eb118-206">Se non esiste ancora, durante un tooaccess tentativo Printix viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="eb118-206">A new user is created during an attempt tooaccess Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="eb118-207">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="eb118-207">If you need toocreate a user manually, you need toocontact hello [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eb118-208">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb118-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eb118-209">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPrintix.</span><span class="sxs-lookup"><span data-stu-id="eb118-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPrintix.</span></span>

![Assegna utente][200] 

<span data-ttu-id="eb118-211">**tooassign Britta Simon tooPrintix, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eb118-211">**tooassign Britta Simon tooPrintix, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb118-212">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="eb118-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="eb118-214">Nell'elenco di applicazioni hello, selezionare **Printix**.</span><span class="sxs-lookup"><span data-stu-id="eb118-214">In hello applications list, select **Printix**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="eb118-216">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="eb118-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="eb118-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="eb118-218">Click **Add** button.</span></span> <span data-ttu-id="eb118-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="eb118-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="eb118-221">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="eb118-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eb118-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="eb118-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb118-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="eb118-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb118-224">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="eb118-224">Testing single sign-on</span></span>

<span data-ttu-id="eb118-225">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="eb118-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eb118-226">Quando si fa clic su riquadro Printix hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Printix applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb118-226">When you click hello Printix tile in hello Access Panel, you should get automatically signed-on tooyour Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eb118-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="eb118-227">Additional resources</span></span>

* [<span data-ttu-id="eb118-228">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb118-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb118-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb118-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

