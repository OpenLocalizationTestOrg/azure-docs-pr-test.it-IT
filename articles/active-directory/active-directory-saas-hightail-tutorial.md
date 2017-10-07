---
title: 'Esercitazione: Integrazione di Azure Active Directory con Hightail | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Hightail.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="47a18-103">Esercitazione: Integrazione di Azure Active Directory con Hightail</span><span class="sxs-lookup"><span data-stu-id="47a18-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="47a18-104">In questa esercitazione, è illustrato come toointegrate Hightail con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47a18-104">In this tutorial, you learn how toointegrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47a18-105">Integrazione Hightail con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="47a18-105">Integrating Hightail with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="47a18-106">È possibile controllare in Azure AD che ha accesso tooHightail</span><span class="sxs-lookup"><span data-stu-id="47a18-106">You can control in Azure AD who has access tooHightail</span></span>
- <span data-ttu-id="47a18-107">È possibile abilitare l'utenti tooautomatically get connesso tooHightail (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="47a18-107">You can enable your users tooautomatically get signed-on tooHightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="47a18-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="47a18-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="47a18-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47a18-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47a18-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="47a18-110">Prerequisites</span></span>

<span data-ttu-id="47a18-111">integrazione di Azure AD con Hightail tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="47a18-111">tooconfigure Azure AD integration with Hightail, you need hello following items:</span></span>

- <span data-ttu-id="47a18-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47a18-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47a18-113">Sottoscrizione di Hightail abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="47a18-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="47a18-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="47a18-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47a18-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="47a18-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47a18-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="47a18-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47a18-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47a18-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47a18-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="47a18-118">Scenario description</span></span>
<span data-ttu-id="47a18-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="47a18-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47a18-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="47a18-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47a18-121">Aggiunta di Hightail dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="47a18-121">Adding Hightail from hello gallery</span></span>
2. <span data-ttu-id="47a18-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47a18-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-hello-gallery"></a><span data-ttu-id="47a18-123">Aggiunta di Hightail dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="47a18-123">Adding Hightail from hello gallery</span></span>
<span data-ttu-id="47a18-124">integrazione hello tooconfigure di Hightail in Azure AD, è necessario tooadd Hightail dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="47a18-124">tooconfigure hello integration of Hightail into Azure AD, you need tooadd Hightail from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="47a18-125">**tooadd Hightail dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47a18-125">**tooadd Hightail from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="47a18-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="47a18-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="47a18-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="47a18-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="47a18-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="47a18-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="47a18-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="47a18-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="47a18-133">Nella casella di ricerca hello, digitare **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="47a18-133">In hello search box, type **Hightail**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="47a18-135">Nel riquadro dei risultati hello, selezionare **Hightail**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="47a18-135">In hello results panel, select **Hightail**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="47a18-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47a18-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="47a18-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Hightail mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="47a18-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="47a18-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Hightail è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47a18-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hightail is tooa user in Azure AD.</span></span> <span data-ttu-id="47a18-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Hightail deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="47a18-140">In other words, a link relationship between an Azure AD user and hello related user in Hightail needs toobe established.</span></span>

