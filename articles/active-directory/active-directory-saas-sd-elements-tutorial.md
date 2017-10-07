---
title: 'Esercitazione: Integrazione di Azure Active Directory con SD Elements| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e gli elementi SD.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="4ae21-103">Esercitazione: Integrazione di Azure Active Directory con SD Elements</span><span class="sxs-lookup"><span data-stu-id="4ae21-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="4ae21-104">In questa esercitazione, è illustrato come toointegrate elementi SD con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4ae21-104">In this tutorial, you learn how toointegrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ae21-105">L'integrazione di elementi SD con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4ae21-105">Integrating SD Elements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4ae21-106">È possibile controllare in Azure AD che ha accesso tooSD elementi</span><span class="sxs-lookup"><span data-stu-id="4ae21-106">You can control in Azure AD who has access tooSD Elements</span></span>
- <span data-ttu-id="4ae21-107">È possibile abilitare l'utenti tooautomatically get connesso tooSD elementi (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ae21-107">You can enable your users tooautomatically get signed-on tooSD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4ae21-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4ae21-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4ae21-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ae21-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ae21-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4ae21-110">Prerequisites</span></span>

<span data-ttu-id="4ae21-111">integrazione di Azure AD con elementi SD tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4ae21-111">tooconfigure Azure AD integration with SD Elements, you need hello following items:</span></span>

- <span data-ttu-id="4ae21-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ae21-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4ae21-113">Sottoscrizione di SD Elements abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4ae21-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4ae21-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4ae21-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4ae21-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4ae21-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4ae21-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4ae21-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4ae21-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ae21-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4ae21-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4ae21-118">Scenario description</span></span>
<span data-ttu-id="4ae21-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4ae21-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4ae21-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4ae21-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ae21-121">Aggiunta di elementi dalla raccolta hello SD</span><span class="sxs-lookup"><span data-stu-id="4ae21-121">Adding SD Elements from hello gallery</span></span>
2. <span data-ttu-id="4ae21-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ae21-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-hello-gallery"></a><span data-ttu-id="4ae21-123">Aggiunta di elementi dalla raccolta hello SD</span><span class="sxs-lookup"><span data-stu-id="4ae21-123">Adding SD Elements from hello gallery</span></span>
<span data-ttu-id="4ae21-124">integrazione hello tooconfigure di elementi SD in Azure AD, è necessario tooadd SD elementi dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4ae21-124">tooconfigure hello integration of SD Elements into Azure AD, you need tooadd SD Elements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4ae21-125">**tooadd SD elementi dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ae21-125">**tooadd SD Elements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ae21-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4ae21-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4ae21-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4ae21-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4ae21-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4ae21-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4ae21-133">Nella casella di ricerca hello, digitare **SD elementi**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-133">In hello search box, type **SD Elements**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="4ae21-135">Nel riquadro dei risultati hello, selezionare **SD elementi**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4ae21-135">In hello results panel, select **SD Elements**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4ae21-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ae21-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4ae21-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SD Elements usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4ae21-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4ae21-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello negli elementi SD è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ae21-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SD Elements is tooa user in Azure AD.</span></span> <span data-ttu-id="4ae21-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello negli elementi SD deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4ae21-140">In other words, a link relationship between an Azure AD user and hello related user in SD Elements needs toobe established.</span></span>

