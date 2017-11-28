---
title: 'Esercitazione: Integrazione di Azure Active Directory con FilesAnywhere | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e FilesAnywhere.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="3e320-103">Esercitazione: Integrazione di Azure Active Directory con FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="3e320-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="3e320-104">In questa esercitazione, è illustrato come toointegrate FilesAnywhere con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e320-104">In this tutorial, you learn how toointegrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e320-105">Integrazione FilesAnywhere con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="3e320-105">Integrating FilesAnywhere with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3e320-106">È possibile controllare in Azure AD che ha accesso tooFilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="3e320-106">You can control in Azure AD who has access tooFilesAnywhere</span></span>
- <span data-ttu-id="3e320-107">È possibile abilitare l'utenti tooautomatically get connesso tooFilesAnywhere (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e320-107">You can enable your users tooautomatically get signed-on tooFilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e320-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="3e320-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="3e320-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e320-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e320-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3e320-110">Prerequisites</span></span>

<span data-ttu-id="3e320-111">integrazione di Azure AD con FilesAnywhere tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="3e320-111">tooconfigure Azure AD integration with FilesAnywhere, you need hello following items:</span></span>

- <span data-ttu-id="3e320-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e320-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e320-113">Sottoscrizione di FilesAnywhere abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3e320-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="3e320-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="3e320-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="3e320-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="3e320-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e320-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3e320-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3e320-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e320-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3e320-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3e320-118">Scenario description</span></span>
<span data-ttu-id="3e320-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3e320-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e320-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="3e320-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e320-121">Aggiunta di FilesAnywhere dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3e320-121">Adding FilesAnywhere from hello gallery</span></span>
2. <span data-ttu-id="3e320-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e320-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-hello-gallery"></a><span data-ttu-id="3e320-123">Aggiunta di FilesAnywhere dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3e320-123">Adding FilesAnywhere from hello gallery</span></span>
<span data-ttu-id="3e320-124">integrazione hello tooconfigure di FilesAnywhere in Azure AD, è necessario tooadd FilesAnywhere dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3e320-124">tooconfigure hello integration of FilesAnywhere into Azure AD, you need tooadd FilesAnywhere from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3e320-125">**tooadd FilesAnywhere dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e320-125">**tooadd FilesAnywhere from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e320-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="3e320-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e320-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3e320-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3e320-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e320-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="3e320-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="3e320-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="3e320-133">Nella casella di ricerca hello, digitare **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="3e320-133">In hello search box, type **FilesAnywhere**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="3e320-135">Nel riquadro dei risultati hello, selezionare **FilesAnywhere**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3e320-135">In hello results panel, select **FilesAnywhere**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e320-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e320-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e320-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FilesAnywhere in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3e320-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e320-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in FilesAnywhere è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e320-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FilesAnywhere is tooa user in Azure AD.</span></span> <span data-ttu-id="3e320-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in FilesAnywhere deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="3e320-140">In other words, a link relationship between an Azure AD user and hello related user in FilesAnywhere needs toobe established.</span></span>

<span data-ttu-id="3e320-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3e320-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="3e320-142">tooconfigure e prova AD Azure single sign-on con FilesAnywhere, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="3e320-142">tooconfigure and test Azure AD single sign-on with FilesAnywhere, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3e320-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3e320-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3e320-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e320-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e320-145">**[Creazione di un utente test FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave un equivalente di Britta Simon in FilesAnywhere toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="3e320-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - toohave a counterpart of Britta Simon in FilesAnywhere that is linked toohello Azure AD representation of her.</span></span>
3. <span data-ttu-id="3e320-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e320-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="3e320-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="3e320-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e320-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e320-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e320-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3e320-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="3e320-150">**Azure AD tooconfigure single sign-on con FilesAnywhere, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e320-150">**tooconfigure Azure AD single sign-on with FilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e320-151">Nel portale di gestione di Azure hello in hello **FilesAnywhere** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3e320-151">In hello Azure Management portal, on hello **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="3e320-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e320-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="3e320-155">In hello **FilesAnywhere dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**:</span><span class="sxs-lookup"><span data-stu-id="3e320-155">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="3e320-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e320-157">a.</span></span> <span data-ttu-id="3e320-158">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="3e320-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="3e320-159">Si noti il valore di hello **215** è un **clientid** ed è solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="3e320-159">Please note that hello value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="3e320-160">È necessario tooreplace con valore clientid effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="3e320-160">You need tooreplace it with hello actual clientid value.</span></span>

4. <span data-ttu-id="3e320-161">In hello **FilesAnywhere dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e320-161">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="3e320-163">a.</span><span class="sxs-lookup"><span data-stu-id="3e320-163">a.</span></span> <span data-ttu-id="3e320-164">Fare clic su hello **Mostra URL impostazioni avanzate** opzione</span><span class="sxs-lookup"><span data-stu-id="3e320-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="3e320-165">b.</span><span class="sxs-lookup"><span data-stu-id="3e320-165">b.</span></span> <span data-ttu-id="3e320-166">In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="3e320-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e320-167">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="3e320-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="3e320-168">È necessario tooupdate questi valori con hello URL di URL di accesso e di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="3e320-168">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="3e320-169">Contatto [team di supporto FilesAnywhere](mailto:support@FilesAnywhere.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="3e320-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) tooget these values.</span></span> 

