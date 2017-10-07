---
title: 'Esercitazione: Integrazione di Azure Active Directory con ServiceChannel | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ServiceChannel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="cc1d5-103">Esercitazione: Integrazione di Azure Active Directory con ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="cc1d5-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="cc1d5-104">In questa esercitazione, è illustrato come toointegrate ServiceChannel con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc1d5-104">In this tutorial, you learn how toointegrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc1d5-105">Integrazione di ServiceChannel con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="cc1d5-105">Integrating ServiceChannel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc1d5-106">È possibile controllare in Azure AD che ha accesso tooServiceChannel</span><span class="sxs-lookup"><span data-stu-id="cc1d5-106">You can control in Azure AD who has access tooServiceChannel</span></span>
- <span data-ttu-id="cc1d5-107">È possibile abilitare l'utenti tooautomatically get connesso tooServiceChannel (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1d5-107">You can enable your users tooautomatically get signed-on tooServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc1d5-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="cc1d5-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="cc1d5-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc1d5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc1d5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cc1d5-110">Prerequisites</span></span>

<span data-ttu-id="cc1d5-111">integrazione di Azure AD con ServiceChannel tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="cc1d5-111">tooconfigure Azure AD integration with ServiceChannel, you need hello following items:</span></span>

- <span data-ttu-id="cc1d5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc1d5-113">Sottoscrizione di ServiceChannel abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc1d5-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc1d5-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="cc1d5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc1d5-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cc1d5-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc1d5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc1d5-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cc1d5-118">Scenario description</span></span>
<span data-ttu-id="cc1d5-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc1d5-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="cc1d5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc1d5-121">Aggiunta di ServiceChannel dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cc1d5-121">Adding ServiceChannel from hello gallery</span></span>
2. <span data-ttu-id="cc1d5-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-hello-gallery"></a><span data-ttu-id="cc1d5-123">Aggiunta di ServiceChannel dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cc1d5-123">Adding ServiceChannel from hello gallery</span></span>
<span data-ttu-id="cc1d5-124">integrazione hello tooconfigure di ServiceChannel in Azure AD, è necessario tooadd ServiceChannel dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-124">tooconfigure hello integration of ServiceChannel into Azure AD, you need tooadd ServiceChannel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc1d5-125">**tooadd ServiceChannel dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc1d5-125">**tooadd ServiceChannel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc1d5-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc1d5-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc1d5-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="cc1d5-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="cc1d5-133">Nella casella di ricerca hello, digitare **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-133">In hello search box, type **ServiceChannel**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="cc1d5-135">Nel riquadro dei risultati hello, selezionare **ServiceChannel**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-135">In hello results panel, select **ServiceChannel**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc1d5-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1d5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc1d5-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con ServiceChannel con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc1d5-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc1d5-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ServiceChannel è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceChannel is tooa user in Azure AD.</span></span> <span data-ttu-id="cc1d5-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ServiceChannel deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-140">In other words, a link relationship between an Azure AD user and hello related user in ServiceChannel needs toobe established.</span></span>

<span data-ttu-id="cc1d5-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceChannel.</span></span>

