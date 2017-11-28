---
title: 'Esercitazione: integrazione di Azure Active Directory con iLMS | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e iLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="8c9ee-103">Esercitazione: Integrazione di Azure Active Directory con iLMS</span><span class="sxs-lookup"><span data-stu-id="8c9ee-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="8c9ee-104">In questa esercitazione, è illustrato come iLMS toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c9ee-104">In this tutorial, you learn how toointegrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c9ee-105">Integrazione iLMS con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-105">Integrating iLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8c9ee-106">È possibile controllare in Azure AD che ha accesso tooiLMS</span><span class="sxs-lookup"><span data-stu-id="8c9ee-106">You can control in Azure AD who has access tooiLMS</span></span>
- <span data-ttu-id="8c9ee-107">È possibile abilitare l'utenti tooautomatically get connesso tooiLMS (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c9ee-107">You can enable your users tooautomatically get signed-on tooiLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8c9ee-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8c9ee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8c9ee-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c9ee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c9ee-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8c9ee-110">Prerequisites</span></span>

<span data-ttu-id="8c9ee-111">integrazione di Azure AD con iLMS tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-111">tooconfigure Azure AD integration with iLMS, you need hello following items:</span></span>

- <span data-ttu-id="8c9ee-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c9ee-113">Sottoscrizione di iLMS abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8c9ee-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8c9ee-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8c9ee-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c9ee-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8c9ee-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c9ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c9ee-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8c9ee-118">Scenario description</span></span>
<span data-ttu-id="8c9ee-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c9ee-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c9ee-121">Aggiunta di iLMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8c9ee-121">Adding iLMS from hello gallery</span></span>
2. <span data-ttu-id="8c9ee-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c9ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-hello-gallery"></a><span data-ttu-id="8c9ee-123">Aggiunta di iLMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8c9ee-123">Adding iLMS from hello gallery</span></span>
<span data-ttu-id="8c9ee-124">integrazione hello tooconfigure di iLMS in Azure AD, è necessario iLMS tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-124">tooconfigure hello integration of iLMS into Azure AD, you need tooadd iLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8c9ee-125">**iLMS tooadd dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8c9ee-125">**tooadd iLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c9ee-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8c9ee-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8c9ee-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8c9ee-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-131">tooadd new application, click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8c9ee-133">Nella casella di ricerca hello, digitare **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-133">In hello search box, type **iLMS**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="8c9ee-135">Nel riquadro dei risultati hello, selezionare **iLMS**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-135">In hello results panel, select **iLMS**, then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8c9ee-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c9ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8c9ee-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con iLMS in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8c9ee-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8c9ee-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in iLMS è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in iLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="8c9ee-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in iLMS deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-140">In other words, a link relationship between an Azure AD user and hello related user in iLMS needs toobe established.</span></span>

<span data-ttu-id="8c9ee-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in iLMS.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in iLMS.</span></span>

