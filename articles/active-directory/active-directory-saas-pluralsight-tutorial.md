---
title: 'Esercitazione: Integrazione di Azure Active Directory con Pluralsight | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Pluralsight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8394eed79f21fb889816d8dafe2d71187be72b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="8fad6-103">Esercitazione: Integrazione di Azure Active Directory con Pluralsight</span><span class="sxs-lookup"><span data-stu-id="8fad6-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="8fad6-104">In questa esercitazione, è illustrato come toointegrate Pluralsight con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8fad6-104">In this tutorial, you learn how toointegrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8fad6-105">Integrazione Pluralsight con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8fad6-105">Integrating Pluralsight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8fad6-106">È possibile controllare in Azure AD che ha accesso tooPluralsight</span><span class="sxs-lookup"><span data-stu-id="8fad6-106">You can control in Azure AD who has access tooPluralsight</span></span>
- <span data-ttu-id="8fad6-107">È possibile abilitare l'utenti tooautomatically get connesso tooPluralsight (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fad6-107">You can enable your users tooautomatically get signed-on tooPluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8fad6-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8fad6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8fad6-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8fad6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fad6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8fad6-110">Prerequisites</span></span>

<span data-ttu-id="8fad6-111">integrazione di Azure AD con Pluralsight tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8fad6-111">tooconfigure Azure AD integration with Pluralsight, you need hello following items:</span></span>

- <span data-ttu-id="8fad6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fad6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8fad6-113">Sottoscrizione di Pluralsight abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8fad6-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8fad6-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8fad6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8fad6-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8fad6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8fad6-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8fad6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8fad6-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8fad6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8fad6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8fad6-118">Scenario description</span></span>
<span data-ttu-id="8fad6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8fad6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8fad6-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8fad6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8fad6-121">Aggiunta di Pluralsight dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8fad6-121">Adding Pluralsight from hello gallery</span></span>
2. <span data-ttu-id="8fad6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fad6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-hello-gallery"></a><span data-ttu-id="8fad6-123">Aggiunta di Pluralsight dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8fad6-123">Adding Pluralsight from hello gallery</span></span>
<span data-ttu-id="8fad6-124">integrazione hello tooconfigure di Pluralsight in Azure AD, è necessario tooadd Pluralsight dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8fad6-124">tooconfigure hello integration of Pluralsight into Azure AD, you need tooadd Pluralsight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8fad6-125">**tooadd Pluralsight dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8fad6-125">**tooadd Pluralsight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fad6-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8fad6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8fad6-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8fad6-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8fad6-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8fad6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8fad6-133">Nella casella di ricerca hello, digitare **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-133">In hello search box, type **Pluralsight**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="8fad6-135">Nel riquadro dei risultati hello, selezionare **Pluralsight**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8fad6-135">In hello results panel, select **Pluralsight**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8fad6-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fad6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8fad6-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Pluralsight con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8fad6-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8fad6-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Pluralsight è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fad6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pluralsight is tooa user in Azure AD.</span></span> <span data-ttu-id="8fad6-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello Pluralsight deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8fad6-140">In other words, a link relationship between an Azure AD user and hello related user in Pluralsight needs toobe established.</span></span>