5. <span data-ttu-id="3e320-170">Applicazione FilesAnywhere Software prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="3e320-170">FilesAnywhere Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="3e320-171">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e320-171">Please configure hello following claims for this application.</span></span> <span data-ttu-id="3e320-172">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e320-172">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="3e320-173">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="3e320-173">hello following screenshot shows an example for this.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="3e320-175">Hello quando gli utenti effettua l'iscrizione con FilesAnywhere ricevono valore hello **clientid** dall'attributo [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="3e320-175">When hello users signs up with FilesAnywhere they get hello value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="3e320-176">È l'attributo "Id Client" hello di tooadd con valore univoco di hello fornito da FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3e320-176">You have tooadd hello "Client Id" attribute with hello unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="3e320-177">Tutti gli attributi indicati sopra sono obbligatori.</span><span class="sxs-lookup"><span data-stu-id="3e320-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="3e320-178">Si noti il valore di hello **2331** di **clientid** è solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="3e320-178">Please note that hello value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="3e320-179">È necessario tooprovide valore effettivo di hello.</span><span class="sxs-lookup"><span data-stu-id="3e320-179">You need tooprovide hello actual value.</span></span>


6. <span data-ttu-id="3e320-180">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e320-180">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="3e320-181">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="3e320-181">Attribute Name</span></span> | <span data-ttu-id="3e320-182">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="3e320-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="3e320-183">clientid</span><span class="sxs-lookup"><span data-stu-id="3e320-183">clientid</span></span> | <span data-ttu-id="3e320-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="3e320-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="3e320-185">a.</span><span class="sxs-lookup"><span data-stu-id="3e320-185">a.</span></span> <span data-ttu-id="3e320-186">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3e320-186">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="3e320-189">b.</span><span class="sxs-lookup"><span data-stu-id="3e320-189">b.</span></span> <span data-ttu-id="3e320-190">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="3e320-190">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="3e320-191">c.</span><span class="sxs-lookup"><span data-stu-id="3e320-191">c.</span></span> <span data-ttu-id="3e320-192">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="3e320-192">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="3e320-193">d.</span><span class="sxs-lookup"><span data-stu-id="3e320-193">d.</span></span> <span data-ttu-id="3e320-194">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="3e320-194">Click **Ok**</span></span>

7. <span data-ttu-id="3e320-195">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3e320-195">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3e320-197">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="3e320-197">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="3e320-199">In hello **FilesAnywhere configurazione** fare clic su **configurare FilesAnywhere** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="3e320-199">On hello **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** tooopen **Configure sign-on** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="3e320-202">configurazione di SSO tooget completo per l'applicazione alla fine di FilesAnywhere, contattare [team di supporto FilesAnywhere](mailto:support@FilesAnywhere.com) e fornire loro token SAML hello scaricato URL Single Sign On (SSO) e di certificato di firma.</span><span class="sxs-lookup"><span data-stu-id="3e320-202">tooget SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them hello downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e320-203">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e320-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e320-204">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3e320-204">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="3e320-206">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e320-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e320-207">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="3e320-207">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e320-209">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="3e320-209">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e320-211">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3e320-211">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e320-213">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e320-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e320-215">a.</span><span class="sxs-lookup"><span data-stu-id="3e320-215">a.</span></span> <span data-ttu-id="3e320-216">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e320-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e320-217">b.</span><span class="sxs-lookup"><span data-stu-id="3e320-217">b.</span></span> <span data-ttu-id="3e320-218">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e320-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e320-219">c.</span><span class="sxs-lookup"><span data-stu-id="3e320-219">c.</span></span> <span data-ttu-id="3e320-220">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="3e320-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3e320-221">d.</span><span class="sxs-lookup"><span data-stu-id="3e320-221">d.</span></span> <span data-ttu-id="3e320-222">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3e320-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="3e320-223">Creare un utente test di FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="3e320-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="3e320-224">L'applicazione supporta solo in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti verrà creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3e320-224">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3e320-225">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e320-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3e320-226">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooFilesAnywhere proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="3e320-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFilesAnywhere.</span></span>

![Assegna utente][200] 

<span data-ttu-id="3e320-228">**tooassign Britta Simon tooFilesAnywhere, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e320-228">**tooassign Britta Simon tooFilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e320-229">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e320-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3e320-231">Nell'elenco di applicazioni hello, selezionare **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="3e320-231">In hello applications list, select **FilesAnywhere**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="3e320-233">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3e320-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="3e320-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3e320-235">Click **Add** button.</span></span> <span data-ttu-id="3e320-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3e320-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="3e320-238">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="3e320-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3e320-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3e320-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e320-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3e320-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="3e320-241">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3e320-241">Testing single sign-on</span></span>

<span data-ttu-id="3e320-242">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3e320-242">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3e320-243">Quando si fa clic su riquadro FilesAnywhere hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour FilesAnywhere applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e320-243">When you click hello FilesAnywhere tile in hello Access Panel, you should get automatically signed-on tooyour FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3e320-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3e320-244">Additional resources</span></span>

* [<span data-ttu-id="3e320-245">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e320-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e320-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e320-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