<span data-ttu-id="cc1d5-142">tooconfigure e prova AD Azure single sign-on con ServiceChannel, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="cc1d5-142">tooconfigure and test Azure AD single sign-on with ServiceChannel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc1d5-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc1d5-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc1d5-145">**[Creazione di un utente test ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="cc1d5-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc1d5-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc1d5-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc1d5-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="cc1d5-150">**Azure AD tooconfigure single sign-on con ServiceChannel, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc1d5-150">**tooconfigure Azure AD single sign-on with ServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc1d5-151">Nel portale di gestione di Azure hello in hello **ServiceChannel** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-151">In hello Azure Management portal, on hello **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="cc1d5-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="cc1d5-155">In hello **ServiceChannel dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cc1d5-155">On hello **ServiceChannel Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="cc1d5-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-157">a.</span></span> <span data-ttu-id="cc1d5-158">In hello **identificatore** casella di testo, tipo di valore hello di:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="cc1d5-158">In hello **Identifier** textbox, type hello value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="cc1d5-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-159">b.</span></span> <span data-ttu-id="cc1d5-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="cc1d5-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc1d5-161">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="cc1d5-162">È necessario tooupdate questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="cc1d5-163">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="cc1d5-164">Contatto [team di supporto di ServiceChannel](https://servicechannel.zendesk.com/hc/en-us) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) tooget these values.</span></span>

4. <span data-ttu-id="cc1d5-165">L'applicazione di ServiceChannel prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-165">Your ServiceChannel application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="cc1d5-166">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-166">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="cc1d5-167">**NameIdentifier (ID utente)** è hello solo attestazioni obbligatorie e valore predefinito di hello è **User** ma ServiceChannel prevede che questo toobe mappato con **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-167">**NameIdentifier(User Identifier)** is hello only mandatory claim and hello default value is **user.userprincipalname** but ServiceChannel expects this toobe mapped with **user.mail**.</span></span> <span data-ttu-id="cc1d5-168">Se si prevede di provisioning utenti Just In Time tooenable, è consigliabile aggiungere hello seguenti attestazioni, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-168">If you are planning tooenable Just In Time user provisioning, then you should add hello following claims as shown below.</span></span> <span data-ttu-id="cc1d5-169">**Ruolo** attestazione deve toobe mappato troppo**user.assignedroles** che contiene il ruolo di hello di hello utente.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-169">**Role** claim needs toobe mapped too**user.assignedroles** which contains hello role of hello user.</span></span>  

    <span data-ttu-id="cc1d5-170">Per altre istruzioni sulle attestazioni, fare riferimento alla guida di ServiceChannel [qui](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example).</span><span class="sxs-lookup"><span data-stu-id="cc1d5-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="cc1d5-172">Fare clic su [qui](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow come tooconfigure **ruolo** in Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1d5-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow how tooconfigure **Role** in Azure AD</span></span>

5. <span data-ttu-id="cc1d5-173">In **gli attributi utente** fare clic su **visualizzare e modificare tutti gli altri attributi utente** e impostare gli attributi di hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span>

    | <span data-ttu-id="cc1d5-174">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="cc1d5-174">Attribute Name</span></span> | <span data-ttu-id="cc1d5-175">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="cc1d5-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="cc1d5-176">Ruolo</span><span class="sxs-lookup"><span data-stu-id="cc1d5-176">Role</span></span>| <span data-ttu-id="cc1d5-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="cc1d5-177">user.assignedroles</span></span> |

    <span data-ttu-id="cc1d5-178">a.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-178">a.</span></span> <span data-ttu-id="cc1d5-179">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="cc1d5-182">b.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-182">b.</span></span> <span data-ttu-id="cc1d5-183">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="cc1d5-184">c.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-184">c.</span></span> <span data-ttu-id="cc1d5-185">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="cc1d5-186">d.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-186">d.</span></span> <span data-ttu-id="cc1d5-187">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="cc1d5-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="cc1d5-188">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="cc1d5-190">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-190">Click **Save**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cc1d5-192">In hello **ServiceChannel configurazione** fare clic su **configurare ServiceChannel** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-192">On hello **ServiceChannel Configuration** section, click **Configure ServiceChannel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cc1d5-193">Si noti hello **ID entità SAML** da hello **riferimento rapido** sezione.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-193">Please note hello **SAML Enitity ID** from hello **Quick Reference** section.</span></span>

9. <span data-ttu-id="cc1d5-194">tooconfigure single sign-on sul **ServiceChannel** lato, è necessario hello toosend scaricato **certificato (Base64)** e **ID entità SAML** troppo[ Il team di supporto di ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="cc1d5-194">tooconfigure single sign-on on **ServiceChannel** side, you need toosend hello downloaded **certificate (Base64)** and **SAML Entity ID** too[ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="cc1d5-195">Verrà impostata questa in hello toohave ordine connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-195">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc1d5-196">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1d5-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc1d5-197">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-197">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="cc1d5-199">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc1d5-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc1d5-200">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-200">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc1d5-202">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-202">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc1d5-204">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-204">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc1d5-206">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cc1d5-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc1d5-208">a.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-208">a.</span></span> <span data-ttu-id="cc1d5-209">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc1d5-210">b.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-210">b.</span></span> <span data-ttu-id="cc1d5-211">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc1d5-212">c.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-212">c.</span></span> <span data-ttu-id="cc1d5-213">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cc1d5-214">d.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-214">d.</span></span> <span data-ttu-id="cc1d5-215">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="cc1d5-216">Creazione di un utente test di ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="cc1d5-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="cc1d5-217">L'applicazione supporta solo in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti verrà creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-217">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="cc1d5-218">Per eseguire il provisioning degli utenti completo, contattare il [team di supporto di ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="cc1d5-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cc1d5-219">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc1d5-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cc1d5-220">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooServiceChannel proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceChannel.</span></span>

![Assegna utente][200] 

<span data-ttu-id="cc1d5-222">**tooassign Britta Simon tooServiceChannel, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc1d5-222">**tooassign Britta Simon tooServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc1d5-223">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cc1d5-225">Nell'elenco di applicazioni hello, selezionare **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-225">In hello applications list, select **ServiceChannel**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="cc1d5-227">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="cc1d5-229">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-229">Click **Add** button.</span></span> <span data-ttu-id="cc1d5-230">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="cc1d5-232">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc1d5-233">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc1d5-234">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc1d5-235">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cc1d5-235">Testing single sign-on</span></span>

<span data-ttu-id="cc1d5-236">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cc1d5-237">Quando si fa clic su riquadro ServiceChannel hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour ServiceChannel applicazione.</span><span class="sxs-lookup"><span data-stu-id="cc1d5-237">When you click hello ServiceChannel tile in hello Access Panel, you should get automatically signed-on tooyour ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc1d5-238">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cc1d5-238">Additional resources</span></span>

* [<span data-ttu-id="cc1d5-239">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc1d5-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc1d5-240">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc1d5-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png