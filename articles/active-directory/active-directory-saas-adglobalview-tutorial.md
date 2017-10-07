---
title: 'Esercitazione: Integrazione di Azure Active Directory con ADP Globalview | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ADP Globalview.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: aee2d56f05b486d12facbc41c9503455094604ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="0caee-103">Esercitazione: Integrazione di Azure Active Directory con ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="0caee-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="0caee-104">In questa esercitazione, è illustrato come toointegrate ADP Globalview con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0caee-104">In this tutorial, you learn how toointegrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0caee-105">Integrazione ADP Globalview con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0caee-105">Integrating ADP Globalview with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0caee-106">È possibile controllare in Azure AD che ha accesso tooADP Globalview</span><span class="sxs-lookup"><span data-stu-id="0caee-106">You can control in Azure AD who has access tooADP Globalview</span></span>
- <span data-ttu-id="0caee-107">È possibile abilitare l'utenti tooautomatically get connesso tooADP Globalview (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0caee-107">You can enable your users tooautomatically get signed-on tooADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0caee-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0caee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0caee-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0caee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0caee-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0caee-110">Prerequisites</span></span>

<span data-ttu-id="0caee-111">integrazione di Azure AD con ADP Globalview tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0caee-111">tooconfigure Azure AD integration with ADP Globalview, you need hello following items:</span></span>

- <span data-ttu-id="0caee-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0caee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0caee-113">Sottoscrizione di ADP Globalview abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0caee-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0caee-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0caee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0caee-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="0caee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0caee-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0caee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0caee-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0caee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0caee-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0caee-118">Scenario description</span></span>
<span data-ttu-id="0caee-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0caee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0caee-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="0caee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0caee-121">Aggiunta di ADP Globalview dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0caee-121">Adding ADP Globalview from hello gallery</span></span>
2. <span data-ttu-id="0caee-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0caee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-hello-gallery"></a><span data-ttu-id="0caee-123">Aggiunta di ADP Globalview dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0caee-123">Adding ADP Globalview from hello gallery</span></span>
<span data-ttu-id="0caee-124">integrazione hello tooconfigure di ADP Globalview in Azure AD, è necessario tooadd ADP Globalview dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0caee-124">tooconfigure hello integration of ADP Globalview into Azure AD, you need tooadd ADP Globalview from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0caee-125">**tooadd ADP Globalview dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0caee-125">**tooadd ADP Globalview from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0caee-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0caee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0caee-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0caee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0caee-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0caee-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0caee-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0caee-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0caee-133">Nella casella di ricerca hello, digitare **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="0caee-133">In hello search box, type **ADP Globalview**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="0caee-135">Nel riquadro dei risultati hello, selezionare **ADP Globalview**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0caee-135">In hello results panel, select **ADP Globalview**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0caee-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0caee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0caee-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ADP Globalview mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0caee-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0caee-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ADP Globalview è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0caee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP Globalview is tooa user in Azure AD.</span></span> <span data-ttu-id="0caee-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in ADP Globalview deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="0caee-140">In other words, a link relationship between an Azure AD user and hello related user in ADP Globalview needs toobe established.</span></span>

<span data-ttu-id="0caee-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="0caee-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP Globalview.</span></span>

