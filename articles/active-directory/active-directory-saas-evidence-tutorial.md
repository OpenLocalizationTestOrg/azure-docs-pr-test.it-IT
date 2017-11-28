---
title: 'Esercitazione: Integrazione di Azure Active Directory con Evidence.com | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed Evidence.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="ec3a9-103">Esercitazione: Integrazione di Azure Active Directory con Evidence.com</span><span class="sxs-lookup"><span data-stu-id="ec3a9-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="ec3a9-104">In questa esercitazione, è illustrato come toointegrate Evidence.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ec3a9-104">In this tutorial, you learn how toointegrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ec3a9-105">Integrazione Evidence.com con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ec3a9-105">Integrating Evidence.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ec3a9-106">È possibile controllare in Azure AD che ha accesso tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-106">You can control in Azure AD who has access tooEvidence.com.</span></span>
- <span data-ttu-id="ec3a9-107">È possibile abilitare l'utenti tooautomatically get connesso tooEvidence.com (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-107">You can enable your users tooautomatically get signed-on tooEvidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ec3a9-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ec3a9-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ec3a9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec3a9-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ec3a9-110">Prerequisites</span></span>

<span data-ttu-id="ec3a9-111">integrazione di Azure AD con Evidence.com tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ec3a9-111">tooconfigure Azure AD integration with Evidence.com, you need hello following items:</span></span>

- <span data-ttu-id="ec3a9-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ec3a9-113">Sottoscrizione di Evidence.com abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ec3a9-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ec3a9-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ec3a9-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ec3a9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ec3a9-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ec3a9-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec3a9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ec3a9-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ec3a9-118">Scenario description</span></span>
<span data-ttu-id="ec3a9-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ec3a9-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ec3a9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ec3a9-121">Aggiunta di Evidence.com dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ec3a9-121">Adding Evidence.com from hello gallery</span></span>
2. <span data-ttu-id="ec3a9-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec3a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-hello-gallery"></a><span data-ttu-id="ec3a9-123">Aggiunta di Evidence.com dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ec3a9-123">Adding Evidence.com from hello gallery</span></span>
<span data-ttu-id="ec3a9-124">integrazione hello tooconfigure di Evidence.com in Azure AD, è necessario tooadd Evidence.com dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-124">tooconfigure hello integration of Evidence.com into Azure AD, you need tooadd Evidence.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ec3a9-125">**tooadd Evidence.com dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ec3a9-125">**tooadd Evidence.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec3a9-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="ec3a9-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ec3a9-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="ec3a9-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="ec3a9-133">Nella casella di ricerca hello, digitare **Evidence.com**selezionare **Evidence.com** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-133">In hello search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ec3a9-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec3a9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ec3a9-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Evidence.com con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ec3a9-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ec3a9-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Evidence.com è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evidence.com is tooa user in Azure AD.</span></span> <span data-ttu-id="ec3a9-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Evidence.com deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-138">In other words, a link relationship between an Azure AD user and hello related user in Evidence.com needs toobe established.</span></span>

