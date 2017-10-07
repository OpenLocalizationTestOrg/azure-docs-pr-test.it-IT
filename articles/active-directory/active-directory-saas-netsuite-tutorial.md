---
title: 'Esercitazione: Integrazione di Azure Active Directory con NetSuite | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="d57e2-103">Esercitazione: Integrazione di Azure Active Directory con NetSuite</span><span class="sxs-lookup"><span data-stu-id="d57e2-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="d57e2-104">In questa esercitazione, è illustrato come toointegrate Netsuite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d57e2-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d57e2-105">Integrazione Netsuite con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d57e2-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d57e2-106">È possibile controllare in Azure AD che ha accesso tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="d57e2-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="d57e2-107">È possibile abilitare l'utenti tooautomatically get connesso tooNetsuite (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d57e2-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d57e2-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d57e2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d57e2-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d57e2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d57e2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d57e2-110">Prerequisites</span></span>

<span data-ttu-id="d57e2-111">integrazione di Azure AD con Netsuite tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d57e2-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="d57e2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d57e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d57e2-113">Sottoscrizione di Netsuite abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d57e2-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d57e2-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d57e2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d57e2-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d57e2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d57e2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d57e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d57e2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d57e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d57e2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d57e2-118">Scenario description</span></span>
<span data-ttu-id="d57e2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d57e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d57e2-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d57e2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d57e2-121">Aggiunta di Netsuite dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d57e2-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="d57e2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d57e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="d57e2-123">Aggiunta di Netsuite dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d57e2-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="d57e2-124">integrazione hello tooconfigure di Netsuite in Azure AD, è necessario tooadd Netsuite dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d57e2-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d57e2-125">**tooadd Netsuite dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d57e2-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d57e2-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d57e2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d57e2-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d57e2-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d57e2-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d57e2-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d57e2-133">Nella casella di ricerca hello, digitare **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-133">In hello search box, type **Netsuite**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="d57e2-135">Nel riquadro dei risultati hello, selezionare **Netsuite**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d57e2-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d57e2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d57e2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d57e2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Netsuite in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d57e2-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d57e2-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Netsuite è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d57e2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="d57e2-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Netsuite richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="d57e2-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="d57e2-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="d57e2-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="d57e2-142">tooconfigure e prova AD Azure single sign-on con Netsuite, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d57e2-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d57e2-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d57e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d57e2-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d57e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d57e2-145">**[Creazione di un utente test Netsuite](#creating-a-netsuite-test-user)**  -toohave un equivalente di Britta Simon in Netsuite che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d57e2-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d57e2-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d57e2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d57e2-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d57e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d57e2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d57e2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d57e2-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Netsuite.</span><span class="sxs-lookup"><span data-stu-id="d57e2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="d57e2-150">**Azure AD tooconfigure single sign-on con Netsuite, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d57e2-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="d57e2-151">Nel portale di Azure su hello hello **Netsuite** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d57e2-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d57e2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="d57e2-155">In hello **Netsuite dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d57e2-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="d57e2-157">In hello **URL di risposta** casella di testo, digitare un URL con modello di hello: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="d57e2-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d57e2-158">Poiché il valore non è reale,</span><span class="sxs-lookup"><span data-stu-id="d57e2-158">This value is not real value.</span></span> <span data-ttu-id="d57e2-159">Il valore di hello aggiornamento con hello URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="d57e2-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="d57e2-160">Contatto [team di supporto Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="d57e2-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="d57e2-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d57e2-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="d57e2-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d57e2-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d57e2-165">In hello **Netsuite configurazione** fare clic su **configurare Netsuite** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="d57e2-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d57e2-166">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d57e2-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="d57e2-168">Aprire una nuova scheda nel browser e accedere al sito della società Netsuite come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d57e2-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="d57e2-169">Nella barra degli strumenti di hello nella parte superiore di hello di hello pagina, fare clic su **installazione**, quindi fare clic su **Setup Manager**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="d57e2-171">Da hello **le attività di configurazione** elenco, selezionare **integrazione**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="d57e2-173">In hello **Manage Authentication** fare clic su **SAML Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="d57e2-175">In hello **SAML Setup** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d57e2-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="d57e2-176">a.</span><span class="sxs-lookup"><span data-stu-id="d57e2-176">a.</span></span> <span data-ttu-id="d57e2-177">Hello copia **SAML Single Sign-On Service URL** valore **riferimento rapido** sezione **Configura sign-on** e incollarlo in hello **Provider di identità Pagina di accesso** campo Netsuite.</span><span class="sxs-lookup"><span data-stu-id="d57e2-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="d57e2-179">b.</span><span class="sxs-lookup"><span data-stu-id="d57e2-179">b.</span></span> <span data-ttu-id="d57e2-180">In NetSuite selezionare **Primary Authentication Method** (Metodo di autenticazione primario).</span><span class="sxs-lookup"><span data-stu-id="d57e2-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="d57e2-181">c.</span><span class="sxs-lookup"><span data-stu-id="d57e2-181">c.</span></span> <span data-ttu-id="d57e2-182">Per il campo hello etichettata **SAMLV2 Identity Provider Metadata**selezionare **caricare File di metadati IDP**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="d57e2-183">Quindi fare clic su **Sfoglia** file di metadati hello tooupload scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d57e2-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="d57e2-185">d.</span><span class="sxs-lookup"><span data-stu-id="d57e2-185">d.</span></span> <span data-ttu-id="d57e2-186">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-186">Click **Submit**.</span></span>

12. <span data-ttu-id="d57e2-187">In Azure AD fare clic sulla casella di controllo **Visualizza e modifica tutti gli altri attributi utente** e aggiungere l'attributo.</span><span class="sxs-lookup"><span data-stu-id="d57e2-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="d57e2-189">Per hello **nome dell'attributo** digitare `account`.</span><span class="sxs-lookup"><span data-stu-id="d57e2-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="d57e2-190">Per hello **valore dell'attributo** , digitare l'ID di account Netsuite. Questo valore è costante e modifica con l'account.</span><span class="sxs-lookup"><span data-stu-id="d57e2-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="d57e2-191">Istruzioni su come toofind l'ID account sono incluse di seguito:</span><span class="sxs-lookup"><span data-stu-id="d57e2-191">Instructions on how toofind your account ID are included below:</span></span>

      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="d57e2-193">a.</span><span class="sxs-lookup"><span data-stu-id="d57e2-193">a.</span></span> <span data-ttu-id="d57e2-194">In Netsuite, fare clic su **installazione** dal menu di navigazione superiore hello.</span><span class="sxs-lookup"><span data-stu-id="d57e2-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="d57e2-195">b.</span><span class="sxs-lookup"><span data-stu-id="d57e2-195">b.</span></span> <span data-ttu-id="d57e2-196">Fare clic in hello **le attività di configurazione** sezione del menu di navigazione sinistro hello, seleziona hello **integrazione** sezione e fare clic su **preferenze di servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="d57e2-197">c.</span><span class="sxs-lookup"><span data-stu-id="d57e2-197">c.</span></span> <span data-ttu-id="d57e2-198">Copiare l'ID Account Netsuite e incollarlo in hello **valore dell'attributo** campo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d57e2-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="d57e2-200">Prima che gli utenti possono eseguire single sign-on in Netsuite, si devono prima essere assegnate autorizzazioni appropriate di hello in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="d57e2-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="d57e2-201">Seguire le istruzioni di hello sotto tooassign queste autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="d57e2-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="d57e2-202">a.</span><span class="sxs-lookup"><span data-stu-id="d57e2-202">a.</span></span> <span data-ttu-id="d57e2-203">Scegliere dal menu di spostamento superiore di hello **installazione**, quindi fare clic su **Setup Manager**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="d57e2-205">b.</span><span class="sxs-lookup"><span data-stu-id="d57e2-205">b.</span></span> <span data-ttu-id="d57e2-206">Scegliere dal menu di navigazione a sinistra di hello **Users/Roles**, quindi fare clic su **gestione ruoli**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="d57e2-208">c.</span><span class="sxs-lookup"><span data-stu-id="d57e2-208">c.</span></span> <span data-ttu-id="d57e2-209">Fare clic su **New Role**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-209">Click **New Role**.</span></span>

    <span data-ttu-id="d57e2-210">d.</span><span class="sxs-lookup"><span data-stu-id="d57e2-210">d.</span></span> <span data-ttu-id="d57e2-211">Digitare un **nome** per il nuovo ruolo e seleziona hello **Single Sign-On solo** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="d57e2-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="d57e2-213">e.</span><span class="sxs-lookup"><span data-stu-id="d57e2-213">e.</span></span> <span data-ttu-id="d57e2-214">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-214">Click **Save**.</span></span>

    <span data-ttu-id="d57e2-215">f.</span><span class="sxs-lookup"><span data-stu-id="d57e2-215">f.</span></span> <span data-ttu-id="d57e2-216">Scegliere dal menu hello in primo piano hello **autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="d57e2-217">Fare quindi clic su **Setup**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-217">Then click **Setup**.</span></span>
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="d57e2-219">g.</span><span class="sxs-lookup"><span data-stu-id="d57e2-219">g.</span></span> <span data-ttu-id="d57e2-220">Selezionare **Set Up SAM Single Sign-on** (Configura Single Sign-on SAM), quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="d57e2-221">h.</span><span class="sxs-lookup"><span data-stu-id="d57e2-221">h.</span></span> <span data-ttu-id="d57e2-222">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-222">Click **Save**.</span></span>

    <span data-ttu-id="d57e2-223">i.</span><span class="sxs-lookup"><span data-stu-id="d57e2-223">i.</span></span> <span data-ttu-id="d57e2-224">Scegliere dal menu di spostamento superiore di hello **installazione**, quindi fare clic su **Setup Manager**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="d57e2-226">j.</span><span class="sxs-lookup"><span data-stu-id="d57e2-226">j.</span></span> <span data-ttu-id="d57e2-227">Scegliere dal menu di navigazione a sinistra di hello **Users/Roles**, quindi fare clic su **Gestisci utenti**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="d57e2-229">k.</span><span class="sxs-lookup"><span data-stu-id="d57e2-229">k.</span></span> <span data-ttu-id="d57e2-230">Selezionare un utente di test.</span><span class="sxs-lookup"><span data-stu-id="d57e2-230">Select a test user.</span></span> <span data-ttu-id="d57e2-231">Fare quindi clic su **Edit**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-231">Then click **Edit**.</span></span>
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="d57e2-233">l.</span><span class="sxs-lookup"><span data-stu-id="d57e2-233">l.</span></span> <span data-ttu-id="d57e2-234">Nella finestra di dialogo ruoli hello, selezionare il ruolo hello che è stato creato e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="d57e2-236">m.</span><span class="sxs-lookup"><span data-stu-id="d57e2-236">m.</span></span> <span data-ttu-id="d57e2-237">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="d57e2-238">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="d57e2-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d57e2-239">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d57e2-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d57e2-240">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d57e2-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d57e2-241">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d57e2-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="d57e2-242">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d57e2-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d57e2-244">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d57e2-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d57e2-245">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d57e2-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="d57e2-247">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d57e2-249">Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d57e2-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d57e2-251">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d57e2-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d57e2-253">a.</span><span class="sxs-lookup"><span data-stu-id="d57e2-253">a.</span></span> <span data-ttu-id="d57e2-254">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d57e2-255">b.</span><span class="sxs-lookup"><span data-stu-id="d57e2-255">b.</span></span> <span data-ttu-id="d57e2-256">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d57e2-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d57e2-257">c.</span><span class="sxs-lookup"><span data-stu-id="d57e2-257">c.</span></span> <span data-ttu-id="d57e2-258">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d57e2-259">d.</span><span class="sxs-lookup"><span data-stu-id="d57e2-259">d.</span></span> <span data-ttu-id="d57e2-260">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="d57e2-261">Creazione di un utente test di Netsuite</span><span class="sxs-lookup"><span data-stu-id="d57e2-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="d57e2-262">In questa sezione si crea un utente di nome Britta Simon in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="d57e2-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="d57e2-263">Netsuite supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d57e2-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="d57e2-264">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d57e2-264">There is no action item for you in this section.</span></span> <span data-ttu-id="d57e2-265">Se un utente non esiste già in Netsuite, quando si tenta di tooaccess Netsuite uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="d57e2-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d57e2-266">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d57e2-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d57e2-267">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="d57e2-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d57e2-269">**tooassign Britta Simon tooNetsuite, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d57e2-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="d57e2-270">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d57e2-272">Nell'elenco di applicazioni hello, selezionare **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-272">In hello applications list, select **Netsuite**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="d57e2-274">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d57e2-276">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-276">Click **Add** button.</span></span> <span data-ttu-id="d57e2-277">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d57e2-279">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d57e2-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d57e2-280">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d57e2-281">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d57e2-282">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d57e2-282">Testing single sign-on</span></span>

<span data-ttu-id="d57e2-283">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d57e2-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d57e2-284">tootest le impostazioni single sign-on, aprire il pannello di accesso a hello [https://myapps.microsoft.com](https://myapps.microsoft.com/), accedere all'account di prova hello e fare clic su **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="d57e2-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d57e2-285">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d57e2-285">Additional resources</span></span>

* [<span data-ttu-id="d57e2-286">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d57e2-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d57e2-287">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d57e2-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d57e2-288">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="d57e2-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