<span data-ttu-id="8c9ee-142">tooconfigure e prova AD Azure single sign-on con iLMS, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-142">tooconfigure and test Azure AD single sign-on with iLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8c9ee-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8c9ee-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c9ee-145">**[Creazione di un utente test iLMS](#creating-an-ilms-test-user)**  -toohave un equivalente di Britta Simon in iLMS toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - toohave a counterpart of Britta Simon in iLMS that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="8c9ee-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c9ee-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8c9ee-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c9ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8c9ee-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione iLMS.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="8c9ee-150">**Azure AD tooconfigure single sign-on con iLMS, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8c9ee-150">**tooconfigure Azure AD single sign-on with iLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c9ee-151">Nel portale di Azure su hello hello **iLMS** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-151">In hello Azure portal, on hello **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8c9ee-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="8c9ee-155">In hello **iLMS dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-155">On hello **iLMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="8c9ee-157">a.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-157">a.</span></span> <span data-ttu-id="8c9ee-158">In hello **identificatore** casella di testo, incollare hello **identificatore** valore copiate da **Provider di servizi** sezione delle impostazioni di SAML nel portale di amministrazione iLMS.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-158">In hello **Identifier** textbox, paste hello **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="8c9ee-159">b.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-159">b.</span></span> <span data-ttu-id="8c9ee-160">In hello **URL di risposta** casella di testo, incollare hello **Endpoint (URL)** valore copiate da **Provider di servizi** sezione delle impostazioni di SAML nel portale di amministrazione iLMS con seguente hello modello`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="8c9ee-160">In hello **Reply URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having hello following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="8c9ee-161">Questo '123456' è un valore di esempio dell'identificatore.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="8c9ee-162">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="8c9ee-164">In hello **Sign-on URL** casella di testo, incollare hello **Endpoint (URL)** valore copiate da **Provider di servizi** sezione delle impostazioni di SAML nel portale di amministrazione iLMS come`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="8c9ee-164">In hello **Sign-on URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="8c9ee-165">tooenable JIT provisioning, iLMS prevista dall'applicazione asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-165">tooenable JIT provisioning, iLMS application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="8c9ee-166">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="8c9ee-167">È possibile gestire i valori hello di questi attributi da hello **gli attributi utente** sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-167">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="8c9ee-168">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-168">hello following screenshot shows an example for this.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="8c9ee-170">Creare **reparto, area** e **divisione** gli attributi e aggiungere il nome di hello di questi attributi in iLMS.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-170">Create **Department, Region** and **Division** attributes and add hello name of these attributes in iLMS.</span></span> <span data-ttu-id="8c9ee-171">Tutti gli attributi indicati sopra sono obbligatori.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-171">All these attributes shown above are required.</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="8c9ee-172">Si dispone di tooenable **creare Account utente Un-recognized** in iLMS toomap questi attributi.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-172">You have tooenable **Create Un-recognized User Account** in iLMS toomap these attributes.</span></span> <span data-ttu-id="8c9ee-173">Seguire le istruzioni di hello [qui](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget un'idea configurazione attributi hello.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-173">Follow hello instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget an idea on hello attributes configuration.</span></span>

6. <span data-ttu-id="8c9ee-174">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-174">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="8c9ee-175">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="8c9ee-175">Attribute Name</span></span> | <span data-ttu-id="8c9ee-176">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="8c9ee-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="8c9ee-177">divisione</span><span class="sxs-lookup"><span data-stu-id="8c9ee-177">division</span></span> | <span data-ttu-id="8c9ee-178">user.department</span><span class="sxs-lookup"><span data-stu-id="8c9ee-178">user.department</span></span> |
    | <span data-ttu-id="8c9ee-179">region</span><span class="sxs-lookup"><span data-stu-id="8c9ee-179">region</span></span> | <span data-ttu-id="8c9ee-180">user.state</span><span class="sxs-lookup"><span data-stu-id="8c9ee-180">user.state</span></span> |
    | <span data-ttu-id="8c9ee-181">department</span><span class="sxs-lookup"><span data-stu-id="8c9ee-181">department</span></span> | <span data-ttu-id="8c9ee-182">user. jobtitle</span><span class="sxs-lookup"><span data-stu-id="8c9ee-182">user.jobtitle</span></span> |

    <span data-ttu-id="8c9ee-183">a.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-183">a.</span></span> <span data-ttu-id="8c9ee-184">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-184">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="8c9ee-187">b.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-187">b.</span></span> <span data-ttu-id="8c9ee-188">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-188">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8c9ee-189">c.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-189">c.</span></span> <span data-ttu-id="8c9ee-190">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-190">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8c9ee-191">d.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-191">d.</span></span> <span data-ttu-id="8c9ee-192">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="8c9ee-192">Click **Ok**</span></span>

7. <span data-ttu-id="8c9ee-193">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-193">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="8c9ee-195">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8c9ee-195">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="8c9ee-197">In una finestra del web browser, accedere tooyour **il portale di amministrazione di iLMS** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-197">In a different web browser window, log in tooyour **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="8c9ee-198">Fare clic su **SSO:SAML** in **impostazioni** scheda Impostazioni SAML tooopen ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-198">Click **SSO:SAML** under **Settings** tab tooopen SAML settings and perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="8c9ee-200">a.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-200">a.</span></span> <span data-ttu-id="8c9ee-201">Espandere hello **Provider di servizi** hello sezione e copia **identificatore** e **Endpoint (URL)** valore.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-201">Expand hello **Service Provider** section and copy hello **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="8c9ee-203">b.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-203">b.</span></span> <span data-ttu-id="8c9ee-204">Nella sezione **Provider di identità** fare clic su **Import metadata** (Importa metadati).</span><span class="sxs-lookup"><span data-stu-id="8c9ee-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="8c9ee-205">c.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-205">c.</span></span> <span data-ttu-id="8c9ee-206">Seleziona hello **metadati** file scaricato dal portale di Azure dalla **certificato di firma SAML** sezione.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-206">Select hello **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="8c9ee-208">d.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-208">d.</span></span> <span data-ttu-id="8c9ee-209">Se si desidera tooenable JIT provisioning toocreate iLMS account per annullare-riconosce gli utenti, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-209">If you want tooenable JIT provisioning toocreate iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="8c9ee-210">Selezionare **Create Un-recognized User Account** (Crea account utente non riconosciuto).</span><span class="sxs-lookup"><span data-stu-id="8c9ee-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="8c9ee-212">Eseguire il mapping di attributi hello in Azure AD con attributi hello in iLMS.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-212">Map hello attributes in Azure AD with hello attributes in iLMS.</span></span> <span data-ttu-id="8c9ee-213">Nella colonna attributo hello, specificare gli attributi hello hello nome o il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-213">In hello attribute column, specify hello attributes name or hello default value.</span></span>

    <span data-ttu-id="8c9ee-214">e.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-214">e.</span></span> <span data-ttu-id="8c9ee-215">Andare troppo**regole Business** scheda ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-215">Go too**Business Rules** tab and perform hello following steps:</span></span> 
        
       ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="8c9ee-217">Controllare **creare aree Un-recognized, divisioni e i reparti** toocreate aree, divisioni e i reparti che non esistono già in fase di hello di Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-217">Check **Create Un-recognized Regions, Divisions and Departments** toocreate Regions, Divisions, and Departments that do not already exist at hello time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="8c9ee-218">Controllare **profilo utente aggiornamento durante Accedi** toospecify se hello del profilo utente viene aggiornata con ogni Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-218">Check **Update User Profile During Sign-in** toospecify whether hello user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="8c9ee-219">Se hello **"Aggiornamento vuoto valori per Non campi nel profilo utente obbligatorio"** opzione è selezionata, i campi facoltativi profilo vuoti al momento dell'accesso verrà inoltre causano hello iLMS profilo utente toocontain valori vuoti per i campi.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-219">If hello **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause hello user’s iLMS profile toocontain blank values for those fields.</span></span>
        
       - <span data-ttu-id="8c9ee-220">Controllare **inviare posta elettronica di notifica di errore** e immettere la posta elettronica hello dell'utente hello in cui si desidera tooreceive hello errore notifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-220">Check **Send Error Notification Email** and enter hello email of hello user where you want tooreceive hello error notification email.</span></span>

11. <span data-ttu-id="8c9ee-221">Fare clic su **salvare** pulsante Impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-221">Click **Save** button toosave hello settings.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="8c9ee-223">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8c9ee-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8c9ee-224">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8c9ee-225">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8c9ee-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8c9ee-226">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c9ee-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="8c9ee-227">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8c9ee-229">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8c9ee-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c9ee-230">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8c9ee-232">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-232">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8c9ee-234">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-234">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8c9ee-236">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8c9ee-238">a.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-238">a.</span></span> <span data-ttu-id="8c9ee-239">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c9ee-240">b.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-240">b.</span></span> <span data-ttu-id="8c9ee-241">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8c9ee-242">c.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-242">c.</span></span> <span data-ttu-id="8c9ee-243">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8c9ee-244">d.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-244">d.</span></span> <span data-ttu-id="8c9ee-245">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="8c9ee-246">Creazione di un utente test di iLMS</span><span class="sxs-lookup"><span data-stu-id="8c9ee-246">Creating an iLMS test user</span></span>

<span data-ttu-id="8c9ee-247">L'applicazione supporta solo in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti viene creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-247">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="8c9ee-248">JIT funzionerà, se si è scelto di hello **creare Account utente Un-recognized** casella di controllo durante l'impostazione di configurazione SAML nel portale di amministrazione iLMS.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-248">JIT will work, if you have clicked hello **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="8c9ee-249">Se è necessario un utente toocreate manualmente, quindi seguire i passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="8c9ee-249">If you need toocreate an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="8c9ee-250">Accedere nel sito della società di tooyour iLMS come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-250">Log in tooyour iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="8c9ee-251">Fare clic su **"Registrazione utente"** in **utenti** scheda tooopen **registrazione utente** pagina.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-251">Click **“Register User”** under **Users** tab tooopen **Register User** page.</span></span> 
   
   ![Aggiungere un dipendente](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="8c9ee-253">In hello **"Registrazione utente"** eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-253">On hello **“Register User”** page, perform hello following steps.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="8c9ee-255">a.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-255">a.</span></span> <span data-ttu-id="8c9ee-256">In hello **nome** casella Tipo hello Laura nome.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-256">In hello **First Name** textbox, type hello first name Britta.</span></span>
   
    <span data-ttu-id="8c9ee-257">b.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-257">b.</span></span> <span data-ttu-id="8c9ee-258">In hello **cognome** casella di testo, hello tipo cognome Simon.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-258">In hello **Last Name** textbox, type hello last name Simon.</span></span>

    <span data-ttu-id="8c9ee-259">c.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-259">c.</span></span> <span data-ttu-id="8c9ee-260">In hello **ID di posta elettronica** casella di testo, digitare hello indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-260">In hello **Email ID** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="8c9ee-261">d.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-261">d.</span></span> <span data-ttu-id="8c9ee-262">In hello **area** elenco a discesa valore selezionare hello per area.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-262">In hello **Region** dropdown, select hello value for region.</span></span>

    <span data-ttu-id="8c9ee-263">e.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-263">e.</span></span> <span data-ttu-id="8c9ee-264">In hello **divisione** elenco a discesa valore selezionare hello per la divisione.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-264">In hello **Division** dropdown, select hello value for division.</span></span>

    <span data-ttu-id="8c9ee-265">f.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-265">f.</span></span> <span data-ttu-id="8c9ee-266">In hello **reparto** elenco a discesa valore selezionare hello per reparto.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-266">In hello **Department** dropdown, select hello value for department.</span></span>

    <span data-ttu-id="8c9ee-267">g.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-267">g.</span></span> <span data-ttu-id="8c9ee-268">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8c9ee-269">È possibile inviare toouser di posta elettronica di registrazione selezionando **invia messaggi di registrazione** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-269">You can send registration mail toouser by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8c9ee-270">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c9ee-270">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8c9ee-271">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooiLMS proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-271">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooiLMS.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8c9ee-273">**tooassign Britta Simon tooiLMS, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8c9ee-273">**tooassign Britta Simon tooiLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c9ee-274">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-274">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8c9ee-276">Nell'elenco di applicazioni hello, selezionare **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-276">In hello applications list, select **iLMS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="8c9ee-278">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-278">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8c9ee-280">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-280">Click **Add** button.</span></span> <span data-ttu-id="8c9ee-281">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8c9ee-283">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-283">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8c9ee-284">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8c9ee-285">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8c9ee-286">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8c9ee-286">Testing single sign-on</span></span>

<span data-ttu-id="8c9ee-287">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-287">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8c9ee-288">Quando si fa clic hello iLMS riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour iLMS applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c9ee-288">When you click hello iLMS tile in hello Access Panel, you should get automatically signed-on tooyour iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8c9ee-289">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8c9ee-289">Additional resources</span></span>

* [<span data-ttu-id="8c9ee-290">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c9ee-290">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c9ee-291">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c9ee-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

