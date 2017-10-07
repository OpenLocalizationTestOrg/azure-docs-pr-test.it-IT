---
title: 'Esercitazione: Integrazione di Azure Active Directory con Teamphoria| Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Teamphoria.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="9b79b-103">Esercitazione: Integrazione di Azure Active Directory con Teamphoria</span><span class="sxs-lookup"><span data-stu-id="9b79b-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="9b79b-104">In questa esercitazione, è illustrato come toointegrate Teamphoria con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b79b-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b79b-105">Integrazione Teamphoria con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="9b79b-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9b79b-106">È possibile controllare in Azure AD che ha accesso tooTeamphoria</span><span class="sxs-lookup"><span data-stu-id="9b79b-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="9b79b-107">È possibile abilitare l'utenti tooautomatically get connesso tooTeamphoria (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b79b-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b79b-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="9b79b-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9b79b-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9b79b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="9b79b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9b79b-110">Prerequisites</span></span>

<span data-ttu-id="9b79b-111">integrazione di Azure AD con Teamphoria tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="9b79b-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="9b79b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b79b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b79b-113">Sottoscrizione di Teamphoria abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9b79b-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b79b-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="9b79b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b79b-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="9b79b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b79b-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9b79b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9b79b-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b79b-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b79b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9b79b-118">Scenario description</span></span>
<span data-ttu-id="9b79b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9b79b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b79b-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="9b79b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b79b-121">Aggiunta di Teamphoria dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="9b79b-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="9b79b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b79b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="9b79b-123">Aggiunta di Teamphoria dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="9b79b-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="9b79b-124">integrazione hello tooconfigure di Teamphoria in Azure AD, è necessario tooadd Teamphoria dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9b79b-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9b79b-125">**tooadd Teamphoria dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9b79b-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b79b-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9b79b-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9b79b-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9b79b-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="9b79b-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="9b79b-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="9b79b-133">Nella casella di ricerca hello, digitare **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-133">In hello search box, type **Teamphoria**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="9b79b-135">Nel riquadro dei risultati hello, selezionare **Teamphoria**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9b79b-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9b79b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b79b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9b79b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Teamphoria usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9b79b-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9b79b-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Teamphoria è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b79b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="9b79b-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Teamphoria deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="9b79b-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="9b79b-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="9b79b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="9b79b-142">tooconfigure e prova AD Azure single sign-on con Teamphoria, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="9b79b-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9b79b-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9b79b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9b79b-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b79b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b79b-145">**[Creazione di un utente test Teamphoria](#creating-a-teamphoria-test-user)**  -toohave un equivalente di Britta Simon in Teamphoria toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="9b79b-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9b79b-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9b79b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9b79b-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="9b79b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9b79b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b79b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9b79b-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="9b79b-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="9b79b-150">**Azure AD tooconfigure single sign-on con Teamphoria, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9b79b-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b79b-151">Nel portale di gestione di Azure hello in hello **Teamphoria** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="9b79b-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9b79b-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="9b79b-155">In hello **Teamphoria dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9b79b-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="9b79b-157">a.</span><span class="sxs-lookup"><span data-stu-id="9b79b-157">a.</span></span> <span data-ttu-id="9b79b-158">In hello **Sign-on URL** casella di testo, digitare l'URL hello utilizzando hello seguente motivo:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="9b79b-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="9b79b-159">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="9b79b-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="9b79b-160">Hai tooupdate questi valori con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9b79b-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="9b79b-161">Contatto [team di supporto Teamphoria Client](https://www.teamphoria.com/) tooget hello Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="9b79b-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="9b79b-162">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il certificato di hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="9b79b-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="9b79b-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="9b79b-164">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9b79b-166">In hello **Teamphoria configurazione** fare clic su **configurare Teamphoria** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="9b79b-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9b79b-167">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="9b79b-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="9b79b-169">tooconfigure single sign-on sul **Teamphoria** lato, applicazione Teamphoria tooyour di account di accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="9b79b-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="9b79b-170">Andare troppo**le impostazioni di amministrazione** opzione nella barra degli strumenti a sinistra di hello e in hello hello scheda Configurazione fare clic su **SINGLE SIGN-ON** finestra di configurazione SSO tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="9b79b-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="9b79b-172">Fare clic su **Aggiungi nuovo PROVIDER di identità** opzione nel modulo di hello angolo superiore destro tooopen hello per l'aggiunta di impostazioni di hello per SSO.</span><span class="sxs-lookup"><span data-stu-id="9b79b-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="9b79b-174">Immettere i dettagli di hello nei campi hello, come descritto di seguito</span><span class="sxs-lookup"><span data-stu-id="9b79b-174">Enter hello details in hello fields as described below-</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="9b79b-176">a.</span><span class="sxs-lookup"><span data-stu-id="9b79b-176">a.</span></span> <span data-ttu-id="9b79b-177">**NOME visualizzato** : immettere il nome visualizzato hello di plug-in hello nella pagina di amministrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="9b79b-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="9b79b-178">b.</span><span class="sxs-lookup"><span data-stu-id="9b79b-178">b.</span></span> <span data-ttu-id="9b79b-179">**Nome pulsante** : nome hello della scheda hello che verrà visualizzato nella pagina di accesso hello per l'accesso tramite SSO.</span><span class="sxs-lookup"><span data-stu-id="9b79b-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="9b79b-180">c.</span><span class="sxs-lookup"><span data-stu-id="9b79b-180">c.</span></span> <span data-ttu-id="9b79b-181">**CERTIFICATO** : hello aprire certificato scaricato in precedenza dal portale di Azure nel blocco note, copia hello contenuto di hello hello stesso e incollarlo qui nella casella hello.</span><span class="sxs-lookup"><span data-stu-id="9b79b-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="9b79b-182">d.</span><span class="sxs-lookup"><span data-stu-id="9b79b-182">d.</span></span> <span data-ttu-id="9b79b-183">**PUNTO di ingresso** : hello Incolla **SAML Single Sign-On Service URL** copiati precedenti hello modulo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b79b-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="9b79b-184">e.</span><span class="sxs-lookup"><span data-stu-id="9b79b-184">e.</span></span> <span data-ttu-id="9b79b-185">Opzione troppo opzione hello**ON** e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9b79b-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b79b-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="9b79b-187">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9b79b-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="9b79b-189">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9b79b-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b79b-190">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9b79b-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9b79b-192">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="9b79b-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9b79b-194">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9b79b-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9b79b-196">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9b79b-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b79b-198">a.</span><span class="sxs-lookup"><span data-stu-id="9b79b-198">a.</span></span> <span data-ttu-id="9b79b-199">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b79b-200">b.</span><span class="sxs-lookup"><span data-stu-id="9b79b-200">b.</span></span> <span data-ttu-id="9b79b-201">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9b79b-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b79b-202">c.</span><span class="sxs-lookup"><span data-stu-id="9b79b-202">c.</span></span> <span data-ttu-id="9b79b-203">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9b79b-204">d.</span><span class="sxs-lookup"><span data-stu-id="9b79b-204">d.</span></span> <span data-ttu-id="9b79b-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="9b79b-206">Creare un utente test di Teamphoria</span><span class="sxs-lookup"><span data-stu-id="9b79b-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="9b79b-207">In ordine tooenable Azure AD utenti toolog in Teamphoria, è necessario eseguirne il provisioning in Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="9b79b-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="9b79b-208">Nel caso di hello di Teamphoria, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="9b79b-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="9b79b-209">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="9b79b-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b79b-210">Accedi tooyour sito della società Teamphoria come amministratore.</span><span class="sxs-lookup"><span data-stu-id="9b79b-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="9b79b-211">Fare clic su **ADMIN** impostazioni sulla barra degli strumenti a sinistra di hello e in hello **GESTISCI** fare clic su scheda **utenti** pagina di amministrazione di hello tooopen per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="9b79b-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="9b79b-213">Fare clic su hello **manuale INVITARE** opzione.</span><span class="sxs-lookup"><span data-stu-id="9b79b-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![Invita persone](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="9b79b-215">In questa pagina effettuare l'operazione seguente.</span><span class="sxs-lookup"><span data-stu-id="9b79b-215">On this page, perform following action.</span></span> 
    
    ![Invita persone](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="9b79b-217">a.</span><span class="sxs-lookup"><span data-stu-id="9b79b-217">a.</span></span> <span data-ttu-id="9b79b-218">In hello **indirizzo di posta elettronica** casella di testo, hello **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9b79b-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b79b-219">b.</span><span class="sxs-lookup"><span data-stu-id="9b79b-219">b.</span></span> <span data-ttu-id="9b79b-220">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="9b79b-221">c.</span><span class="sxs-lookup"><span data-stu-id="9b79b-221">c.</span></span> <span data-ttu-id="9b79b-222">In hello **cognome** casella tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="9b79b-223">d.</span><span class="sxs-lookup"><span data-stu-id="9b79b-223">d.</span></span> <span data-ttu-id="9b79b-224">Fare clic su **INVITE 1 USER** (Invita 1 utente).</span><span class="sxs-lookup"><span data-stu-id="9b79b-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="9b79b-225">L'utente deve tooaccept hello invito tooget creata nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="9b79b-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9b79b-226">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b79b-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9b79b-227">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooTeamphoria proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="9b79b-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![Assegna utente][200] 

<span data-ttu-id="9b79b-229">**tooassign Britta Simon tooTeamphoria, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9b79b-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b79b-230">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9b79b-232">Nell'elenco di applicazioni hello, selezionare **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-232">In hello applications list, select **Teamphoria**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="9b79b-234">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="9b79b-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-236">Click **Add** button.</span></span> <span data-ttu-id="9b79b-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="9b79b-239">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="9b79b-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9b79b-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b79b-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9b79b-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9b79b-242">Testing single sign-on</span></span>

<span data-ttu-id="9b79b-243">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9b79b-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9b79b-244">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9b79b-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="9b79b-245">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9b79b-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9b79b-246">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9b79b-246">Additional resources</span></span>

* [<span data-ttu-id="9b79b-247">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b79b-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b79b-248">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b79b-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

