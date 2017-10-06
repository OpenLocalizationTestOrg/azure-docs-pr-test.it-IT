---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workpath | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Workpath.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 69f443f314edb7c8c489a6c193e09b6f8fe6795a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="8ce07-103">Esercitazione: Integrazione di Azure Active Directory con Workpath</span><span class="sxs-lookup"><span data-stu-id="8ce07-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="8ce07-104">In questa esercitazione, è illustrato come toointegrate Workpath con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ce07-104">In this tutorial, you learn how toointegrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ce07-105">Integrazione Workpath con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8ce07-105">Integrating Workpath with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8ce07-106">È possibile controllare in Azure AD che ha accesso tooWorkpath</span><span class="sxs-lookup"><span data-stu-id="8ce07-106">You can control in Azure AD who has access tooWorkpath</span></span>
- <span data-ttu-id="8ce07-107">È possibile abilitare l'utenti tooautomatically get connesso tooWorkpath (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce07-107">You can enable your users tooautomatically get signed-on tooWorkpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ce07-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8ce07-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8ce07-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ce07-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ce07-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8ce07-110">Prerequisites</span></span>

<span data-ttu-id="8ce07-111">integrazione di Azure AD con Workpath tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8ce07-111">tooconfigure Azure AD integration with Workpath, you need hello following items:</span></span>

- <span data-ttu-id="8ce07-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ce07-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ce07-113">Sottoscrizione di Workpath abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8ce07-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ce07-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8ce07-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ce07-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8ce07-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ce07-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8ce07-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ce07-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ce07-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ce07-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8ce07-118">Scenario description</span></span>
<span data-ttu-id="8ce07-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8ce07-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ce07-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8ce07-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ce07-121">Aggiunta di Workpath dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8ce07-121">Adding Workpath from hello gallery</span></span>
2. <span data-ttu-id="8ce07-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce07-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-hello-gallery"></a><span data-ttu-id="8ce07-123">Aggiunta di Workpath dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8ce07-123">Adding Workpath from hello gallery</span></span>
<span data-ttu-id="8ce07-124">integrazione hello tooconfigure di Workpath in Azure AD, è necessario tooadd Workpath dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8ce07-124">tooconfigure hello integration of Workpath into Azure AD, you need tooadd Workpath from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8ce07-125">**tooadd Workpath dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ce07-125">**tooadd Workpath from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ce07-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8ce07-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8ce07-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8ce07-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8ce07-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8ce07-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8ce07-133">Nella casella di ricerca hello, digitare **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-133">In hello search box, type **Workpath**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="8ce07-135">Nel riquadro dei risultati hello, selezionare **Workpath**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ce07-135">In hello results panel, select **Workpath**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ce07-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce07-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ce07-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workpath con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8ce07-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8ce07-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Workpath è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ce07-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workpath is tooa user in Azure AD.</span></span> <span data-ttu-id="8ce07-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Workpath deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8ce07-140">In other words, a link relationship between an Azure AD user and hello related user in Workpath needs toobe established.</span></span>

