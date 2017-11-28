---
title: 'Esercitazione: Integrazione di Azure Active Directory con OfficeSpace Software | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e OfficeSpace Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="57ec0-103">Esercitazione: Integrazione di Azure Active Directory con OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="57ec0-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="57ec0-104">In questa esercitazione, è illustrato come toointegrate OfficeSpace Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57ec0-104">In this tutorial, you learn how toointegrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57ec0-105">Integrazione di OfficeSpace Software con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="57ec0-105">Integrating OfficeSpace Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="57ec0-106">È possibile controllare in Azure AD che ha accesso tooOfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="57ec0-106">You can control in Azure AD who has access tooOfficeSpace Software.</span></span>
- <span data-ttu-id="57ec0-107">È possibile abilitare l'utenti tooautomatically get connesso tooOfficeSpace Software (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57ec0-107">You can enable your users tooautomatically get signed-on tooOfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="57ec0-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57ec0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="57ec0-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57ec0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57ec0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="57ec0-110">Prerequisites</span></span>

<span data-ttu-id="57ec0-111">tooconfigure integrazione di Azure AD con OfficeSpace Software, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="57ec0-111">tooconfigure Azure AD integration with OfficeSpace Software, you need hello following items:</span></span>

- <span data-ttu-id="57ec0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57ec0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57ec0-113">Sottoscrizione di OfficeSpace Software abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="57ec0-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57ec0-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="57ec0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57ec0-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="57ec0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57ec0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="57ec0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57ec0-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57ec0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57ec0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="57ec0-118">Scenario description</span></span>
<span data-ttu-id="57ec0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="57ec0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57ec0-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="57ec0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57ec0-121">Aggiunta di OfficeSpace Software dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="57ec0-121">Adding OfficeSpace Software from hello gallery</span></span>
2. <span data-ttu-id="57ec0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="57ec0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-hello-gallery"></a><span data-ttu-id="57ec0-123">Aggiunta di OfficeSpace Software dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="57ec0-123">Adding OfficeSpace Software from hello gallery</span></span>
<span data-ttu-id="57ec0-124">integrazione hello tooconfigure di OfficeSpace Software in Azure AD, è necessario tooadd OfficeSpace Software dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="57ec0-124">tooconfigure hello integration of OfficeSpace Software into Azure AD, you need tooadd OfficeSpace Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="57ec0-125">**tooadd OfficeSpace Software dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="57ec0-125">**tooadd OfficeSpace Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="57ec0-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="57ec0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="57ec0-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="57ec0-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="57ec0-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="57ec0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="57ec0-133">Nella casella di ricerca hello, digitare **OfficeSpace Software**selezionare **OfficeSpace Software** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="57ec0-133">In hello search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco dei risultati di OfficeSpace Software in hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="57ec0-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="57ec0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="57ec0-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con OfficeSpace Software usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="57ec0-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57ec0-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in OfficeSpace Software è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57ec0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OfficeSpace Software is tooa user in Azure AD.</span></span> <span data-ttu-id="57ec0-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in OfficeSpace Software richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="57ec0-138">In other words, a link relationship between an Azure AD user and hello related user in OfficeSpace Software needs toobe established.</span></span>