<span data-ttu-id="ec3a9-139">In Evidence.com, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-139">In Evidence.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ec3a9-140">tooconfigure e prova AD Azure single sign-on con Evidence.com, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ec3a9-140">tooconfigure and test Azure AD single sign-on with Evidence.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ec3a9-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ec3a9-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ec3a9-143">**[Creare un utente test Evidence.com](#create-a-evidencecom-test-user)**  -toohave un equivalente di Britta Simon in Evidence.com che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - toohave a counterpart of Britta Simon in Evidence.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ec3a9-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ec3a9-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ec3a9-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec3a9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ec3a9-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="ec3a9-148">**Azure AD tooconfigure single sign-on con Evidence.com, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ec3a9-148">**tooconfigure Azure AD single sign-on with Evidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec3a9-149">Nel portale di Azure su hello hello **Evidence.com** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-149">In hello Azure portal, on hello **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="ec3a9-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="ec3a9-153">In hello **Evidence.com dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ec3a9-153">On hello **Evidence.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="ec3a9-155">a.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-155">a.</span></span> <span data-ttu-id="ec3a9-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="ec3a9-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="ec3a9-157">b.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-157">b.</span></span> <span data-ttu-id="ec3a9-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="ec3a9-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ec3a9-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ec3a9-159">These values are not real.</span></span> <span data-ttu-id="ec3a9-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ec3a9-161">Contatto [team di supporto Evidence.com Client](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget these values.</span></span> 

4. <span data-ttu-id="ec3a9-162">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="ec3a9-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ec3a9-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ec3a9-166">In hello **Evidence.com configurazione** fare clic su **configurare Evidence.com** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-166">On hello **Evidence.com Configuration** section, click **Configure Evidence.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ec3a9-167">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ec3a9-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="ec3a9-169">In una finestra del browser web separato, account di accesso tooyour Evidence.com tenant come amministratore e passare troppo**Admin** scheda</span><span class="sxs-lookup"><span data-stu-id="ec3a9-169">In a separate web browser window, login tooyour Evidence.com tenant as an administrator and navigate too**Admin** Tab</span></span>

8. <span data-ttu-id="ec3a9-170">Fare clic su **Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="ec3a9-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="ec3a9-171">Selezionare **SAML Based Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="ec3a9-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="ec3a9-172">Hello copia **ID entità SAML**, **SAML Single Sign-On Service URL** e **Sign-Out URL** i valori mostrati nei campi corrispondenti toohello Evidence.com e di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-172">Copy hello **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in hello Azure portal and toohello corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="ec3a9-173">Aprire il file Certificate(Base64) scaricato nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato di sicurezza** casella.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-173">Open your downloaded Certificate(Base64) file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Security Certificate** box.</span></span> 

12. <span data-ttu-id="ec3a9-174">Salvare la configurazione di hello in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-174">Save hello configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="ec3a9-175">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ec3a9-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ec3a9-176">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ec3a9-177">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ec3a9-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ec3a9-178">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec3a9-178">Create an Azure AD test user</span></span>

<span data-ttu-id="ec3a9-179">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="ec3a9-181">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ec3a9-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec3a9-182">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-182">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ec3a9-184">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-184">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ec3a9-186">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-186">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ec3a9-188">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ec3a9-188">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ec3a9-190">a.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-190">a.</span></span> <span data-ttu-id="ec3a9-191">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-191">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ec3a9-192">b.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-192">b.</span></span> <span data-ttu-id="ec3a9-193">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-193">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ec3a9-194">c.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-194">c.</span></span> <span data-ttu-id="ec3a9-195">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-195">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ec3a9-196">d.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-196">d.</span></span> <span data-ttu-id="ec3a9-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="ec3a9-198">Creare un utente test per Evidence.com</span><span class="sxs-lookup"><span data-stu-id="ec3a9-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="ec3a9-199">Per Azure AD utenti toobe in grado di toosign in è necessario eseguirne il provisioning per l'accesso all'interno di hello Evidence.com applicazione.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-199">For Azure AD users toobe able toosign in, they must be provisioned for access inside hello Evidence.com application.</span></span> <span data-ttu-id="ec3a9-200">In questa sezione viene descritto come degli account utente di Azure AD toocreate all'interno di Evidence.com</span><span class="sxs-lookup"><span data-stu-id="ec3a9-200">This section describes how toocreate Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="ec3a9-201">**un account utente in Evidence.com tooprovision:**</span><span class="sxs-lookup"><span data-stu-id="ec3a9-201">**tooprovision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="ec3a9-202">In una finestra del Web browser accedere al sito aziendale Evidence.com come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="ec3a9-203">Passare troppo**Admin** scheda.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-203">Navigate too**Admin** tab.</span></span>

3. <span data-ttu-id="ec3a9-204">Fare clic su **Add User**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="ec3a9-205">Fare clic su hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-205">Click hello **Add** button.</span></span>

5. <span data-ttu-id="ec3a9-206">Hello **indirizzo di posta elettronica** di hello aggiunto l'utente deve corrispondere hello nome utente di utenti hello in Azure AD che si desiderano toogive accesso.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-206">hello **Email Address** of hello added user must match hello username of hello users in Azure AD who you wish toogive access.</span></span> <span data-ttu-id="ec3a9-207">Se l'indirizzo di posta elettronica e il nome utente hello non sono hello stesso valore all'interno dell'organizzazione, è possibile utilizzare hello **Evidence.com > attributi > Single Sign-On** sezione di hello toochange portale Azure hello nameidenitifer inviati indirizzo di posta elettronica tooEvidence.com toobe hello.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-207">If hello username and email address are not hello same value in your organization, you can use hello **Evidence.com > Attributes > Single Sign-On** section of hello Azure portal toochange hello nameidenitifer sent tooEvidence.com toobe hello email address.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ec3a9-208">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec3a9-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ec3a9-209">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvidence.com.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="ec3a9-211">**tooassign Britta Simon tooEvidence.com, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ec3a9-211">**tooassign Britta Simon tooEvidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec3a9-212">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ec3a9-214">Nell'elenco di applicazioni hello, selezionare **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-214">In hello applications list, select **Evidence.com**.</span></span>

    ![collegamento Evidence.com Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="ec3a9-216">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="ec3a9-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-218">Click **Add** button.</span></span> <span data-ttu-id="ec3a9-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="ec3a9-221">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ec3a9-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ec3a9-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ec3a9-224">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ec3a9-224">Test single sign-on</span></span>

<span data-ttu-id="ec3a9-225">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ec3a9-226">Quando si fa clic su riquadro Evidence.com hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Evidence.com applicazione.</span><span class="sxs-lookup"><span data-stu-id="ec3a9-226">When you click hello Evidence.com tile in hello Access Panel, you should get automatically signed-on tooyour Evidence.com application.</span></span>
<span data-ttu-id="ec3a9-227">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ec3a9-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ec3a9-228">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ec3a9-228">Additional resources</span></span>

* [<span data-ttu-id="ec3a9-229">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec3a9-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ec3a9-230">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec3a9-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