<span data-ttu-id="8fad6-141">In Pluralsight, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="8fad6-141">In Pluralsight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8fad6-142">tooconfigure e prova AD Azure single sign-on con Pluralsight, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8fad6-142">tooconfigure and test Azure AD single sign-on with Pluralsight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8fad6-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8fad6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8fad6-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8fad6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8fad6-145">**[Creazione di un utente test Pluralsight](#creating-a-pluralsight-test-user)**  -toohave un equivalente di Britta Simon di Pluralsight che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8fad6-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - toohave a counterpart of Britta Simon in Pluralsight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8fad6-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8fad6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8fad6-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8fad6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8fad6-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fad6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8fad6-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="8fad6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="8fad6-150">**Azure AD tooconfigure single sign-on con Pluralsight, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8fad6-150">**tooconfigure Azure AD single sign-on with Pluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fad6-151">Nel portale di Azure su hello hello **Pluralsight** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-151">In hello Azure portal, on hello **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8fad6-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8fad6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="8fad6-155">In hello **Pluralsight dominio e gli URL** sezione, eseguire l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="8fad6-155">On hello **Pluralsight Domain and URLs** section, perform hello following:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="8fad6-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="8fad6-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8fad6-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="8fad6-158">This value is not real.</span></span> <span data-ttu-id="8fad6-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8fad6-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="8fad6-160">Contatto [team di supporto Pluralsight Client](mailto:support@pluralsight.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="8fad6-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="8fad6-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8fad6-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="8fad6-163">obiettivo di Hello di questa sezione è tooenable Azure AD accesso single sign-on in hello portale di Azure e tooconfigure SSO nell'applicazione Pluralsight hello.</span><span class="sxs-lookup"><span data-stu-id="8fad6-163">hello objective of this section is tooenable Azure AD single sign-on in hello Azure portal and tooconfigure SSO in hello Pluralsight application.</span></span>

    <span data-ttu-id="8fad6-164">Hello Pluralsight applicazione prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="8fad6-164">hello Pluralsight application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="8fad6-165">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="8fad6-165">hello following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="8fad6-167">È inoltre possibile aggiungere hello **"ID univoco"** attributo con hello appropriato valore, ad esempio EmployeeID o un altro elemento che soddisfi per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8fad6-167">You can also add hello **"Unique ID"** attribute with hello appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="8fad6-168">Si noti inoltre che non si tratta di attributo obbligatorio hello; Tuttavia, è possibile aggiungere troppo identificare utente univoco hello.</span><span class="sxs-lookup"><span data-stu-id="8fad6-168">Also note that this is not hello required attribute; however, you can add it too identify hello unique user.</span></span> 

6. <span data-ttu-id="8fad6-169">hello tooadd necessario **attributi token SAML**, per ogni riga nella tabella hello riportata di seguito, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8fad6-169">tooadd hello required **SAML token attributes**, for each row shown in hello table below, perform hello following steps:</span></span>
   
   | <span data-ttu-id="8fad6-170">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="8fad6-170">Attribute Name</span></span> | <span data-ttu-id="8fad6-171">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="8fad6-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="8fad6-172">Nome</span><span class="sxs-lookup"><span data-stu-id="8fad6-172">First Name</span></span> |<span data-ttu-id="8fad6-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8fad6-173">user.givenname</span></span> |
   | <span data-ttu-id="8fad6-174">Cognome</span><span class="sxs-lookup"><span data-stu-id="8fad6-174">Last Name</span></span> |<span data-ttu-id="8fad6-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="8fad6-175">user.surname</span></span> |
   | <span data-ttu-id="8fad6-176">Email</span><span class="sxs-lookup"><span data-stu-id="8fad6-176">Email</span></span> |<span data-ttu-id="8fad6-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="8fad6-177">user.mail</span></span> |
   
   <span data-ttu-id="8fad6-178">a.</span><span class="sxs-lookup"><span data-stu-id="8fad6-178">a.</span></span> <span data-ttu-id="8fad6-179">Fare clic su **Aggiungi attributo utente** tooopen hello **aggiungere Attribure utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8fad6-179">Click **add user attribute** tooopen hello **Add User Attribure** dialog.</span></span>
    
     ![Configura accesso Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="8fad6-181">b.</span><span class="sxs-lookup"><span data-stu-id="8fad6-181">b.</span></span> <span data-ttu-id="8fad6-182">In hello **nome dell'attributo** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8fad6-182">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
  
   <span data-ttu-id="8fad6-183">c.</span><span class="sxs-lookup"><span data-stu-id="8fad6-183">c.</span></span> <span data-ttu-id="8fad6-184">Da hello **valore dell'attributo** elenco, il valore di attributo hello selezionare mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8fad6-184">From hello **Attribute Value** list, select hello attribute value shown for that row.</span></span>
  
   <span data-ttu-id="8fad6-185">d.</span><span class="sxs-lookup"><span data-stu-id="8fad6-185">d.</span></span> <span data-ttu-id="8fad6-186">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="8fad6-187">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8fad6-187">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8fad6-189">tooget SSO è configurato per l'applicazione, contattare [servizi professionali Pluralsight](mailTo:professionalservices@pluralsight.com) team e fornire il file di metadati scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="8fad6-189">tooget SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide hello downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="8fad6-190">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8fad6-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8fad6-191">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8fad6-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8fad6-192">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8fad6-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8fad6-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fad6-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="8fad6-194">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8fad6-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8fad6-196">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8fad6-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fad6-197">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8fad6-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8fad6-199">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8fad6-201">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="8fad6-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8fad6-203">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8fad6-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8fad6-205">a.</span><span class="sxs-lookup"><span data-stu-id="8fad6-205">a.</span></span> <span data-ttu-id="8fad6-206">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8fad6-207">b.</span><span class="sxs-lookup"><span data-stu-id="8fad6-207">b.</span></span> <span data-ttu-id="8fad6-208">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8fad6-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8fad6-209">c.</span><span class="sxs-lookup"><span data-stu-id="8fad6-209">c.</span></span> <span data-ttu-id="8fad6-210">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8fad6-211">d.</span><span class="sxs-lookup"><span data-stu-id="8fad6-211">d.</span></span> <span data-ttu-id="8fad6-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="8fad6-213">Creazione di un utente test Pluralsight</span><span class="sxs-lookup"><span data-stu-id="8fad6-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="8fad6-214">obiettivo di Hello di questa sezione è un utente denominato Britta Simon di Pluralsight toocreate.</span><span class="sxs-lookup"><span data-stu-id="8fad6-214">hello objective of this section is toocreate a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="8fad6-215">Rivolgersi [team di supporto Pluralsight Client](mailto:support@pluralsight.com) utenti hello tooadd hello Pluralsight account.</span><span class="sxs-lookup"><span data-stu-id="8fad6-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) tooadd hello users in hello Pluralsight account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8fad6-216">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fad6-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8fad6-217">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPluralsight.</span><span class="sxs-lookup"><span data-stu-id="8fad6-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPluralsight.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8fad6-219">**tooassign Britta Simon tooPluralsight, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8fad6-219">**tooassign Britta Simon tooPluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fad6-220">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8fad6-222">Nell'elenco di applicazioni hello, selezionare **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-222">In hello applications list, select **Pluralsight**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="8fad6-224">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8fad6-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-226">Click **Add** button.</span></span> <span data-ttu-id="8fad6-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8fad6-229">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8fad6-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8fad6-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8fad6-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8fad6-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8fad6-232">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8fad6-232">Testing single sign-on</span></span>

<span data-ttu-id="8fad6-233">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8fad6-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8fad6-234">Quando si fa clic su riquadro Pluralsight hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Pluralsight applicazione.</span><span class="sxs-lookup"><span data-stu-id="8fad6-234">When you click hello Pluralsight tile in hello Access Panel, you should get automatically signed-on tooyour Pluralsight application.</span></span> <span data-ttu-id="8fad6-235">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8fad6-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8fad6-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8fad6-236">Additional resources</span></span>

* [<span data-ttu-id="8fad6-237">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fad6-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8fad6-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fad6-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

