---
title: 'Esercitazione: Integrazione di Azure Active Directory con RunMyProcess | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e RunMyProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="5a241-103">Esercitazione: Integrazione di Azure Active Directory con RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="5a241-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="5a241-104">In questa esercitazione, è illustrato come toointegrate RunMyProcess con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a241-104">In this tutorial, you learn how toointegrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a241-105">Integrazione di RunMyProcess con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5a241-105">Integrating RunMyProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5a241-106">È possibile controllare in Azure AD che ha accesso tooRunMyProcess</span><span class="sxs-lookup"><span data-stu-id="5a241-106">You can control in Azure AD who has access tooRunMyProcess</span></span>
- <span data-ttu-id="5a241-107">È possibile abilitare l'utenti tooautomatically get connesso tooRunMyProcess (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a241-107">You can enable your users tooautomatically get signed-on tooRunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5a241-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5a241-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5a241-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a241-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a241-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5a241-110">Prerequisites</span></span>

<span data-ttu-id="5a241-111">integrazione di Azure AD con RunMyProcess tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5a241-111">tooconfigure Azure AD integration with RunMyProcess, you need hello following items:</span></span>

- <span data-ttu-id="5a241-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a241-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a241-113">Sottoscrizione di RunMyProcess abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5a241-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a241-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5a241-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a241-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5a241-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a241-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5a241-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a241-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a241-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a241-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5a241-118">Scenario description</span></span>
<span data-ttu-id="5a241-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5a241-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a241-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5a241-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a241-121">Aggiunta di RunMyProcess dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5a241-121">Adding RunMyProcess from hello gallery</span></span>
2. <span data-ttu-id="5a241-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a241-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-hello-gallery"></a><span data-ttu-id="5a241-123">Aggiunta di RunMyProcess dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5a241-123">Adding RunMyProcess from hello gallery</span></span>
<span data-ttu-id="5a241-124">integrazione hello tooconfigure di RunMyProcess in Azure AD, è necessario tooadd RunMyProcess dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5a241-124">tooconfigure hello integration of RunMyProcess into Azure AD, you need tooadd RunMyProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5a241-125">**tooadd RunMyProcess dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5a241-125">**tooadd RunMyProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a241-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5a241-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5a241-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5a241-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5a241-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5a241-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5a241-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5a241-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5a241-133">Nella casella di ricerca hello, digitare **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="5a241-133">In hello search box, type **RunMyProcess**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="5a241-135">Nel riquadro dei risultati hello, selezionare **RunMyProcess**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5a241-135">In hello results panel, select **RunMyProcess**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5a241-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a241-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5a241-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con RunMyProcess in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5a241-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5a241-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in RunMyProcess è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a241-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RunMyProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="5a241-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in RunMyProcess deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5a241-140">In other words, a link relationship between an Azure AD user and hello related user in RunMyProcess needs toobe established.</span></span>