<span data-ttu-id="57ec0-139">In OfficeSpace Software, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="57ec0-139">In OfficeSpace Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="57ec0-140">tooconfigure e test Azure single sign-on AD con OfficeSpace Software, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="57ec0-140">tooconfigure and test Azure AD single sign-on with OfficeSpace Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="57ec0-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="57ec0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="57ec0-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57ec0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57ec0-143">**[Creare un utente test OfficeSpace Software](#create-a-officespace-software-test-user)**  -toohave un equivalente di Britta Simon in OfficeSpace Software che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="57ec0-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - toohave a counterpart of Britta Simon in OfficeSpace Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="57ec0-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="57ec0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57ec0-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="57ec0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="57ec0-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="57ec0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="57ec0-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="57ec0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="57ec0-148">**Azure AD tooconfigure single sign-on con OfficeSpace Software, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="57ec0-148">**tooconfigure Azure AD single sign-on with OfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="57ec0-149">Nel portale di Azure su hello hello **OfficeSpace Software** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-149">In hello Azure portal, on hello **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="57ec0-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="57ec0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="57ec0-153">In hello **OfficeSpace Software dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="57ec0-153">On hello **OfficeSpace Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="57ec0-155">a.</span><span class="sxs-lookup"><span data-stu-id="57ec0-155">a.</span></span> <span data-ttu-id="57ec0-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="57ec0-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="57ec0-157">b.</span><span class="sxs-lookup"><span data-stu-id="57ec0-157">b.</span></span> <span data-ttu-id="57ec0-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="57ec0-158">In hello **Identifier** textbox, type a URL using hello following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57ec0-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="57ec0-159">These values are not real.</span></span> <span data-ttu-id="57ec0-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="57ec0-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="57ec0-161">Contatto [team di supporto di OfficeSpace Software Client](mailto:support@officespacesoftware.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="57ec0-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) tooget these values.</span></span> 

4. <span data-ttu-id="57ec0-162">Applicazione di OfficeSpace Software prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="57ec0-162">OfficeSpace Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="57ec0-163">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="57ec0-163">Please configure hello following claims for this application.</span></span> <span data-ttu-id="57ec0-164">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57ec0-164">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="57ec0-165">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="57ec0-165">hello following screenshot shows an example for this.</span></span>
    
    ![Configurazione dell'attributo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="57ec0-167">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo Seleziona **user.mail** come **identificatore utente** e per ogni riga visualizzata Nella tabella hello riportata di seguito, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="57ec0-167">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="57ec0-168">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="57ec0-168">Attribute Name</span></span> | <span data-ttu-id="57ec0-169">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="57ec0-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="57ec0-170">email</span><span class="sxs-lookup"><span data-stu-id="57ec0-170">email</span></span> | <span data-ttu-id="57ec0-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="57ec0-171">user.mail</span></span> |
    | <span data-ttu-id="57ec0-172">name</span><span class="sxs-lookup"><span data-stu-id="57ec0-172">name</span></span> | <span data-ttu-id="57ec0-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="57ec0-173">user.displayname</span></span> |
    | <span data-ttu-id="57ec0-174">first_name</span><span class="sxs-lookup"><span data-stu-id="57ec0-174">first_name</span></span> | <span data-ttu-id="57ec0-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="57ec0-175">user.givenname</span></span> |
    | <span data-ttu-id="57ec0-176">last_name</span><span class="sxs-lookup"><span data-stu-id="57ec0-176">last_name</span></span> | <span data-ttu-id="57ec0-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="57ec0-177">user.surname</span></span> |

    <span data-ttu-id="57ec0-178">a.</span><span class="sxs-lookup"><span data-stu-id="57ec0-178">a.</span></span> <span data-ttu-id="57ec0-179">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="57ec0-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="57ec0-180">Configurazione, aggiunta</span><span class="sxs-lookup"><span data-stu-id="57ec0-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Configurazione dell'attributo](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="57ec0-182">b.</span><span class="sxs-lookup"><span data-stu-id="57ec0-182">b.</span></span> <span data-ttu-id="57ec0-183">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="57ec0-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="57ec0-184">c.</span><span class="sxs-lookup"><span data-stu-id="57ec0-184">c.</span></span> <span data-ttu-id="57ec0-185">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="57ec0-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="57ec0-186">d.</span><span class="sxs-lookup"><span data-stu-id="57ec0-186">d.</span></span> <span data-ttu-id="57ec0-187">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="57ec0-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="57ec0-188">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="57ec0-188">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of hello certificate.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="57ec0-190">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="57ec0-190">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="57ec0-192">In hello **OfficeSpace Software configurazione** fare clic su **Configura OfficeSpace Software** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="57ec0-192">On hello **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="57ec0-193">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="57ec0-193">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="57ec0-195">In un'altra finestra del browser Web accedere al tenant di OfficeSpace Software come amministratore.</span><span class="sxs-lookup"><span data-stu-id="57ec0-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="57ec0-196">Andare troppo**impostazioni** e fare clic su **connettori**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-196">Go too**Settings** and click **Connectors**.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="57ec0-198">Fare clic su **Autenticazione SAML**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-198">Click **SAML Authentication**.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="57ec0-200">In hello **SAML Authentication** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="57ec0-200">In hello **SAML Authentication** section, perform hello following steps:</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="57ec0-202">a.</span><span class="sxs-lookup"><span data-stu-id="57ec0-202">a.</span></span> <span data-ttu-id="57ec0-203">In hello **Logout provider url** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57ec0-203">In hello **Logout provider url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="57ec0-204">b.</span><span class="sxs-lookup"><span data-stu-id="57ec0-204">b.</span></span> <span data-ttu-id="57ec0-205">In hello **Client idp target url** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57ec0-205">In hello **Client idp target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="57ec0-206">c.</span><span class="sxs-lookup"><span data-stu-id="57ec0-206">c.</span></span> <span data-ttu-id="57ec0-207">Hello Incolla **identificazione personale** valore a cui è stato copiato dal portale di Azure in hello **impronta digitale certificato Client IDP** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="57ec0-207">Paste hello **Thumbprint** value which you have copied from Azure portal, into hello **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="57ec0-208">d.</span><span class="sxs-lookup"><span data-stu-id="57ec0-208">d.</span></span> <span data-ttu-id="57ec0-209">Fare clic su **Salva impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="57ec0-210">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="57ec0-210">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="57ec0-211">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="57ec0-211">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="57ec0-212">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57ec0-212">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="57ec0-213">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="57ec0-213">Create an Azure AD test user</span></span>

<span data-ttu-id="57ec0-214">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="57ec0-214">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="57ec0-216">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="57ec0-216">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="57ec0-217">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="57ec0-217">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="57ec0-219">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-219">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="57ec0-221">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="57ec0-221">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="57ec0-223">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="57ec0-223">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="57ec0-225">a.</span><span class="sxs-lookup"><span data-stu-id="57ec0-225">a.</span></span> <span data-ttu-id="57ec0-226">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-226">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57ec0-227">b.</span><span class="sxs-lookup"><span data-stu-id="57ec0-227">b.</span></span> <span data-ttu-id="57ec0-228">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57ec0-228">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="57ec0-229">c.</span><span class="sxs-lookup"><span data-stu-id="57ec0-229">c.</span></span> <span data-ttu-id="57ec0-230">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="57ec0-230">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="57ec0-231">d.</span><span class="sxs-lookup"><span data-stu-id="57ec0-231">d.</span></span> <span data-ttu-id="57ec0-232">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="57ec0-233">Creare un utente di test di OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="57ec0-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="57ec0-234">obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon in OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="57ec0-234">hello objective of this section is toocreate a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="57ec0-235">OfficeSpace Software supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="57ec0-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="57ec0-236">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="57ec0-236">There is no action item for you in this section.</span></span> <span data-ttu-id="57ec0-237">Verrà creato un nuovo utente durante una tooaccess tentativo OfficeSpace Software se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="57ec0-237">A new user will be created during an attempt tooaccess OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="57ec0-238">Se è necessario un utente toocreate manualmente, è necessario tooContact [team di supporto di OfficeSpace Software](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="57ec0-238">If you need toocreate an user manually, you need tooContact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="57ec0-239">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="57ec0-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="57ec0-240">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooOfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="57ec0-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOfficeSpace Software.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="57ec0-242">**tooassign Britta Simon tooOfficeSpace Software, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="57ec0-242">**tooassign Britta Simon tooOfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="57ec0-243">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="57ec0-245">Nell'elenco di applicazioni hello, selezionare **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-245">In hello applications list, select **OfficeSpace Software**.</span></span>

    ![collegamento di OfficeSpace Software nell'elenco delle applicazioni hello Hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="57ec0-247">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="57ec0-249">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-249">Click **Add** button.</span></span> <span data-ttu-id="57ec0-250">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="57ec0-252">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="57ec0-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="57ec0-253">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57ec0-254">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="57ec0-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="57ec0-255">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="57ec0-255">Test single sign-on</span></span>

<span data-ttu-id="57ec0-256">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="57ec0-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="57ec0-257">Quando si fa clic hello OfficeSpace Software riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="57ec0-257">When you click hello OfficeSpace Software tile in hello Access Panel, you should get automatically signed-on tooyour OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57ec0-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="57ec0-258">Additional resources</span></span>

* [<span data-ttu-id="57ec0-259">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57ec0-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57ec0-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57ec0-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