<span data-ttu-id="47a18-141">In Hightail, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="47a18-141">In Hightail, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="47a18-142">tooconfigure e prova AD Azure single sign-on con Hightail, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="47a18-142">tooconfigure and test Azure AD single sign-on with Hightail, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="47a18-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="47a18-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="47a18-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47a18-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47a18-145">**[Creazione di un utente test Hightail](#creating-a-hightail-test-user)**  -toohave un equivalente di Britta Simon in Hightail che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="47a18-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - toohave a counterpart of Britta Simon in Hightail that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="47a18-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="47a18-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47a18-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="47a18-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="47a18-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47a18-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="47a18-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Hightail.</span><span class="sxs-lookup"><span data-stu-id="47a18-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="47a18-150">**Azure AD tooconfigure single sign-on con Hightail, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47a18-150">**tooconfigure Azure AD single sign-on with Hightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="47a18-151">Nel portale di Azure su hello hello **Hightail** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="47a18-151">In hello Azure portal, on hello **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="47a18-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="47a18-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="47a18-155">In hello **Hightail dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47a18-155">On hello **Hightail Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="47a18-157">In hello **URL di risposta** casella di testo, digitare l'URL hello come:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="47a18-157">In hello **Reply URL** textbox, type hello URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="47a18-158">Hello valore precedente non è il valore reale.</span><span class="sxs-lookup"><span data-stu-id="47a18-158">hello preceding value is not real value.</span></span> <span data-ttu-id="47a18-159">È possibile aggiornare il valore di hello con URL risposta effettivo hello illustrato più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="47a18-159">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="47a18-160">In hello **Hightail dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47a18-160">On hello **Hightail Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="47a18-162">a.</span><span class="sxs-lookup"><span data-stu-id="47a18-162">a.</span></span> <span data-ttu-id="47a18-163">Fare clic su hello **Mostra URL impostazioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="47a18-163">Click hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="47a18-164">b.</span><span class="sxs-lookup"><span data-stu-id="47a18-164">b.</span></span> <span data-ttu-id="47a18-165">In hello **URL di accesso** casella di testo, digitare l'URL hello come:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="47a18-165">In hello **Sign On URL** textbox, type hello URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="47a18-166">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="47a18-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="47a18-168">Hightail asserzioni SAML hello prevista dall'applicazione in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="47a18-168">Hightail application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="47a18-169">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="47a18-169">Please configure hello following claims for this application.</span></span> <span data-ttu-id="47a18-170">È possibile gestire i valori hello di questi attributi da hello **"Atrribute"** scheda dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="47a18-170">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="47a18-171">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="47a18-171">hello following screenshot shows an example for this.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="47a18-173">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47a18-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="47a18-174">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="47a18-174">Attribute Name</span></span> | <span data-ttu-id="47a18-175">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="47a18-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="47a18-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="47a18-176">FirstName</span></span> | <span data-ttu-id="47a18-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="47a18-177">user.givenname</span></span> |
    | <span data-ttu-id="47a18-178">LastName</span><span class="sxs-lookup"><span data-stu-id="47a18-178">LastName</span></span> | <span data-ttu-id="47a18-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="47a18-179">user.surname</span></span> |
    | <span data-ttu-id="47a18-180">Email</span><span class="sxs-lookup"><span data-stu-id="47a18-180">Email</span></span> | <span data-ttu-id="47a18-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="47a18-181">user.mail</span></span> |    
    | <span data-ttu-id="47a18-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="47a18-182">UserIdentity</span></span> | <span data-ttu-id="47a18-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="47a18-183">user.mail</span></span> |
    
    <span data-ttu-id="47a18-184">a.</span><span class="sxs-lookup"><span data-stu-id="47a18-184">a.</span></span> <span data-ttu-id="47a18-185">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="47a18-185">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="47a18-188">b.</span><span class="sxs-lookup"><span data-stu-id="47a18-188">b.</span></span> <span data-ttu-id="47a18-189">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="47a18-189">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="47a18-190">c.</span><span class="sxs-lookup"><span data-stu-id="47a18-190">c.</span></span> <span data-ttu-id="47a18-191">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="47a18-191">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="47a18-192">d.</span><span class="sxs-lookup"><span data-stu-id="47a18-192">d.</span></span> <span data-ttu-id="47a18-193">Lasciare hello **Namespace** vuoto.</span><span class="sxs-lookup"><span data-stu-id="47a18-193">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="47a18-194">e.</span><span class="sxs-lookup"><span data-stu-id="47a18-194">e.</span></span> <span data-ttu-id="47a18-195">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="47a18-195">Click **Ok**.</span></span>

7. <span data-ttu-id="47a18-196">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="47a18-196">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="47a18-198">In hello **Hightail configurazione** fare clic su **configurare Hightail** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="47a18-198">On hello **Hightail Configuration** section, click **Configure Hightail** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="47a18-199">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="47a18-199">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="47a18-201">Prima di configurare hello Single Sign-On in app Hightail, elenco approvato il dominio di posta elettronica con Hightail team in modo che tutti gli utenti che utilizzano questo dominio di hello possono utilizzare funzionalità Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="47a18-201">Before configuring hello Single Sign On at Hightail app, please white list your email domain with Hightail team so that all hello users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="47a18-202">tooget SSO configurato per l'applicazione, è necessario toosign-on tooyour Hightail tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="47a18-202">tooget SSO configured for your application, you need toosign-on tooyour Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="47a18-203">a.</span><span class="sxs-lookup"><span data-stu-id="47a18-203">a.</span></span> <span data-ttu-id="47a18-204">Scegliere hello hello menu in alto hello **Account** e selezionare **configurare SAML**.</span><span class="sxs-lookup"><span data-stu-id="47a18-204">In hello menu on hello top, click hello **Account** tab and select **Configure SAML**.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="47a18-206">b.</span><span class="sxs-lookup"><span data-stu-id="47a18-206">b.</span></span> <span data-ttu-id="47a18-207">Selezionare una casella di controllo hello **Abilita autenticazione SAML**.</span><span class="sxs-lookup"><span data-stu-id="47a18-207">Select hello checkbox of **Enable SAML Authentication**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="47a18-209">c.</span><span class="sxs-lookup"><span data-stu-id="47a18-209">c.</span></span> <span data-ttu-id="47a18-210">Aprire il certificato con codifica base 64 nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato di firma di Token SAML** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="47a18-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **SAML Token Signing Certificate** textbox.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="47a18-212">d.</span><span class="sxs-lookup"><span data-stu-id="47a18-212">d.</span></span> <span data-ttu-id="47a18-213">In hello **autorità SAML (Provider di identità)** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** copiata dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="47a18-213">In hello **SAML Authority (Identity Provider)** textbox, paste hello value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="47a18-215">e.</span><span class="sxs-lookup"><span data-stu-id="47a18-215">e.</span></span> <span data-ttu-id="47a18-216">Se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP** selezionare **"Provider di identità (IdP) avviato Accedi"**.</span><span class="sxs-lookup"><span data-stu-id="47a18-216">If you wish tooconfigure hello application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="47a18-217">Se si usa la **modalità avviata da SP**, selezionare **"Service Provider (SP) initiated log in"** ("Accesso avviato con provider di servizi (SP)").</span><span class="sxs-lookup"><span data-stu-id="47a18-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="47a18-219">f.</span><span class="sxs-lookup"><span data-stu-id="47a18-219">f.</span></span> <span data-ttu-id="47a18-220">Copiare l'URL di consumer hello SAML per l'istanza e incollarlo in **URL di risposta** nella casella di testo **Hightail dominio e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="47a18-220">Copy hello SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="47a18-221">g.</span><span class="sxs-lookup"><span data-stu-id="47a18-221">g.</span></span> <span data-ttu-id="47a18-222">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="47a18-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="47a18-223">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="47a18-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="47a18-224">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="47a18-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="47a18-225">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="47a18-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="47a18-226">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47a18-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="47a18-227">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="47a18-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="47a18-229">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47a18-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="47a18-230">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="47a18-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="47a18-232">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="47a18-232">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="47a18-234">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="47a18-234">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="47a18-236">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47a18-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="47a18-238">a.</span><span class="sxs-lookup"><span data-stu-id="47a18-238">a.</span></span> <span data-ttu-id="47a18-239">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="47a18-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="47a18-240">b.</span><span class="sxs-lookup"><span data-stu-id="47a18-240">b.</span></span> <span data-ttu-id="47a18-241">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="47a18-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="47a18-242">c.</span><span class="sxs-lookup"><span data-stu-id="47a18-242">c.</span></span> <span data-ttu-id="47a18-243">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="47a18-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="47a18-244">d.</span><span class="sxs-lookup"><span data-stu-id="47a18-244">d.</span></span> <span data-ttu-id="47a18-245">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="47a18-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="47a18-246">Creazione di un utente test di Hightail</span><span class="sxs-lookup"><span data-stu-id="47a18-246">Creating a Hightail test user</span></span>

<span data-ttu-id="47a18-247">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Hightail toocreate.</span><span class="sxs-lookup"><span data-stu-id="47a18-247">hello objective of this section is toocreate a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="47a18-248">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="47a18-248">There is no action item for you in this section.</span></span> <span data-ttu-id="47a18-249">Hightail supporta il provisioning utenti just-in-time in base alle attestazioni personalizzate hello.</span><span class="sxs-lookup"><span data-stu-id="47a18-249">Hightail supports just-in-time user provisioning based on hello custom claims.</span></span> <span data-ttu-id="47a18-250">Se sono state configurate le attestazioni personalizzate hello, come illustrato nella sezione hello  **[configurazione Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  sopra, viene automaticamente creato un utente in un'applicazione hello non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="47a18-250">If you have configured hello custom claims as shown in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in hello application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="47a18-251">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto Hightail](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="47a18-251">If you need toocreate a user manually, you need toocontact hello [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="47a18-252">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="47a18-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="47a18-253">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHightail.</span><span class="sxs-lookup"><span data-stu-id="47a18-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHightail.</span></span>

![Assegna utente][200] 

<span data-ttu-id="47a18-255">**tooassign Britta Simon tooHightail, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47a18-255">**tooassign Britta Simon tooHightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="47a18-256">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="47a18-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="47a18-258">Nell'elenco di applicazioni hello, selezionare **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="47a18-258">In hello applications list, select **Hightail**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="47a18-260">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="47a18-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="47a18-262">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="47a18-262">Click **Add** button.</span></span> <span data-ttu-id="47a18-263">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="47a18-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="47a18-265">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="47a18-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="47a18-266">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="47a18-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47a18-267">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="47a18-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="47a18-268">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="47a18-268">Testing single sign-on</span></span>

<span data-ttu-id="47a18-269">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="47a18-269">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="47a18-270">Quando si fa clic su riquadro Hightail hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Hightail applicazione.</span><span class="sxs-lookup"><span data-stu-id="47a18-270">When you click hello Hightail tile in hello Access Panel, you should get automatically signed-on tooyour Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="47a18-271">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="47a18-271">Additional resources</span></span>

* [<span data-ttu-id="47a18-272">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47a18-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47a18-273">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47a18-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

