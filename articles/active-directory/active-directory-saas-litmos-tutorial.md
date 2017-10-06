---
title: Esercitazione Integrazione di Azure Active Directory con Litmos | Documentazione Microsoft
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Litmos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="4fc0a-103">Esercitazione Integrazione di Azure Active Directory con Litmos</span><span class="sxs-lookup"><span data-stu-id="4fc0a-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="4fc0a-104">In questa esercitazione, è illustrato come toointegrate Litmos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4fc0a-104">In this tutorial, you learn how toointegrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fc0a-105">Integrazione Litmos con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4fc0a-105">Integrating Litmos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4fc0a-106">È possibile controllare in Azure AD che ha accesso tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-106">You can control in Azure AD who has access tooLitmos.</span></span>
- <span data-ttu-id="4fc0a-107">È possibile abilitare l'utenti tooautomatically get connesso tooLitmos (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-107">You can enable your users tooautomatically get signed-on tooLitmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4fc0a-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4fc0a-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4fc0a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fc0a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4fc0a-110">Prerequisites</span></span>

<span data-ttu-id="4fc0a-111">integrazione di Azure AD con Litmos tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4fc0a-111">tooconfigure Azure AD integration with Litmos, you need hello following items:</span></span>

- <span data-ttu-id="4fc0a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4fc0a-113">Sottoscrizione di Litmos abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4fc0a-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fc0a-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4fc0a-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4fc0a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4fc0a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fc0a-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fc0a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fc0a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4fc0a-118">Scenario description</span></span>
<span data-ttu-id="4fc0a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fc0a-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4fc0a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fc0a-121">Aggiunta di Litmos dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4fc0a-121">Adding Litmos from hello gallery</span></span>
2. <span data-ttu-id="4fc0a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fc0a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-hello-gallery"></a><span data-ttu-id="4fc0a-123">Aggiunta di Litmos dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4fc0a-123">Adding Litmos from hello gallery</span></span>
<span data-ttu-id="4fc0a-124">integrazione hello tooconfigure di Litmos in Azure AD, è necessario tooadd Litmos dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-124">tooconfigure hello integration of Litmos into Azure AD, you need tooadd Litmos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4fc0a-125">**tooadd Litmos dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4fc0a-125">**tooadd Litmos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fc0a-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="4fc0a-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4fc0a-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="4fc0a-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="4fc0a-133">Nella casella di ricerca hello, digitare **Litmos**selezionare **Litmos** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-133">In hello search box, type **Litmos**, select **Litmos** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4fc0a-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fc0a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4fc0a-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Litmos usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4fc0a-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4fc0a-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Litmos è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Litmos is tooa user in Azure AD.</span></span> <span data-ttu-id="4fc0a-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Litmos deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-138">In other words, a link relationship between an Azure AD user and hello related user in Litmos needs toobe established.</span></span>