<span data-ttu-id="4ae21-141">Negli elementi SD, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4ae21-141">In SD Elements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4ae21-142">tooconfigure e prova AD Azure single sign-on con elementi SD, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4ae21-142">tooconfigure and test Azure AD single sign-on with SD Elements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4ae21-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4ae21-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4ae21-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ae21-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ae21-145">**[Creazione di un utente test SD elementi](#creating-a-sd-elements-test-user)**  -toohave un equivalente di Britta Simon in elementi SD rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4ae21-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - toohave a counterpart of Britta Simon in SD Elements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4ae21-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4ae21-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4ae21-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4ae21-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4ae21-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ae21-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4ae21-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione elementi SD.</span><span class="sxs-lookup"><span data-stu-id="4ae21-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="4ae21-150">**Azure AD tooconfigure single sign-on con elementi SD, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ae21-150">**tooconfigure Azure AD single sign-on with SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ae21-151">Nel portale di Azure su hello hello **SD elementi** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-151">In hello Azure portal, on hello **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4ae21-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4ae21-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="4ae21-155">In hello **SD elementi dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ae21-155">On hello **SD Elements Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="4ae21-157">a.</span><span class="sxs-lookup"><span data-stu-id="4ae21-157">a.</span></span> <span data-ttu-id="4ae21-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="4ae21-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="4ae21-159">b.</span><span class="sxs-lookup"><span data-stu-id="4ae21-159">b.</span></span> <span data-ttu-id="4ae21-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="4ae21-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4ae21-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4ae21-161">These values are not real.</span></span> <span data-ttu-id="4ae21-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="4ae21-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="4ae21-163">Contatto [team di supporto elementi SD](mailto:support@sdelements.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="4ae21-163">Contact [SD Elements support team](mailto:support@sdelements.com) tooget these values.</span></span>

4. <span data-ttu-id="4ae21-164">Applicazione di elementi SD prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="4ae21-164">SD Elements application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="4ae21-165">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ae21-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="4ae21-166">È possibile gestire i valori hello di questi attributi da hello **"Attributo utente"** scheda dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="4ae21-166">You can manage hello values of these attributes from hello **"User Attribute"** tab of hello application.</span></span> <span data-ttu-id="4ae21-167">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="4ae21-167">hello following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="4ae21-169">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ae21-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span> 

    | <span data-ttu-id="4ae21-170">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="4ae21-170">Attribute Name</span></span> | <span data-ttu-id="4ae21-171">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="4ae21-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="4ae21-172">email</span><span class="sxs-lookup"><span data-stu-id="4ae21-172">email</span></span> |<span data-ttu-id="4ae21-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="4ae21-173">user.mail</span></span> |
    | <span data-ttu-id="4ae21-174">firstname</span><span class="sxs-lookup"><span data-stu-id="4ae21-174">firstname</span></span> |<span data-ttu-id="4ae21-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4ae21-175">user.givenname</span></span> |
    | <span data-ttu-id="4ae21-176">lastname</span><span class="sxs-lookup"><span data-stu-id="4ae21-176">lastname</span></span> |<span data-ttu-id="4ae21-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="4ae21-177">user.surname</span></span> |

    <span data-ttu-id="4ae21-178">a.</span><span class="sxs-lookup"><span data-stu-id="4ae21-178">a.</span></span> <span data-ttu-id="4ae21-179">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4ae21-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="4ae21-182">b.</span><span class="sxs-lookup"><span data-stu-id="4ae21-182">b.</span></span> <span data-ttu-id="4ae21-183">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="4ae21-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="4ae21-184">c.</span><span class="sxs-lookup"><span data-stu-id="4ae21-184">c.</span></span> <span data-ttu-id="4ae21-185">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="4ae21-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="4ae21-186">d.</span><span class="sxs-lookup"><span data-stu-id="4ae21-186">d.</span></span> <span data-ttu-id="4ae21-187">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="4ae21-188">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4ae21-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="4ae21-190">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4ae21-190">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4ae21-192">In hello **SD elementi di configurazione** fare clic su **configurare elementi SD** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="4ae21-192">On hello **SD Elements Configuration** section, click **Configure SD Elements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4ae21-193">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4ae21-193">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="4ae21-195">tooget abilitato single sign-on, contattare il [team di supporto SD elementi](mailto:support@sdelements.com) e fornire loro il file di certificato scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="4ae21-195">tooget single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with hello downloaded certificate file.</span></span> 

10. <span data-ttu-id="4ae21-196">In un'altra finestra del browser tenant SD elementi tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4ae21-196">In a different browser window, sign-on tooyour SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="4ae21-197">Scegliere dal menu hello in primo piano hello **sistema**e quindi **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-197">In hello menu on hello top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="4ae21-199">In hello **Single Sign-On Settings** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ae21-199">On hello **Single Sign-On Settings** dialog, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="4ae21-201">a.</span><span class="sxs-lookup"><span data-stu-id="4ae21-201">a.</span></span> <span data-ttu-id="4ae21-202">Come **SSO Type** selezionare **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="4ae21-203">b.</span><span class="sxs-lookup"><span data-stu-id="4ae21-203">b.</span></span> <span data-ttu-id="4ae21-204">In hello **Identity Provider Entity ID** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae21-204">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="4ae21-205">c.</span><span class="sxs-lookup"><span data-stu-id="4ae21-205">c.</span></span> <span data-ttu-id="4ae21-206">In hello **Identity Provider Single Sign-On Service** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae21-206">In hello **Identity Provider Single Sign-On Service** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="4ae21-207">d.</span><span class="sxs-lookup"><span data-stu-id="4ae21-207">d.</span></span> <span data-ttu-id="4ae21-208">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4ae21-209">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4ae21-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4ae21-210">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4ae21-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4ae21-211">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4ae21-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4ae21-212">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ae21-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="4ae21-213">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4ae21-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4ae21-215">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ae21-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ae21-216">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4ae21-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4ae21-218">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4ae21-220">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4ae21-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4ae21-222">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ae21-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4ae21-224">a.</span><span class="sxs-lookup"><span data-stu-id="4ae21-224">a.</span></span> <span data-ttu-id="4ae21-225">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4ae21-226">b.</span><span class="sxs-lookup"><span data-stu-id="4ae21-226">b.</span></span> <span data-ttu-id="4ae21-227">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4ae21-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4ae21-228">c.</span><span class="sxs-lookup"><span data-stu-id="4ae21-228">c.</span></span> <span data-ttu-id="4ae21-229">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4ae21-230">d.</span><span class="sxs-lookup"><span data-stu-id="4ae21-230">d.</span></span> <span data-ttu-id="4ae21-231">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="4ae21-232">Creazione di un utente test di SD Elements</span><span class="sxs-lookup"><span data-stu-id="4ae21-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="4ae21-233">obiettivo di Hello di questa sezione è un utente denominato Britta Simon negli elementi SD toocreate.</span><span class="sxs-lookup"><span data-stu-id="4ae21-233">hello objective of this section is toocreate a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="4ae21-234">In caso di hello elementi SD, la creazione di utenti SD elementi è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="4ae21-234">In hello case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="4ae21-235">**toocreate Britta Simon negli elementi SD, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ae21-235">**toocreate Britta Simon in SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ae21-236">In una finestra del web browser, sito di società SD elementi tooyour sign-on come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4ae21-236">In a web browser window, sign-on tooyour SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="4ae21-237">Scegliere dal menu hello in primo piano hello **Gestione utenti**e quindi **utenti**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-237">In hello menu on hello top, click **User Management**, and then **Users**.</span></span>
   
    ![Creazione di un utente test di SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="4ae21-239">Fare clic su **Add new user**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-239">Click **Add New User**.</span></span>
   
    ![Creazione di un utente test di SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="4ae21-241">In hello **Add New User** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ae21-241">On hello **Add New User** dialog, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="4ae21-243">a.</span><span class="sxs-lookup"><span data-stu-id="4ae21-243">a.</span></span> <span data-ttu-id="4ae21-244">In hello **posta elettronica** casella di testo immettere hello email dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="4ae21-244">In hello **E-mail** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="4ae21-245">b.</span><span class="sxs-lookup"><span data-stu-id="4ae21-245">b.</span></span> <span data-ttu-id="4ae21-246">In hello **nome** casella di testo, immettere nome hello dell'utente come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-246">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="4ae21-247">c.</span><span class="sxs-lookup"><span data-stu-id="4ae21-247">c.</span></span> <span data-ttu-id="4ae21-248">In hello **cognome** casella di testo immettere hello cognome dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-248">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="4ae21-249">d.</span><span class="sxs-lookup"><span data-stu-id="4ae21-249">d.</span></span> <span data-ttu-id="4ae21-250">Come **Role** (Ruolo) selezionare **User** (Utente).</span><span class="sxs-lookup"><span data-stu-id="4ae21-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="4ae21-251">e.</span><span class="sxs-lookup"><span data-stu-id="4ae21-251">e.</span></span> <span data-ttu-id="4ae21-252">Fare clic su **Create User**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-252">Click **Create User**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4ae21-253">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ae21-253">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4ae21-254">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSD elementi.</span><span class="sxs-lookup"><span data-stu-id="4ae21-254">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSD Elements.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4ae21-256">**tooassign Britta Simon tooSD elementi, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ae21-256">**tooassign Britta Simon tooSD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ae21-257">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-257">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4ae21-259">Nell'elenco di applicazioni hello, selezionare **SD elementi**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-259">In hello applications list, select **SD Elements**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="4ae21-261">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-261">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4ae21-263">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-263">Click **Add** button.</span></span> <span data-ttu-id="4ae21-264">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4ae21-266">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4ae21-266">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4ae21-267">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4ae21-268">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4ae21-269">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4ae21-269">Testing single sign-on</span></span>

<span data-ttu-id="4ae21-270">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4ae21-270">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="4ae21-271">Quando si fa clic hello SD elementi riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione elementi SD.</span><span class="sxs-lookup"><span data-stu-id="4ae21-271">When you click hello SD Elements tile in hello Access Panel, you should get automatically signed-on tooyour SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4ae21-272">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4ae21-272">Additional resources</span></span>

* [<span data-ttu-id="4ae21-273">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ae21-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ae21-274">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ae21-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