<span data-ttu-id="5a241-141">In RunMyProcess, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5a241-141">In RunMyProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5a241-142">tooconfigure e prova AD Azure single sign-on con RunMyProcess, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5a241-142">tooconfigure and test Azure AD single sign-on with RunMyProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5a241-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5a241-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5a241-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5a241-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a241-145">**[Creazione di un utente test RunMyProcess](#creating-a-runmyprocess-test-user)**  -toohave un equivalente di Britta Simon in RunMyProcess che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5a241-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - toohave a counterpart of Britta Simon in RunMyProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a241-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5a241-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a241-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5a241-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5a241-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a241-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5a241-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5a241-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="5a241-150">**Azure AD tooconfigure single sign-on con RunMyProcess, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5a241-150">**tooconfigure Azure AD single sign-on with RunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a241-151">Nel portale di Azure su hello hello **RunMyProcess** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5a241-151">In hello Azure portal, on hello **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5a241-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5a241-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="5a241-155">In hello **RunMyProcess dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5a241-155">On hello **RunMyProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="5a241-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="5a241-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a241-158">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="5a241-158">hello value is not real.</span></span> <span data-ttu-id="5a241-159">Il valore di hello aggiornamento con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5a241-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5a241-160">Contatto [team di supporto Client di RunMyProcess](mailto:support@runmyprocess.com) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="5a241-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) tooget hello value.</span></span> 

4. <span data-ttu-id="5a241-161">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5a241-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="5a241-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5a241-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5a241-165">In hello **RunMyProcess configurazione** fare clic su **configurare RunMyProcess** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="5a241-165">On hello **RunMyProcess Configuration** section, click **Configure RunMyProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5a241-166">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5a241-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="5a241-168">In una finestra del web browser, accesso tooyour tenant di RunMyProcess come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5a241-168">In a different web browser window, sign-on tooyour RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="5a241-169">Nel pannello di spostamento a sinistra fare clic su **Account** e selezionare **Configuration** (Configurazione).</span><span class="sxs-lookup"><span data-stu-id="5a241-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="5a241-171">Andare troppo**metodo di autenticazione** sezione ed eseguire i passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="5a241-171">Go too**Authentication method** section and perform below steps:</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="5a241-173">a.</span><span class="sxs-lookup"><span data-stu-id="5a241-173">a.</span></span> <span data-ttu-id="5a241-174">In **Metodo** selezionare **SSO con Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="5a241-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="5a241-175">b.</span><span class="sxs-lookup"><span data-stu-id="5a241-175">b.</span></span> <span data-ttu-id="5a241-176">In hello **reindirizzamento SSO** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a241-176">In hello **SSO redirect** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5a241-177">c.</span><span class="sxs-lookup"><span data-stu-id="5a241-177">c.</span></span> <span data-ttu-id="5a241-178">In hello **reindirizzamento disconnessione** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a241-178">In hello **Logout redirect** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5a241-179">d.</span><span class="sxs-lookup"><span data-stu-id="5a241-179">d.</span></span> <span data-ttu-id="5a241-180">In hello **formato Id nome** casella di testo, hello tipo valore **Name Identifier Format** come **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="5a241-180">In hello **Name Id Format** textbox, type hello value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="5a241-181">e.</span><span class="sxs-lookup"><span data-stu-id="5a241-181">e.</span></span> <span data-ttu-id="5a241-182">Copiare il contenuto di hello hello scaricato del file di certificato e quindi incollarlo hello **certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="5a241-182">Copy hello content of hello downloaded certificate file and then paste it into hello **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="5a241-183">f.</span><span class="sxs-lookup"><span data-stu-id="5a241-183">f.</span></span> <span data-ttu-id="5a241-184">Fare clic sull'icona di **salvataggio**.</span><span class="sxs-lookup"><span data-stu-id="5a241-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="5a241-185">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5a241-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5a241-186">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5a241-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5a241-187">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a241-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5a241-188">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a241-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="5a241-189">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5a241-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5a241-191">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5a241-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a241-192">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5a241-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5a241-194">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5a241-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5a241-196">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="5a241-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5a241-198">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5a241-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5a241-200">a.</span><span class="sxs-lookup"><span data-stu-id="5a241-200">a.</span></span> <span data-ttu-id="5a241-201">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a241-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a241-202">b.</span><span class="sxs-lookup"><span data-stu-id="5a241-202">b.</span></span> <span data-ttu-id="5a241-203">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5a241-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5a241-204">c.</span><span class="sxs-lookup"><span data-stu-id="5a241-204">c.</span></span> <span data-ttu-id="5a241-205">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5a241-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5a241-206">d.</span><span class="sxs-lookup"><span data-stu-id="5a241-206">d.</span></span> <span data-ttu-id="5a241-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5a241-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="5a241-208">Creazione di un utente test di RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="5a241-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="5a241-209">In ordine tooenable Azure AD utenti toolog in tooRunMyProcess, è necessario eseguirne il provisioning in RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5a241-209">In order tooenable Azure AD users toolog in tooRunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="5a241-210">Nel caso di hello di RunMyProcess, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="5a241-210">In hello case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="5a241-211">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5a241-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a241-212">Accedi tooyour sito della società RunMyProcess come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5a241-212">Log in tooyour RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="5a241-213">Nel pannello di spostamento a sinistra fare clic su **Account** e selezionare **Users** (Utenti), quindi fare clic su **New User** (Nuovo utente).</span><span class="sxs-lookup"><span data-stu-id="5a241-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="5a241-214">![Nuovo utente](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="5a241-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="5a241-215">In hello **impostazioni utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5a241-215">In hello **User Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5a241-216">![Profilo](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profilo")</span><span class="sxs-lookup"><span data-stu-id="5a241-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="5a241-217">a.</span><span class="sxs-lookup"><span data-stu-id="5a241-217">a.</span></span> <span data-ttu-id="5a241-218">Hello tipo **nome** e **posta elettronica** di Azure un valido relative all'account di Active Directory desiderata tooprovision in hello nelle caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="5a241-218">Type hello **Name** and **E-mail** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="5a241-219">b.</span><span class="sxs-lookup"><span data-stu-id="5a241-219">b.</span></span> <span data-ttu-id="5a241-220">Selezionare una **lingua IDE**, una **lingua** e un **profilo**.</span><span class="sxs-lookup"><span data-stu-id="5a241-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="5a241-221">c.</span><span class="sxs-lookup"><span data-stu-id="5a241-221">c.</span></span> <span data-ttu-id="5a241-222">Selezionare **inviare toome di posta elettronica di creazione account**.</span><span class="sxs-lookup"><span data-stu-id="5a241-222">Select **Send account creation e-mail toome**.</span></span> 

    <span data-ttu-id="5a241-223">d.</span><span class="sxs-lookup"><span data-stu-id="5a241-223">d.</span></span> <span data-ttu-id="5a241-224">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5a241-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="5a241-225">È possibile usare qualsiasi altro RunMyProcess utente account strumento di creazione o le API fornite da RunMyProcess tooprovision Azure Active Directory gli account utente.</span><span class="sxs-lookup"><span data-stu-id="5a241-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess tooprovision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5a241-226">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a241-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5a241-227">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooRunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5a241-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRunMyProcess.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5a241-229">**tooassign Britta Simon tooRunMyProcess, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5a241-229">**tooassign Britta Simon tooRunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a241-230">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5a241-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5a241-232">Nell'elenco di applicazioni hello, selezionare **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="5a241-232">In hello applications list, select **RunMyProcess**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="5a241-234">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5a241-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5a241-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5a241-236">Click **Add** button.</span></span> <span data-ttu-id="5a241-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5a241-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5a241-239">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5a241-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5a241-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5a241-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a241-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5a241-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5a241-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5a241-242">Testing single sign-on</span></span>

<span data-ttu-id="5a241-243">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5a241-243">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5a241-244">Quando si fa clic hello RunMyProcess riquadro in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in RunMyProcess applicazione.</span><span class="sxs-lookup"><span data-stu-id="5a241-244">When you click hello RunMyProcess tile in hello Access Panel, you should get automatically signed-on tooyour RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a241-245">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5a241-245">Additional resources</span></span>

* [<span data-ttu-id="5a241-246">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a241-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a241-247">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a241-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