<span data-ttu-id="8ce07-141">In Workpath, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="8ce07-141">In Workpath, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8ce07-142">tooconfigure e prova AD Azure single sign-on con Workpath, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8ce07-142">tooconfigure and test Azure AD single sign-on with Workpath, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8ce07-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8ce07-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8ce07-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ce07-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ce07-145">**[Creazione di un utente test Workpath](#creating-a-workpath-test-user)**  -toohave un equivalente di Britta Simon in Workpath che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8ce07-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - toohave a counterpart of Britta Simon in Workpath that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ce07-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8ce07-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ce07-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8ce07-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ce07-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce07-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ce07-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Workpath.</span><span class="sxs-lookup"><span data-stu-id="8ce07-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="8ce07-150">**Azure AD tooconfigure single sign-on con Workpath, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ce07-150">**tooconfigure Azure AD single sign-on with Workpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ce07-151">Nel portale di Azure su hello hello **Workpath** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-151">In hello Azure portal, on hello **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8ce07-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8ce07-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="8ce07-155">In hello **Workpath dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità avviato da eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ce07-155">On hello **Workpath Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="8ce07-157">a.</span><span class="sxs-lookup"><span data-stu-id="8ce07-157">a.</span></span> <span data-ttu-id="8ce07-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="8ce07-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="8ce07-159">b.</span><span class="sxs-lookup"><span data-stu-id="8ce07-159">b.</span></span> <span data-ttu-id="8ce07-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="8ce07-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="8ce07-161">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="8ce07-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="8ce07-162">Se si desidera in un'applicazione hello tooconfigure **SP** , modalità iniziata da eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ce07-162">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="8ce07-164">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="8ce07-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8ce07-165">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="8ce07-165">These values are not real.</span></span> <span data-ttu-id="8ce07-166">Aggiornare questi valori con URL hello effettivo Sign-on, l'identificatore e l'URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="8ce07-166">Update these values with hello actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="8ce07-167">Contatto [team di supporto Workpath](https://help.workpath.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="8ce07-167">Contact [Workpath support team](https://help.workpath.com) tooget these values.</span></span>

5. <span data-ttu-id="8ce07-168">Applicazione di Workpath prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="8ce07-168">Workpath application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="8ce07-169">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="8ce07-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="8ce07-170">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8ce07-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8ce07-171">Hello seguente schermata illustra un esempio di questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="8ce07-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="8ce07-173">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ce07-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="8ce07-174">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="8ce07-174">Attribute Name</span></span> | <span data-ttu-id="8ce07-175">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="8ce07-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="8ce07-176">first_name</span><span class="sxs-lookup"><span data-stu-id="8ce07-176">first_name</span></span> | <span data-ttu-id="8ce07-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8ce07-177">user.givenname</span></span> |
    | <span data-ttu-id="8ce07-178">last_name</span><span class="sxs-lookup"><span data-stu-id="8ce07-178">last_name</span></span> | <span data-ttu-id="8ce07-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="8ce07-179">user.surname</span></span> |
    
    <span data-ttu-id="8ce07-180">a.</span><span class="sxs-lookup"><span data-stu-id="8ce07-180">a.</span></span> <span data-ttu-id="8ce07-181">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8ce07-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="8ce07-183">b.</span><span class="sxs-lookup"><span data-stu-id="8ce07-183">b.</span></span> <span data-ttu-id="8ce07-184">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8ce07-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="8ce07-186">c.</span><span class="sxs-lookup"><span data-stu-id="8ce07-186">c.</span></span> <span data-ttu-id="8ce07-187">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8ce07-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="8ce07-188">d.</span><span class="sxs-lookup"><span data-stu-id="8ce07-188">d.</span></span> <span data-ttu-id="8ce07-189">Lasciare hello **Namespace** casella di testo vuoto.</span><span class="sxs-lookup"><span data-stu-id="8ce07-189">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="8ce07-190">e.</span><span class="sxs-lookup"><span data-stu-id="8ce07-190">e.</span></span> <span data-ttu-id="8ce07-191">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="8ce07-192">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8ce07-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="8ce07-194">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8ce07-194">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="8ce07-196">In hello **Workpath configurazione** fare clic su **configurare Workpath** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="8ce07-196">On hello **Workpath Configuration** section, click **Configure Workpath** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8ce07-197">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="8ce07-197">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="8ce07-199">tooconfigure single sign-on sul **Workpath** lato, è necessario hello toosend scaricato **Metadata XML**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** troppo[team di supporto Workpath](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="8ce07-199">tooconfigure single sign-on on **Workpath** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="8ce07-200">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8ce07-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8ce07-201">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8ce07-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8ce07-202">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ce07-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ce07-203">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce07-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ce07-204">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8ce07-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8ce07-206">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ce07-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ce07-207">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8ce07-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ce07-209">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ce07-211">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="8ce07-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ce07-213">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ce07-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ce07-215">a.</span><span class="sxs-lookup"><span data-stu-id="8ce07-215">a.</span></span> <span data-ttu-id="8ce07-216">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ce07-217">b.</span><span class="sxs-lookup"><span data-stu-id="8ce07-217">b.</span></span> <span data-ttu-id="8ce07-218">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ce07-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ce07-219">c.</span><span class="sxs-lookup"><span data-stu-id="8ce07-219">c.</span></span> <span data-ttu-id="8ce07-220">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8ce07-221">d.</span><span class="sxs-lookup"><span data-stu-id="8ce07-221">d.</span></span> <span data-ttu-id="8ce07-222">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="8ce07-223">Creazione di un utente di test di Workpath</span><span class="sxs-lookup"><span data-stu-id="8ce07-223">Creating a Workpath test user</span></span>

<span data-ttu-id="8ce07-224">Workpath supporta il provisioning utenti JIT.</span><span class="sxs-lookup"><span data-stu-id="8ce07-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="8ce07-225">Dopo l'autenticazione degli utenti vengono creati automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8ce07-225">After authentication users are created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8ce07-226">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce07-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8ce07-227">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWorkpath.</span><span class="sxs-lookup"><span data-stu-id="8ce07-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkpath.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8ce07-229">**tooassign Britta Simon tooWorkpath, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ce07-229">**tooassign Britta Simon tooWorkpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ce07-230">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8ce07-232">Nell'elenco di applicazioni hello, selezionare **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-232">In hello applications list, select **Workpath**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="8ce07-234">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8ce07-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-236">Click **Add** button.</span></span> <span data-ttu-id="8ce07-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8ce07-239">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8ce07-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8ce07-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ce07-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8ce07-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ce07-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8ce07-242">Testing single sign-on</span></span>

<span data-ttu-id="8ce07-243">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8ce07-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8ce07-244">Quando si fa clic su riquadro Workpath hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Workpath applicazione.</span><span class="sxs-lookup"><span data-stu-id="8ce07-244">When you click hello Workpath tile in hello Access Panel, you should get automatically signed-on tooyour Workpath application.</span></span>
<span data-ttu-id="8ce07-245">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8ce07-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ce07-246">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8ce07-246">Additional resources</span></span>

* [<span data-ttu-id="8ce07-247">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ce07-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ce07-248">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ce07-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