<span data-ttu-id="0caee-142">tooconfigure e prova AD Azure single sign-on con ADP Globalview, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="0caee-142">tooconfigure and test Azure AD single sign-on with ADP Globalview, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0caee-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0caee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0caee-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0caee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0caee-145">**[Creazione di un utente test ADP Globalview](#creating-an-adp-globalview-test-user)**  -toohave un equivalente di Britta Simon in ADP Globalview che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0caee-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - toohave a counterpart of Britta Simon in ADP Globalview that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0caee-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0caee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0caee-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="0caee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0caee-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0caee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0caee-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="0caee-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="0caee-150">**Azure AD tooconfigure single sign-on con ADP Globalview, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0caee-150">**tooconfigure Azure AD single sign-on with ADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="0caee-151">Nel portale di Azure su hello hello **ADP Globalview** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0caee-151">In hello Azure portal, on hello **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0caee-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0caee-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="0caee-155">In hello **ADP Globalview dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0caee-155">On hello **ADP Globalview Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="0caee-157">In hello **identificatore** casella di testo, digitare un URL con modello di hello: `https://<subdomain>.globalview.adp.com/federate` o`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="0caee-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0caee-158">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="0caee-158">hello value is not real.</span></span> <span data-ttu-id="0caee-159">Aggiornare il valore di hello con hello identificatore effettivo.</span><span class="sxs-lookup"><span data-stu-id="0caee-159">Update hello value with hello actual Identifier.</span></span> <span data-ttu-id="0caee-160">Contatto [ADP Globalview supporto](https://www.adp.com/contact-us/overview.aspx) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="0caee-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooget hello value.</span></span>
 
4. <span data-ttu-id="0caee-161">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0caee-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="0caee-163">Hello ADP GlobalView applicazione prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="0caee-163">hello ADP GlobalView application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="0caee-164">Hello seguente schermata mostra un esempio relativo.</span><span class="sxs-lookup"><span data-stu-id="0caee-164">hello following screenshot shows an example for it.</span></span> <span data-ttu-id="0caee-165">Hello attestazione nomi sempre essere **"PersonImmutableID"** e il valore di hello di cui è stato eseguito il mapping di tooExtensionAttribute2, che contiene hello EmployeeID dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="0caee-165">hello claim names always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2, which contains hello EmployeeID of hello user.</span></span> <span data-ttu-id="0caee-166">Di seguito mapping utente hello da Azure AD tooADP GlobalView avviene su hello EmployeeID, ma è possibile eseguirne il mapping tooa valore diverso anche in base alle impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0caee-166">Here hello user mapping from Azure AD tooADP GlobalView is done on hello EmployeeID but you can map it tooa different value also based on your application settings.</span></span> <span data-ttu-id="0caee-167">È possibile utilizzare con hello ADP GlobalView team prima toouse hello identificativo corretto di un utente ed eseguire il mapping di tale valore con hello **"PersonImmutableID"** attestazione.</span><span class="sxs-lookup"><span data-stu-id="0caee-167">You can work with hello ADP GlobalView team first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="0caee-168">È anche possibile mappare hello posta elettronica e UserID attestazione come mostrato nell'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="0caee-168">You can also map hello Email and UserID claim as shown in hello picture.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="0caee-170">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0caee-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="0caee-171">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="0caee-171">Attribute Name</span></span> | <span data-ttu-id="0caee-172">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="0caee-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="0caee-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="0caee-173">personalimmutableid</span></span> | <span data-ttu-id="0caee-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="0caee-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="0caee-175">email</span><span class="sxs-lookup"><span data-stu-id="0caee-175">email</span></span>               | <span data-ttu-id="0caee-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="0caee-176">user.mail</span></span> |
    | <span data-ttu-id="0caee-177">userid</span><span class="sxs-lookup"><span data-stu-id="0caee-177">userid</span></span>              | <span data-ttu-id="0caee-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="0caee-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="0caee-179">a.</span><span class="sxs-lookup"><span data-stu-id="0caee-179">a.</span></span> <span data-ttu-id="0caee-180">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0caee-180">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0caee-183">b.</span><span class="sxs-lookup"><span data-stu-id="0caee-183">b.</span></span> <span data-ttu-id="0caee-184">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="0caee-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="0caee-185">c.</span><span class="sxs-lookup"><span data-stu-id="0caee-185">c.</span></span> <span data-ttu-id="0caee-186">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="0caee-186">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0caee-187">d.</span><span class="sxs-lookup"><span data-stu-id="0caee-187">d.</span></span> <span data-ttu-id="0caee-188">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0caee-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0caee-189">Prima di poter configurare l'asserzione SAML hello, è necessario toocontact il [ADP Globalview supporto](https://www.adp.com/contact-us/overview.aspx) e valore hello dell'attributo dell'identificatore univoco hello per le richieste per il tenant.</span><span class="sxs-lookup"><span data-stu-id="0caee-189">Before you can configure hello SAML assertion, you need toocontact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="0caee-190">È necessario l'attestazione personalizzata di hello tooconfigure valore per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0caee-190">You need this value tooconfigure hello custom claim for your application.</span></span> 

8. <span data-ttu-id="0caee-191">In hello **ADP Globalview configurazione** fare clic su **configurare ADP Globalview** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="0caee-191">On hello **ADP Globalview Configuration** section, click **Configure ADP Globalview** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0caee-192">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="0caee-192">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="0caee-194">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0caee-194">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="0caee-196">tooconfigure single sign-on sul **ADP Globalview** lato, è necessario hello toosend scaricato **certificato (Base64)**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** troppo[ADP Globalview supporto](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="0caee-196">tooconfigure single sign-on on **ADP Globalview** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="0caee-197">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="0caee-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0caee-198">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="0caee-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0caee-199">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0caee-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0caee-200">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0caee-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="0caee-201">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0caee-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0caee-203">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0caee-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0caee-204">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0caee-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="0caee-206">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0caee-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0caee-208">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="0caee-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0caee-210">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0caee-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0caee-212">a.</span><span class="sxs-lookup"><span data-stu-id="0caee-212">a.</span></span> <span data-ttu-id="0caee-213">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0caee-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0caee-214">b.</span><span class="sxs-lookup"><span data-stu-id="0caee-214">b.</span></span> <span data-ttu-id="0caee-215">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0caee-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0caee-216">c.</span><span class="sxs-lookup"><span data-stu-id="0caee-216">c.</span></span> <span data-ttu-id="0caee-217">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="0caee-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0caee-218">d.</span><span class="sxs-lookup"><span data-stu-id="0caee-218">d.</span></span> <span data-ttu-id="0caee-219">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0caee-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="0caee-220">Creazione di un utente test di ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="0caee-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="0caee-221">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in ADP GlobalView toocreate.</span><span class="sxs-lookup"><span data-stu-id="0caee-221">hello objective of this section is toocreate a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="0caee-222">Lavorare con [ADP Globalview supporto](https://www.adp.com/contact-us/overview.aspx) utenti hello tooadd hello ADP GlobalView account.</span><span class="sxs-lookup"><span data-stu-id="0caee-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP GlobalView account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0caee-223">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0caee-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0caee-224">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="0caee-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP Globalview.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0caee-226">**tooassign tooADP Britta Simon Globalview, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0caee-226">**tooassign Britta Simon tooADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="0caee-227">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0caee-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0caee-229">Nell'elenco di applicazioni hello, selezionare **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="0caee-229">In hello applications list, select **ADP Globalview**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="0caee-231">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0caee-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0caee-233">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0caee-233">Click **Add** button.</span></span> <span data-ttu-id="0caee-234">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0caee-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0caee-236">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="0caee-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0caee-237">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0caee-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0caee-238">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0caee-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0caee-239">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0caee-239">Testing single sign-on</span></span>

<span data-ttu-id="0caee-240">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0caee-240">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="0caee-241">Quando si fa clic hello ADP GlobalView riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour ADP GlobalView applicazione.</span><span class="sxs-lookup"><span data-stu-id="0caee-241">When you click hello ADP GlobalView tile in hello Access Panel, you should get automatically signed-on tooyour ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0caee-242">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0caee-242">Additional resources</span></span>

* [<span data-ttu-id="0caee-243">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0caee-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0caee-244">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0caee-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

