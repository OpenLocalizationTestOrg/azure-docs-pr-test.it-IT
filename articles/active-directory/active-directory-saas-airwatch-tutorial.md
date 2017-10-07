---
title: 'Esercitazione: Integrazione di Azure Active Directory con AirWatch | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e AirWatch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="f385a-103">Esercitazione: Integrazione di Azure Active Directory con AirWatch</span><span class="sxs-lookup"><span data-stu-id="f385a-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="f385a-104">In questa esercitazione, è illustrato come toointegrate AirWatch con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f385a-104">In this tutorial, you learn how toointegrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f385a-105">Integrazione di AirWatch con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f385a-105">Integrating AirWatch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f385a-106">È possibile controllare in Azure AD che ha accesso tooAirWatch</span><span class="sxs-lookup"><span data-stu-id="f385a-106">You can control in Azure AD who has access tooAirWatch</span></span>
- <span data-ttu-id="f385a-107">È possibile abilitare l'utenti tooautomatically get connesso tooAirWatch (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f385a-107">You can enable your users tooautomatically get signed-on tooAirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f385a-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f385a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f385a-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f385a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f385a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f385a-110">Prerequisites</span></span>

<span data-ttu-id="f385a-111">integrazione di Azure AD con AirWatch tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f385a-111">tooconfigure Azure AD integration with AirWatch, you need hello following items:</span></span>

- <span data-ttu-id="f385a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f385a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f385a-113">Sottoscrizione di AirWatch abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f385a-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f385a-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f385a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f385a-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f385a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f385a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f385a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f385a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f385a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f385a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f385a-118">Scenario description</span></span>
<span data-ttu-id="f385a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f385a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f385a-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f385a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f385a-121">Aggiunta di AirWatch dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f385a-121">Adding AirWatch from hello gallery</span></span>
2. <span data-ttu-id="f385a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f385a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-hello-gallery"></a><span data-ttu-id="f385a-123">Aggiunta di AirWatch dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f385a-123">Adding AirWatch from hello gallery</span></span>
<span data-ttu-id="f385a-124">integrazione hello tooconfigure di AirWatch in Azure AD, è necessario tooadd AirWatch dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f385a-124">tooconfigure hello integration of AirWatch into Azure AD, you need tooadd AirWatch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f385a-125">**tooadd AirWatch dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f385a-125">**tooadd AirWatch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f385a-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f385a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f385a-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f385a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f385a-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f385a-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f385a-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f385a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f385a-133">Nella casella di ricerca hello, digitare **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="f385a-133">In hello search box, type **AirWatch**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="f385a-135">Nel riquadro dei risultati hello, selezionare **AirWatch**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f385a-135">In hello results panel, select **AirWatch**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f385a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f385a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f385a-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con AirWatch con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f385a-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f385a-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in AirWatch è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f385a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AirWatch is tooa user in Azure AD.</span></span> <span data-ttu-id="f385a-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in AirWatch deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f385a-140">In other words, a link relationship between an Azure AD user and hello related user in AirWatch needs toobe established.</span></span>

<span data-ttu-id="f385a-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in AirWatch.</span><span class="sxs-lookup"><span data-stu-id="f385a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in AirWatch.</span></span>

