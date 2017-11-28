---
title: 'Esercitazione: Integrazione di Azure Active Directory con Trello | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Trello.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="6c8a0-103">Esercitazione: Integrazione di Azure Active Directory con Trello</span><span class="sxs-lookup"><span data-stu-id="6c8a0-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="6c8a0-104">In questa esercitazione, è illustrato come toointegrate Trello con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6c8a0-104">In this tutorial, you learn how toointegrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c8a0-105">Integrazione Trello con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="6c8a0-105">Integrating Trello with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6c8a0-106">È possibile controllare in Azure AD che ha accesso tooTrello</span><span class="sxs-lookup"><span data-stu-id="6c8a0-106">You can control in Azure AD who has access tooTrello</span></span>
- <span data-ttu-id="6c8a0-107">È possibile abilitare l'utenti tooautomatically get connesso tooTrello (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c8a0-107">You can enable your users tooautomatically get signed-on tooTrello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6c8a0-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6c8a0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6c8a0-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6c8a0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c8a0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6c8a0-110">Prerequisites</span></span>

<span data-ttu-id="6c8a0-111">integrazione di Azure AD con Trello tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6c8a0-111">tooconfigure Azure AD integration with Trello, you need hello following items:</span></span>

- <span data-ttu-id="6c8a0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c8a0-113">Sottoscrizione di Trello abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6c8a0-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c8a0-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c8a0-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="6c8a0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c8a0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6c8a0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c8a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c8a0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6c8a0-118">Scenario description</span></span>
<span data-ttu-id="6c8a0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c8a0-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="6c8a0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c8a0-121">Aggiunta di Trello dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6c8a0-121">Adding Trello from hello gallery</span></span>
2. <span data-ttu-id="6c8a0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c8a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-hello-gallery"></a><span data-ttu-id="6c8a0-123">Aggiunta di Trello dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6c8a0-123">Adding Trello from hello gallery</span></span>
<span data-ttu-id="6c8a0-124">integrazione hello tooconfigure di Trello in Azure AD, è necessario tooadd Trello dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-124">tooconfigure hello integration of Trello into Azure AD, you need tooadd Trello from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6c8a0-125">**tooadd Trello dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6c8a0-125">**tooadd Trello from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c8a0-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6c8a0-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6c8a0-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6c8a0-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6c8a0-133">Nella casella di ricerca hello, digitare **Trello**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-133">In hello search box, type **Trello**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="6c8a0-135">Nel riquadro dei risultati hello, selezionare **Trello**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-135">In hello results panel, select **Trello**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6c8a0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c8a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6c8a0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Trello in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6c8a0-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c8a0-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Trello è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trello is tooa user in Azure AD.</span></span> <span data-ttu-id="6c8a0-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Trello deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-140">In other words, a link relationship between an Azure AD user and hello related user in Trello needs toobe established.</span></span>

