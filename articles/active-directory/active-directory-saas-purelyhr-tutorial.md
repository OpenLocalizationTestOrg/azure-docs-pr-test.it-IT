---
title: 'Esercitazione: Integrazione di Azure Active Directory con PurelyHR | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e PurelyHR.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: bdc1748ed650cff36b1ef7d7330dd2a17b3bc760
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="07492-103">Esercitazione: Integrazione di Azure Active Directory con PurelyHR</span><span class="sxs-lookup"><span data-stu-id="07492-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="07492-104">In questa esercitazione, è illustrato come toointegrate PurelyHR con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07492-104">In this tutorial, you learn how toointegrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07492-105">Integrazione PurelyHR con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="07492-105">Integrating PurelyHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="07492-106">È possibile controllare in Azure AD che ha accesso tooPurelyHR</span><span class="sxs-lookup"><span data-stu-id="07492-106">You can control in Azure AD who has access tooPurelyHR</span></span>
- <span data-ttu-id="07492-107">È possibile abilitare l'utenti tooautomatically get connesso tooPurelyHR (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="07492-107">You can enable your users tooautomatically get signed-on tooPurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="07492-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="07492-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="07492-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07492-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07492-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="07492-110">Prerequisites</span></span>

<span data-ttu-id="07492-111">integrazione di Azure AD con PurelyHR tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="07492-111">tooconfigure Azure AD integration with PurelyHR, you need hello following items:</span></span>

- <span data-ttu-id="07492-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07492-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07492-113">Sottoscrizione di PurelyHR abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="07492-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07492-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="07492-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07492-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="07492-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07492-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="07492-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07492-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07492-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07492-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="07492-118">Scenario description</span></span>
<span data-ttu-id="07492-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="07492-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07492-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="07492-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07492-121">Aggiunta di PurelyHR dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="07492-121">Adding PurelyHR from hello gallery</span></span>
2. <span data-ttu-id="07492-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07492-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-hello-gallery"></a><span data-ttu-id="07492-123">Aggiunta di PurelyHR dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="07492-123">Adding PurelyHR from hello gallery</span></span>
<span data-ttu-id="07492-124">integrazione hello tooconfigure di PurelyHR in Azure AD, è necessario tooadd PurelyHR dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="07492-124">tooconfigure hello integration of PurelyHR into Azure AD, you need tooadd PurelyHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="07492-125">**tooadd PurelyHR dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07492-125">**tooadd PurelyHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="07492-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="07492-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07492-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="07492-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="07492-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="07492-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="07492-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="07492-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="07492-133">Nella casella di ricerca hello, digitare **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="07492-133">In hello search box, type **PurelyHR**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="07492-135">Nel riquadro dei risultati hello, selezionare **PurelyHR**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="07492-135">In hello results panel, select **PurelyHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="07492-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07492-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="07492-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PurelyHR con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="07492-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="07492-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in PurelyHR è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07492-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PurelyHR is tooa user in Azure AD.</span></span> <span data-ttu-id="07492-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in PurelyHR deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="07492-140">In other words, a link relationship between an Azure AD user and hello related user in PurelyHR needs toobe established.</span></span>