<span data-ttu-id="4fc0a-139">In Litmos, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-139">In Litmos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4fc0a-140">tooconfigure e prova AD Azure single sign-on con Litmos, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4fc0a-140">tooconfigure and test Azure AD single sign-on with Litmos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4fc0a-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4fc0a-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fc0a-143">**[Creare un utente test Litmos](#create-a-litmos-test-user)**  -toohave un equivalente di Britta Simon in Litmos che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - toohave a counterpart of Britta Simon in Litmos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4fc0a-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fc0a-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4fc0a-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fc0a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4fc0a-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Litmos.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="4fc0a-148">**Azure AD tooconfigure single sign-on con Litmos, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4fc0a-148">**tooconfigure Azure AD single sign-on with Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fc0a-149">Nel portale di Azure su hello hello **Litmos** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-149">In hello Azure portal, on hello **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="4fc0a-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="4fc0a-153">In hello **Litmos dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4fc0a-153">On hello **Litmos Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni sul Single Sign-On di URL e dominio di Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="4fc0a-155">a.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-155">a.</span></span> <span data-ttu-id="4fc0a-156">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="4fc0a-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="4fc0a-157">b.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-157">b.</span></span> <span data-ttu-id="4fc0a-158">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="4fc0a-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fc0a-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4fc0a-159">These values are not real.</span></span> <span data-ttu-id="4fc0a-160">Aggiornare questi valori con hello identificatore e Reply URL effettivo, che vengono descritte più avanti nell'esercitazione o contatto [team di supporto Litmos](https://www.litmos.com/contact-us/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-160">Update these values with hello actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="4fc0a-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="4fc0a-163">Come parte della configurazione di hello, è necessario hello toocustomize **attributi Token SAML** per l'applicazione Litmos.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-163">As part of hello configuration, you need toocustomize hello **SAML Token Attributes** for your Litmos application.</span></span>

    ![Sezione relativa all'attributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="4fc0a-165">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="4fc0a-165">Attribute Name</span></span>   | <span data-ttu-id="4fc0a-166">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="4fc0a-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="4fc0a-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="4fc0a-167">FirstName</span></span> |<span data-ttu-id="4fc0a-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4fc0a-168">user.givenname</span></span> |
    | <span data-ttu-id="4fc0a-169">LastName</span><span class="sxs-lookup"><span data-stu-id="4fc0a-169">LastName</span></span>  |<span data-ttu-id="4fc0a-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="4fc0a-170">user.surname</span></span> |
    | <span data-ttu-id="4fc0a-171">Email</span><span class="sxs-lookup"><span data-stu-id="4fc0a-171">Email</span></span> |<span data-ttu-id="4fc0a-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="4fc0a-172">user.mail</span></span> |

    <span data-ttu-id="4fc0a-173">a.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-173">a.</span></span> <span data-ttu-id="4fc0a-174">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Aggiungi attributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Finestra di dialogo Aggiungi attributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4fc0a-177">b.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-177">b.</span></span> <span data-ttu-id="4fc0a-178">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="4fc0a-179">c.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-179">c.</span></span> <span data-ttu-id="4fc0a-180">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4fc0a-181">d.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-181">d.</span></span> <span data-ttu-id="4fc0a-182">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="4fc0a-183">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4fc0a-183">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4fc0a-185">In un'altra finestra del browser del sito di accesso tooyour Litmos aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-185">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

8. <span data-ttu-id="4fc0a-186">Nella barra di navigazione hello sul lato sinistro di hello, fare clic su **account**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-186">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Sezione relativa agli account sul lato dell'app][22] 

9. <span data-ttu-id="4fc0a-188">Fare clic su hello **integrazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-188">Click hello **Integrations** tab.</span></span>
   
    ![Scheda Integrazione][23] 

10. <span data-ttu-id="4fc0a-190">In hello **integrazioni** scheda, scorrere verso il basso troppo**3rd Party integrazioni**, quindi fare clic su **SAML 2.0** scheda.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-190">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![Sezione SAML 2.0][24] 

11. <span data-ttu-id="4fc0a-192">Copiare il valore di hello in **hello endpoint SAML per litmos:** e incollarlo in hello **URL di risposta** casella di testo in hello **Litmos dominio e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-192">Copy hello value under **hello SAML endpoint for litmos is:** and paste it into hello **Reply URL** textbox in hello **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![Endpoint SAML][26] 

12. <span data-ttu-id="4fc0a-194">Nel **Litmos** applicazione, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4fc0a-194">In your **Litmos** application, perform hello following steps:</span></span>
    
     ![Applicazione Litmos][25] 
     
     <span data-ttu-id="4fc0a-196">a.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-196">a.</span></span> <span data-ttu-id="4fc0a-197">Fare clic su **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="4fc0a-198">b.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-198">b.</span></span> <span data-ttu-id="4fc0a-199">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509 SAML** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-199">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="4fc0a-200">c.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-200">c.</span></span> <span data-ttu-id="4fc0a-201">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="4fc0a-202">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4fc0a-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4fc0a-203">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4fc0a-204">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4fc0a-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4fc0a-205">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fc0a-205">Create an Azure AD test user</span></span>

<span data-ttu-id="4fc0a-206">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="4fc0a-208">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4fc0a-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fc0a-209">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4fc0a-211">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4fc0a-213">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4fc0a-215">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4fc0a-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4fc0a-217">a.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-217">a.</span></span> <span data-ttu-id="4fc0a-218">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fc0a-219">b.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-219">b.</span></span> <span data-ttu-id="4fc0a-220">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4fc0a-221">c.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-221">c.</span></span> <span data-ttu-id="4fc0a-222">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4fc0a-223">d.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-223">d.</span></span> <span data-ttu-id="4fc0a-224">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="4fc0a-225">Creare un utente di test di Litmos</span><span class="sxs-lookup"><span data-stu-id="4fc0a-225">Create a Litmos test user</span></span>

<span data-ttu-id="4fc0a-226">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Litmos toocreate.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-226">hello objective of this section is toocreate a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="4fc0a-227">Hello Litmos applicazione supporta Just-in-Time di provisioning.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-227">hello Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="4fc0a-228">In questo campo, un account utente viene creato automaticamente se necessario durante un'applicazione di hello tooaccess tentativo utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-228">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

<span data-ttu-id="4fc0a-229">**un utente denominato Britta Simon in Litmos, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4fc0a-229">**toocreate a user called Britta Simon in Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fc0a-230">In un'altra finestra del browser del sito di accesso tooyour Litmos aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-230">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

2. <span data-ttu-id="4fc0a-231">Nella barra di navigazione hello sul lato sinistro di hello, fare clic su **account**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-231">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Sezione relativa agli account sul lato dell'app][22] 

3. <span data-ttu-id="4fc0a-233">Fare clic su hello **integrazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-233">Click hello **Integrations** tab.</span></span>
   
    ![Scheda Integrazioni][23] 

4. <span data-ttu-id="4fc0a-235">In hello **integrazioni** scheda, scorrere verso il basso troppo**3rd Party integrazioni**, quindi fare clic su **SAML 2.0** scheda.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-235">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="4fc0a-237">Selezionare **Autogenerate Users**(Genera utenti in automatico)</span><span class="sxs-lookup"><span data-stu-id="4fc0a-237">Select **Autogenerate Users**</span></span>
   
    ![Autogenerate Users (Genera utenti in automatico)][27] 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4fc0a-239">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fc0a-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4fc0a-240">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLitmos.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="4fc0a-242">**tooassign Britta Simon tooLitmos, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4fc0a-242">**tooassign Britta Simon tooLitmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fc0a-243">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4fc0a-245">Nell'elenco di applicazioni hello, selezionare **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-245">In hello applications list, select **Litmos**.</span></span>

    ![collegamento Litmos Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="4fc0a-247">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="4fc0a-249">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-249">Click **Add** button.</span></span> <span data-ttu-id="4fc0a-250">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="4fc0a-252">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4fc0a-253">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4fc0a-254">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4fc0a-255">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4fc0a-255">Test single sign-on</span></span>

<span data-ttu-id="4fc0a-256">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="4fc0a-257">Quando si fa clic hello Litmos riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Litmos applicazione.</span><span class="sxs-lookup"><span data-stu-id="4fc0a-257">When you click hello Litmos tile in hello Access Panel, you should get automatically signed-on tooyour Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4fc0a-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4fc0a-258">Additional resources</span></span>

* [<span data-ttu-id="4fc0a-259">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fc0a-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fc0a-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fc0a-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

