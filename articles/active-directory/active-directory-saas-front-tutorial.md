---
title: 'Esercitazione: Integrazione di Azure Active Directory con Front | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e di primo piano.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="c57cc-103">Esercitazione: Integrazione di Azure Active Directory con Front</span><span class="sxs-lookup"><span data-stu-id="c57cc-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="c57cc-104">In questa esercitazione, è illustrato come toointegrate anteriore con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c57cc-104">In this tutorial, you learn how toointegrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c57cc-105">Integrazione di primo piano con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="c57cc-105">Integrating Front with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c57cc-106">È possibile controllare in Azure AD che ha accesso tooFront.</span><span class="sxs-lookup"><span data-stu-id="c57cc-106">You can control in Azure AD who has access tooFront.</span></span>
- <span data-ttu-id="c57cc-107">È possibile abilitare l'utenti tooautomatically get connesso tooFront (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c57cc-107">You can enable your users tooautomatically get signed-on tooFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c57cc-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c57cc-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c57cc-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c57cc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c57cc-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c57cc-110">Prerequisites</span></span>

<span data-ttu-id="c57cc-111">integrazione di tooconfigure Azure AD con inizio, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="c57cc-111">tooconfigure Azure AD integration with Front, you need hello following items:</span></span>

- <span data-ttu-id="c57cc-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c57cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c57cc-113">Sottoscrizione di Front abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c57cc-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c57cc-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="c57cc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c57cc-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="c57cc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c57cc-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c57cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c57cc-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c57cc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c57cc-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c57cc-118">Scenario description</span></span>
<span data-ttu-id="c57cc-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c57cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c57cc-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="c57cc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c57cc-121">Aggiunta di primo piano dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c57cc-121">Adding Front from hello gallery</span></span>
2. <span data-ttu-id="c57cc-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c57cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-hello-gallery"></a><span data-ttu-id="c57cc-123">Aggiunta di primo piano dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c57cc-123">Adding Front from hello gallery</span></span>
<span data-ttu-id="c57cc-124">integrazione hello tooconfigure di primo piano in Azure AD, è necessario tooadd Front dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c57cc-124">tooconfigure hello integration of Front into Azure AD, you need tooadd Front from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c57cc-125">**tooadd anteriore dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c57cc-125">**tooadd Front from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c57cc-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c57cc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="c57cc-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c57cc-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="c57cc-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c57cc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="c57cc-133">Nella casella di ricerca hello, digitare **front-**selezionare **anteriore** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c57cc-133">In hello search box, type **Front**, select **Front** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Primo piano nell'elenco risultati hello](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c57cc-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c57cc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c57cc-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Front usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c57cc-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c57cc-137">Per toowork di accesso singolo, Azure AD deve tooknow in primo piano quale utente hello controparte è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c57cc-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Front is tooa user in Azure AD.</span></span> <span data-ttu-id="c57cc-138">In altre parole, una relazione di collegamento tra un utente di Azure AD e in primo piano utente correlato hello deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="c57cc-138">In other words, a link relationship between an Azure AD user and hello related user in Front needs toobe established.</span></span>

<span data-ttu-id="c57cc-139">In primo piano, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="c57cc-139">In Front, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c57cc-140">tooconfigure e prova AD Azure single sign-on con inizio, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="c57cc-140">tooconfigure and test Azure AD single sign-on with Front, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c57cc-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c57cc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c57cc-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c57cc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c57cc-143">**[Creare un utente test anteriore](#create-a-front-test-user)**  -toohave un equivalente di Britta Simon in primo piano che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c57cc-143">**[Create a Front test user](#create-a-front-test-user)** - toohave a counterpart of Britta Simon in Front that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c57cc-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c57cc-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c57cc-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="c57cc-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c57cc-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c57cc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c57cc-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nell'applicazione di primo piano.</span><span class="sxs-lookup"><span data-stu-id="c57cc-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="c57cc-148">**tooconfigure AD Azure single sign-on con inizio, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c57cc-148">**tooconfigure Azure AD single sign-on with Front, perform hello following steps:**</span></span>

1. <span data-ttu-id="c57cc-149">Nel portale di Azure su hello hello **anteriore** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-149">In hello Azure portal, on hello **Front** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="c57cc-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c57cc-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="c57cc-153">In hello **dominio anteriore e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="c57cc-153">On hello **Front Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="c57cc-155">a.</span><span class="sxs-lookup"><span data-stu-id="c57cc-155">a.</span></span> <span data-ttu-id="c57cc-156">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="c57cc-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="c57cc-157">b.</span><span class="sxs-lookup"><span data-stu-id="c57cc-157">b.</span></span> <span data-ttu-id="c57cc-158">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="c57cc-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="c57cc-159">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="c57cc-159">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="c57cc-161">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="c57cc-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c57cc-162">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c57cc-162">These values are not real.</span></span> <span data-ttu-id="c57cc-163">Aggiornamento di questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On che vengono descritte più avanti nell'esercitazione o contatto [team di supporto Client anteriore](mailto:support@frontapp.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="c57cc-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) tooget these values.</span></span> 

5. <span data-ttu-id="c57cc-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c57cc-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="c57cc-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c57cc-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c57cc-168">In hello **configurazione front-** fare clic su **configurare anteriore** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="c57cc-168">On hello **Front Configuration** section, click **Configure Front** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c57cc-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="c57cc-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="c57cc-171">Tenant di primo piano tooyour Sign-on come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c57cc-171">Sign-on tooyour Front tenant as an administrator.</span></span>