<span data-ttu-id="f385a-142">tooconfigure e prova AD Azure single sign-on con AirWatch, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f385a-142">tooconfigure and test Azure AD single sign-on with AirWatch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f385a-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f385a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f385a-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f385a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f385a-145">**[Creazione di un utente test AirWatch](#creating-a-airwatch-test-user)**  -toohave un equivalente di Britta Simon in AirWatch che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f385a-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - toohave a counterpart of Britta Simon in AirWatch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f385a-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f385a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f385a-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f385a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f385a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f385a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f385a-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione AirWatch.</span><span class="sxs-lookup"><span data-stu-id="f385a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="f385a-150">**Azure AD tooconfigure single sign-on con AirWatch, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f385a-150">**tooconfigure Azure AD single sign-on with AirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="f385a-151">Nel portale di Azure su hello hello **AirWatch** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f385a-151">In hello Azure portal, on hello **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f385a-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f385a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="f385a-155">In hello **AirWatch dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f385a-155">On hello **AirWatch Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="f385a-157">a.</span><span class="sxs-lookup"><span data-stu-id="f385a-157">a.</span></span> <span data-ttu-id="f385a-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="f385a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="f385a-159">b.</span><span class="sxs-lookup"><span data-stu-id="f385a-159">b.</span></span> <span data-ttu-id="f385a-160">In hello **identificatore** casella di testo, tipo di valore hello di`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="f385a-160">In hello **Identifier** textbox, type hello value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f385a-161">Questo valore non è hello reale.</span><span class="sxs-lookup"><span data-stu-id="f385a-161">This value is not hello real.</span></span> <span data-ttu-id="f385a-162">Aggiornare questo valore con URL hello effettivo Sign-on.</span><span class="sxs-lookup"><span data-stu-id="f385a-162">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="f385a-163">Contatto [team di supporto Client di AirWatch](http://www.air-watch.com/company/contact-us/) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="f385a-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) tooget this value.</span></span> 
 
4. <span data-ttu-id="f385a-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f385a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="f385a-166">In hello **AirWatch configurazione** fare clic su **configurare AirWatch** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="f385a-166">On hello **AirWatch Configuration** section, click **Configure AirWatch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f385a-167">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f385a-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="f385a-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f385a-169">Click **Save** button.</span></span>

    <span data-ttu-id="f385a-170">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="f385a-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="f385a-171">In una finestra del web browser, accedere come amministratore nel sito della società AirWatch di tooyour.</span><span class="sxs-lookup"><span data-stu-id="f385a-171">In a different web browser window, log in tooyour AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="f385a-172">Nel riquadro di spostamento a sinistra di hello, fare clic su **account**, quindi fare clic su **amministratori**.</span><span class="sxs-lookup"><span data-stu-id="f385a-172">In hello left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="f385a-173">![Amministratori](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Amministratori")</span><span class="sxs-lookup"><span data-stu-id="f385a-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="f385a-174">Espandere hello **impostazioni** menu e quindi fare clic su **servizi Directory**.</span><span class="sxs-lookup"><span data-stu-id="f385a-174">Expand hello **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="f385a-175">![Impostazioni](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="f385a-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="f385a-176">Fare clic su hello **utente** scheda hello **DN di Base** casella di testo, digitare il nome di dominio e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="f385a-176">Click hello **User** tab, in hello **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="f385a-177">![Utente](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Utente")</span><span class="sxs-lookup"><span data-stu-id="f385a-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="f385a-178">Fare clic su hello **Server** scheda.</span><span class="sxs-lookup"><span data-stu-id="f385a-178">Click hello **Server** tab.</span></span>
   
   <span data-ttu-id="f385a-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span><span class="sxs-lookup"><span data-stu-id="f385a-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="f385a-180">Eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f385a-180">Perform hello following steps:</span></span>
    
    <span data-ttu-id="f385a-181">![Caricamento](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Caricamento")</span><span class="sxs-lookup"><span data-stu-id="f385a-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="f385a-182">a.</span><span class="sxs-lookup"><span data-stu-id="f385a-182">a.</span></span> <span data-ttu-id="f385a-183">Per **Directory Type** selezionare **None**.</span><span class="sxs-lookup"><span data-stu-id="f385a-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="f385a-184">b.</span><span class="sxs-lookup"><span data-stu-id="f385a-184">b.</span></span> <span data-ttu-id="f385a-185">Selezionare **Use SAML For Authentication**.</span><span class="sxs-lookup"><span data-stu-id="f385a-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="f385a-186">c.</span><span class="sxs-lookup"><span data-stu-id="f385a-186">c.</span></span> <span data-ttu-id="f385a-187">tooupload hello certificato scaricato, fare clic su **caricare**.</span><span class="sxs-lookup"><span data-stu-id="f385a-187">tooupload hello downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="f385a-188">In hello **richiesta** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f385a-188">In hello **Request** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="f385a-189">![Richiesta](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Richiesta")</span><span class="sxs-lookup"><span data-stu-id="f385a-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="f385a-190">a.</span><span class="sxs-lookup"><span data-stu-id="f385a-190">a.</span></span> <span data-ttu-id="f385a-191">Per **Request Binding Type** selezionare **POST**.</span><span class="sxs-lookup"><span data-stu-id="f385a-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="f385a-192">b.</span><span class="sxs-lookup"><span data-stu-id="f385a-192">b.</span></span> <span data-ttu-id="f385a-193">Nel portale di Azure su hello hello **Configura accesso single sign-on in Airwatch** nella pagina, hello copia **SAML Single Sign-On Service URL** valore e quindi incollarlo hello **Provider di identità Single Sign On URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f385a-193">In hello Azure portal, on hello **Configure single sign-on at Airwatch** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="f385a-194">c.</span><span class="sxs-lookup"><span data-stu-id="f385a-194">c.</span></span> <span data-ttu-id="f385a-195">Per **NameID format** selezionare **Email address**.</span><span class="sxs-lookup"><span data-stu-id="f385a-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="f385a-196">d.</span><span class="sxs-lookup"><span data-stu-id="f385a-196">d.</span></span> <span data-ttu-id="f385a-197">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f385a-197">Click **Save**.</span></span>

14. <span data-ttu-id="f385a-198">Fare clic su hello **utente** scheda nuovamente.</span><span class="sxs-lookup"><span data-stu-id="f385a-198">Click hello **User** tab again.</span></span>
    
    <span data-ttu-id="f385a-199">![Utente](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Utente")</span><span class="sxs-lookup"><span data-stu-id="f385a-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="f385a-200">In hello **attributo** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f385a-200">In hello **Attribute** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="f385a-201">![Attributo](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attributo")</span><span class="sxs-lookup"><span data-stu-id="f385a-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="f385a-202">a.</span><span class="sxs-lookup"><span data-stu-id="f385a-202">a.</span></span> <span data-ttu-id="f385a-203">In hello **identificatore di oggetto** casella tipo **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="f385a-203">In hello **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="f385a-204">b.</span><span class="sxs-lookup"><span data-stu-id="f385a-204">b.</span></span> <span data-ttu-id="f385a-205">In hello **Username** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="f385a-205">In hello **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="f385a-206">c.</span><span class="sxs-lookup"><span data-stu-id="f385a-206">c.</span></span> <span data-ttu-id="f385a-207">In hello **nome visualizzato** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="f385a-207">In hello **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="f385a-208">d.</span><span class="sxs-lookup"><span data-stu-id="f385a-208">d.</span></span> <span data-ttu-id="f385a-209">In hello **nome** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="f385a-209">In hello **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="f385a-210">e.</span><span class="sxs-lookup"><span data-stu-id="f385a-210">e.</span></span> <span data-ttu-id="f385a-211">In hello **cognome** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="f385a-211">In hello **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="f385a-212">f.</span><span class="sxs-lookup"><span data-stu-id="f385a-212">f.</span></span> <span data-ttu-id="f385a-213">In hello **posta elettronica** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="f385a-213">In hello **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="f385a-214">g.</span><span class="sxs-lookup"><span data-stu-id="f385a-214">g.</span></span> <span data-ttu-id="f385a-215">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f385a-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f385a-216">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f385a-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="f385a-217">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f385a-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f385a-219">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f385a-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f385a-220">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f385a-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f385a-222">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f385a-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f385a-224">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f385a-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f385a-226">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f385a-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f385a-228">a.</span><span class="sxs-lookup"><span data-stu-id="f385a-228">a.</span></span> <span data-ttu-id="f385a-229">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f385a-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f385a-230">b.</span><span class="sxs-lookup"><span data-stu-id="f385a-230">b.</span></span> <span data-ttu-id="f385a-231">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f385a-231">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="f385a-232">c.</span><span class="sxs-lookup"><span data-stu-id="f385a-232">c.</span></span> <span data-ttu-id="f385a-233">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="f385a-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f385a-234">d.</span><span class="sxs-lookup"><span data-stu-id="f385a-234">d.</span></span> <span data-ttu-id="f385a-235">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f385a-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="f385a-236">Creazione di un utente di test di AirWatch</span><span class="sxs-lookup"><span data-stu-id="f385a-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="f385a-237">toolog agli utenti di Azure AD tooenable in tooAirWatch, è necessario eseguirne il provisioning in tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="f385a-237">tooenable Azure AD users toolog in tooAirWatch, they must be provisioned in tooAirWatch.</span></span>

* <span data-ttu-id="f385a-238">Nel caso di AirWatch, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f385a-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="f385a-239">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f385a-239">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f385a-240">Accedi tooyour **AirWatch** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f385a-240">Log in tooyour **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="f385a-241">Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **account**, quindi fare clic su **utenti**.</span><span class="sxs-lookup"><span data-stu-id="f385a-241">In hello navigation pane on hello left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="f385a-242">![Utenti](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="f385a-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="f385a-243">In hello **utenti** menu, fare clic su **visualizzazione elenco**, quindi fare clic su **Aggiungi \> Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="f385a-243">In hello **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="f385a-244">![Aggiungere un utente](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="f385a-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="f385a-245">In hello **Add / Edit User** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f385a-245">On hello **Add / Edit User** dialog, perform hello following steps:</span></span>

   <span data-ttu-id="f385a-246">![Aggiungere un utente](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="f385a-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="f385a-247">Hello tipo **Username**, **Password**, **Conferma Password**, **nome**, **cognome**,  **Indirizzo di posta elettronica** relative caselle di testo di un valido di Azure all'account di Active Directory desiderata tooprovision in hello.</span><span class="sxs-lookup"><span data-stu-id="f385a-247">Type hello **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="f385a-248">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f385a-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="f385a-249">È possibile usare qualsiasi altro AirWatch utente account strumento di creazione o le API fornite da AirWatch tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="f385a-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f385a-250">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f385a-250">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f385a-251">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="f385a-251">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAirWatch.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f385a-253">**tooassign Britta Simon tooAirWatch, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f385a-253">**tooassign Britta Simon tooAirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="f385a-254">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f385a-254">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f385a-256">Nell'elenco di applicazioni hello, selezionare **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="f385a-256">In hello applications list, select **AirWatch**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="f385a-258">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f385a-258">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f385a-260">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f385a-260">Click **Add** button.</span></span> <span data-ttu-id="f385a-261">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f385a-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f385a-263">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f385a-263">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f385a-264">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f385a-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f385a-265">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f385a-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f385a-266">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f385a-266">Testing single sign-on</span></span>

<span data-ttu-id="f385a-267">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f385a-267">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f385a-268">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="f385a-268">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="f385a-269">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f385a-269">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f385a-270">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f385a-270">Additional resources</span></span>

* [<span data-ttu-id="f385a-271">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f385a-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f385a-272">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f385a-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