<span data-ttu-id="07492-141">In PurelyHR, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="07492-141">In PurelyHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="07492-142">tooconfigure e prova AD Azure single sign-on con PurelyHR, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="07492-142">tooconfigure and test Azure AD single sign-on with PurelyHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="07492-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="07492-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="07492-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07492-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07492-145">**[Creazione di un utente test PurelyHR](#creating-a-purelyhr-test-user)**  -toohave un equivalente di Britta Simon in PurelyHR che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="07492-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - toohave a counterpart of Britta Simon in PurelyHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="07492-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="07492-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07492-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="07492-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="07492-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07492-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="07492-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="07492-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="07492-150">**Azure AD tooconfigure single sign-on con PurelyHR, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07492-150">**tooconfigure Azure AD single sign-on with PurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="07492-151">Nel portale di Azure su hello hello **PurelyHR** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="07492-151">In hello Azure portal, on hello **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="07492-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="07492-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="07492-155">In hello **PurelyHR dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="07492-155">On hello **PurelyHR Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="07492-157">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="07492-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="07492-158">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="07492-158">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="07492-160">In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="07492-160">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="07492-161">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="07492-161">These values are not hello real.</span></span> <span data-ttu-id="07492-162">Aggiornare questi valori con l'URL di risposta effettivo hello e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="07492-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="07492-163">Contatto [team di supporto PurelyHR Client](http://support.purelyhr.com/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="07492-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) tooget these values.</span></span> 

5. <span data-ttu-id="07492-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="07492-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="07492-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="07492-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="07492-168">In hello **PurelyHR configurazione** fare clic su **configurare PurelyHR** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="07492-168">On hello **PurelyHR Configuration** section, click **Configure PurelyHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="07492-169">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="07492-169">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="07492-171">tooconfigure single sign-on sul **PurelyHR** lato, sito Web tootheir account di accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="07492-171">tooconfigure single sign-on on **PurelyHR** side, login tootheir website as an administrator.</span></span>

9. <span data-ttu-id="07492-172">Aprire hello **Dashboard** dalle opzioni di hello nella barra degli strumenti hello e fare clic su **impostazioni SSO**.</span><span class="sxs-lookup"><span data-stu-id="07492-172">Open hello **Dashboard** from hello options in hello toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="07492-173">Incolla hello valori nelle caselle hello come descritto sotto-</span><span class="sxs-lookup"><span data-stu-id="07492-173">Paste hello values in hello boxes as described below-</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="07492-175">a.</span><span class="sxs-lookup"><span data-stu-id="07492-175">a.</span></span> <span data-ttu-id="07492-176">Aprire hello **Certificate(Bas64)** scaricato da hello portale Azure nel blocco note e copiare valore certificato hello.</span><span class="sxs-lookup"><span data-stu-id="07492-176">Open hello **Certificate(Bas64)** downloaded from hello Azure portal in notepad and copy hello certificate value.</span></span> <span data-ttu-id="07492-177">Valore hello Incolla copiato hello **certificato x. 509** casella.</span><span class="sxs-lookup"><span data-stu-id="07492-177">Paste hello copied value into hello **X.509 Certificate** box.</span></span>

    <span data-ttu-id="07492-178">b.</span><span class="sxs-lookup"><span data-stu-id="07492-178">b.</span></span> <span data-ttu-id="07492-179">In hello **Idp Issuer URL** incollare hello **ID entità SAML** copiato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="07492-179">In hello **Idp Issuer URL** box, paste hello **SAML Entity ID** copied from hello Azure portal.</span></span>

    <span data-ttu-id="07492-180">c.</span><span class="sxs-lookup"><span data-stu-id="07492-180">c.</span></span> <span data-ttu-id="07492-181">In hello **Idp Endpoint URL** incollare hello **SAML Single Sign-On Service URL** copiato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="07492-181">In hello **Idp Endpoint URL** box, paste hello **SAML Single Sign-On Service URL** copied from hello Azure portal.</span></span> 

    <span data-ttu-id="07492-182">d.</span><span class="sxs-lookup"><span data-stu-id="07492-182">d.</span></span> <span data-ttu-id="07492-183">Controllare hello **Auto-Create Users** casella di controllo tooenable provisioning utente automatico in PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="07492-183">Check hello **Auto-Create Users** checkbox tooenable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="07492-184">e.</span><span class="sxs-lookup"><span data-stu-id="07492-184">e.</span></span> <span data-ttu-id="07492-185">Fare clic su **Salva modifiche** impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="07492-185">Click **Save Changes** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="07492-186">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="07492-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="07492-187">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="07492-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="07492-188">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07492-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="07492-189">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07492-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="07492-190">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="07492-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="07492-192">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07492-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="07492-193">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="07492-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07492-195">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="07492-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07492-197">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="07492-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07492-199">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07492-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07492-201">a.</span><span class="sxs-lookup"><span data-stu-id="07492-201">a.</span></span> <span data-ttu-id="07492-202">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07492-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07492-203">b.</span><span class="sxs-lookup"><span data-stu-id="07492-203">b.</span></span> <span data-ttu-id="07492-204">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="07492-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="07492-205">c.</span><span class="sxs-lookup"><span data-stu-id="07492-205">c.</span></span> <span data-ttu-id="07492-206">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="07492-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="07492-207">d.</span><span class="sxs-lookup"><span data-stu-id="07492-207">d.</span></span> <span data-ttu-id="07492-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="07492-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="07492-209">Creazione di un utente test di PurelyHR</span><span class="sxs-lookup"><span data-stu-id="07492-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="07492-210">toolog agli utenti di Azure AD tooenable in tooPurelyHR, è necessario eseguirne il provisioning in PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="07492-210">tooenable Azure AD users toolog in tooPurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="07492-211">In PurelyHR, il provisioning è un'attività automatica e non sono necessari passaggi manuali se è abilitato il provisioning utente automatico.</span><span class="sxs-lookup"><span data-stu-id="07492-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="07492-212">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="07492-212">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="07492-213">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPurelyHR.</span><span class="sxs-lookup"><span data-stu-id="07492-213">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPurelyHR.</span></span>

![Assegna utente][200] 

<span data-ttu-id="07492-215">**tooassign Britta Simon tooPurelyHR, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07492-215">**tooassign Britta Simon tooPurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="07492-216">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="07492-216">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="07492-218">Nell'elenco di applicazioni hello, selezionare **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="07492-218">In hello applications list, select **PurelyHR**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="07492-220">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="07492-220">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="07492-222">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="07492-222">Click **Add** button.</span></span> <span data-ttu-id="07492-223">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="07492-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="07492-225">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="07492-225">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="07492-226">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="07492-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07492-227">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="07492-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="07492-228">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="07492-228">Testing single sign-on</span></span>

<span data-ttu-id="07492-229">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="07492-229">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="07492-230">Fare clic su hello assorbire LMS riquadro in hello Pannello di accesso, viene generata automaticamente firmato in tooyour assorbire LMS applicazione.</span><span class="sxs-lookup"><span data-stu-id="07492-230">Click hello Absorb LMS tile in hello Access Panel, you get automatically signed-on tooyour Absorb LMS application.</span></span>

<span data-ttu-id="07492-231">Per ulteriori informazioni su hello Pannello di accesso, vedere.</span><span class="sxs-lookup"><span data-stu-id="07492-231">For more information about hello Access Panel, see.</span></span> <span data-ttu-id="07492-232">[Introduzione toohello Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="07492-232">[Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07492-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="07492-233">Additional resources</span></span>

* [<span data-ttu-id="07492-234">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07492-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07492-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07492-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