<span data-ttu-id="6c8a0-141">In Trello, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-141">In Trello, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6c8a0-142">tooconfigure e prova AD Azure single sign-on con Trello, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="6c8a0-142">tooconfigure and test Azure AD single sign-on with Trello, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6c8a0-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6c8a0-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c8a0-145">**[Creazione di un utente test Trello](#creating-a-trello-test-user)**  -toohave un equivalente di Britta Simon in Trello che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - toohave a counterpart of Britta Simon in Trello that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6c8a0-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c8a0-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6c8a0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c8a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6c8a0-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Trello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="6c8a0-150">**Azure AD tooconfigure single sign-on con Trello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6c8a0-150">**tooconfigure Azure AD single sign-on with Trello, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c8a0-151">Nel portale di Azure su hello hello **Trello** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-151">In hello Azure portal, on hello **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6c8a0-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="6c8a0-155">In hello **Trello dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6c8a0-155">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="6c8a0-157">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="6c8a0-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="6c8a0-158">In hello **Trello dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6c8a0-158">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="6c8a0-160">a.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-160">a.</span></span> <span data-ttu-id="6c8a0-161">Fare clic su hello **Mostra URL impostazioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-161">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="6c8a0-162">b.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-162">b.</span></span> <span data-ttu-id="6c8a0-163">In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="6c8a0-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="6c8a0-164">È necessario ottenere hello  **\<enterprise\>**  slug da Trello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-164">You should get hello **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="6c8a0-165">Se non si dispone di valore dell'intestazione slug hello, contattare [team di supporto Trello](mailto:support@trello.com) slug hello tooget per si enterprise.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-165">If you don't have hello slug value, contact [Trello support team](mailto:support@trello.com) tooget hello slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="6c8a0-166">Attributi specifici toocontain asserzioni SAML hello prevista dall'applicazione di Trello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-166">Trello application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="6c8a0-167">Configurare gli attributi per questa applicazione seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="6c8a0-168">È possibile gestire i valori hello di questi attributi da hello **"Attributi utente"** di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-168">You can manage hello values of these attributes from hello **"User Attributes"** of hello application.</span></span> <span data-ttu-id="6c8a0-169">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-169">hello following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="6c8a0-171">In hello **attributi token SAML** finestra di dialogo, per ogni riga nella tabella hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6c8a0-171">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
    | <span data-ttu-id="6c8a0-172">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="6c8a0-172">Attribute Name</span></span> | <span data-ttu-id="6c8a0-173">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="6c8a0-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="6c8a0-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="6c8a0-174">User.Email</span></span> | <span data-ttu-id="6c8a0-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="6c8a0-175">user.mail</span></span> |
    | <span data-ttu-id="6c8a0-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="6c8a0-176">User.FirstName</span></span> | <span data-ttu-id="6c8a0-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="6c8a0-177">user.givenname</span></span> |
    | <span data-ttu-id="6c8a0-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="6c8a0-178">User.LastName</span></span> | <span data-ttu-id="6c8a0-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="6c8a0-179">user.surname</span></span> |

    <span data-ttu-id="6c8a0-180">a.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-180">a.</span></span> <span data-ttu-id="6c8a0-181">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="6c8a0-184">b.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-184">b.</span></span> <span data-ttu-id="6c8a0-185">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

    <span data-ttu-id="6c8a0-186">c.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-186">c.</span></span> <span data-ttu-id="6c8a0-187">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6c8a0-188">d.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-188">d.</span></span> <span data-ttu-id="6c8a0-189">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="6c8a0-190">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-190">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="6c8a0-192">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6c8a0-192">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6c8a0-194">In hello **Trello configurazione** fare clic su **configurare Trello** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-194">On hello **Trello Configuration** section, click **Configure Trello** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6c8a0-195">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="6c8a0-195">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="6c8a0-197">tooget SSO configurato per l'applicazione, andare troppo[configurazione di SSO enterprise Trello](https://trello.com/sso-configuration) pagina toosend [team di supporto Trello](mailto:support@trello.com) hello **SAML Single Sign-On Service URL** e collegare hello **certificato (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-197">tooget SSO configured for your application, go too[Trello enterprise SSO configuration](https://trello.com/sso-configuration) page toosend [Trello support team](mailto:support@trello.com) hello **SAML Single Sign-On Service URL** and attach hello **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="6c8a0-198">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="6c8a0-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6c8a0-199">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6c8a0-200">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6c8a0-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6c8a0-201">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c8a0-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="6c8a0-202">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6c8a0-204">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6c8a0-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c8a0-205">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6c8a0-207">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6c8a0-209">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6c8a0-211">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6c8a0-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6c8a0-213">a.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-213">a.</span></span> <span data-ttu-id="6c8a0-214">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c8a0-215">b.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-215">b.</span></span> <span data-ttu-id="6c8a0-216">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6c8a0-217">c.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-217">c.</span></span> <span data-ttu-id="6c8a0-218">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6c8a0-219">d.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-219">d.</span></span> <span data-ttu-id="6c8a0-220">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="6c8a0-221">Creazione di un utente test di Trello</span><span class="sxs-lookup"><span data-stu-id="6c8a0-221">Creating a Trello test user</span></span>

<span data-ttu-id="6c8a0-222">In questa sezione viene creato un utente di nome Britta Simon in Trello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="6c8a0-223">In questa sezione viene creato un utente di nome Britta Simon in Trello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="6c8a0-224">Trello supporta il provisioning di just-in-time e creato un nuovo account è hello prima volta che si accede da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-224">Trello supports just-in-time provisioning and a new account is created hello first time you sign in from Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6c8a0-225">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c8a0-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6c8a0-226">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTrello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrello.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6c8a0-228">**tooassign Britta Simon tooTrello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6c8a0-228">**tooassign Britta Simon tooTrello, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c8a0-229">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6c8a0-231">Nell'elenco di applicazioni hello, selezionare **Trello**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-231">In hello applications list, select **Trello**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="6c8a0-233">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6c8a0-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-235">Click **Add** button.</span></span> <span data-ttu-id="6c8a0-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6c8a0-238">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6c8a0-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c8a0-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6c8a0-241">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6c8a0-241">Testing single sign-on</span></span>

<span data-ttu-id="6c8a0-242">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="6c8a0-243">Quando si fa clic su riquadro Trello hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Trello applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c8a0-243">When you click hello Trello tile in hello Access Panel, you should get automatically signed-on tooyour Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6c8a0-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6c8a0-244">Additional resources</span></span>

* [<span data-ttu-id="6c8a0-245">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c8a0-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c8a0-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c8a0-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