9. <span data-ttu-id="c57cc-172">Andare troppo**impostazioni (icona della ruota dentata nella parte inferiore di hello dell'intestazione laterale sinistra hello) > Preferenze**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-172">Go too**Settings (cog icon at hello bottom of hello left sidebar) > Preferences**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="c57cc-174">Fare clic sul collegamento **Single Sign On** .</span><span class="sxs-lookup"><span data-stu-id="c57cc-174">Click **Single Sign On** link.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="c57cc-176">Selezionare **SAML** nell'elenco a discesa hello di **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-176">Select **SAML** in hello drop-down list of **Single Sign On**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="c57cc-178">In hello **punto di ingresso** casella di testo inserire il valore di hello di **URL servizio Single Sign-on** dalla configurazione guidata di Azure AD applicazione.</span><span class="sxs-lookup"><span data-stu-id="c57cc-178">In hello **Entry Point** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="c57cc-180">Aprire lo scaricato **Certificate(Base64)** file nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato di firma** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="c57cc-180">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Signing certificate** textbox.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="c57cc-182">In hello **le impostazioni del provider del servizio** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c57cc-182">On hello **Service provider settings** section, perform hello following steps:</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="c57cc-184">a.</span><span class="sxs-lookup"><span data-stu-id="c57cc-184">a.</span></span> <span data-ttu-id="c57cc-185">Copiare il valore di hello di **ID entità** e incollarlo in hello **identificatore** nella casella di testo **dominio anteriore e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c57cc-185">Copy hello value of **Entity ID** and paste it into hello **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="c57cc-186">b.</span><span class="sxs-lookup"><span data-stu-id="c57cc-186">b.</span></span> <span data-ttu-id="c57cc-187">Copiare il valore di hello di **URL ACS** e incollarlo in hello **Sign-on URL** nella casella di testo **dominio anteriore e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c57cc-187">Copy hello value of **ACS URL** and paste it into hello **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="c57cc-188">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c57cc-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="c57cc-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="c57cc-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c57cc-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c57cc-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c57cc-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c57cc-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c57cc-192">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c57cc-192">Create an Azure AD test user</span></span>

<span data-ttu-id="c57cc-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c57cc-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="c57cc-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c57cc-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c57cc-196">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c57cc-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c57cc-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c57cc-200">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c57cc-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c57cc-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c57cc-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c57cc-204">a.</span><span class="sxs-lookup"><span data-stu-id="c57cc-204">a.</span></span> <span data-ttu-id="c57cc-205">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c57cc-206">b.</span><span class="sxs-lookup"><span data-stu-id="c57cc-206">b.</span></span> <span data-ttu-id="c57cc-207">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c57cc-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c57cc-208">c.</span><span class="sxs-lookup"><span data-stu-id="c57cc-208">c.</span></span> <span data-ttu-id="c57cc-209">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="c57cc-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c57cc-210">d.</span><span class="sxs-lookup"><span data-stu-id="c57cc-210">d.</span></span> <span data-ttu-id="c57cc-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="c57cc-212">Creare un utente test di Front</span><span class="sxs-lookup"><span data-stu-id="c57cc-212">Create a Front test user</span></span>

<span data-ttu-id="c57cc-213">In questa sezione viene creato un utente di nome Britta Simon in Front.</span><span class="sxs-lookup"><span data-stu-id="c57cc-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="c57cc-214">Lavorare con [team di supporto Client anteriore](mailto:support@frontapp.com) per aggiungere gli utenti di hello nella piattaforma di primo piano hello.</span><span class="sxs-lookup"><span data-stu-id="c57cc-214">Work with [Front Client support team](mailto:support@frontapp.com) to add hello users in hello Front platform.</span></span> <span data-ttu-id="c57cc-215">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c57cc-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c57cc-216">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c57cc-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c57cc-217">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooFront.</span><span class="sxs-lookup"><span data-stu-id="c57cc-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFront.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="c57cc-219">**tooassign Britta Simon tooFront, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c57cc-219">**tooassign Britta Simon tooFront, perform hello following steps:**</span></span>

1. <span data-ttu-id="c57cc-220">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c57cc-222">Nell'elenco di applicazioni hello, selezionare **anteriore**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-222">In hello applications list, select **Front**.</span></span>

    ![collegamento di primo piano Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="c57cc-224">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="c57cc-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-226">Click **Add** button.</span></span> <span data-ttu-id="c57cc-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="c57cc-229">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="c57cc-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c57cc-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c57cc-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c57cc-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c57cc-232">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c57cc-232">Test single sign-on</span></span>

<span data-ttu-id="c57cc-233">obiettivo di Hello di questa sezione è tootest utilizzando Azure AD SSOconfiguration hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c57cc-233">hello objective of this section is tootest your Azure AD SSOconfiguration using hello Access Panel.</span></span>

<span data-ttu-id="c57cc-234">Quando si fa clic su riquadro anteriore hello in hello Pannello di accesso, è necessario ottenere l'applicazione Front tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="c57cc-234">When you click hello Front tile in hello Access Panel, you should get automatically signed-on tooyour Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c57cc-235">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c57cc-235">Additional resources</span></span>

* [<span data-ttu-id="c57cc-236">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c57cc-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c57cc-237">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c57cc-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

