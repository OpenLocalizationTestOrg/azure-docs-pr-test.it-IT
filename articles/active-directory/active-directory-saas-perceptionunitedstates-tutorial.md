---
title: 'Esercitazione: Integrazione di Azure Active Directory con Perception United States (Non-UltiPro) | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e percezione United States (Non-UltiPro).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="bba7c-103">Esercitazione: Integrazione di Azure Active Directory con Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="bba7c-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="bba7c-104">In questa esercitazione, è illustrato come toointegrate percezione italy (Non-UltiPro) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bba7c-104">In this tutorial, you learn how toointegrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bba7c-105">Integrazione percezione United States (Non-UltiPro) con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="bba7c-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bba7c-106">È possibile controllare in Azure AD che ha accesso tooPerception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="bba7c-106">You can control in Azure AD who has access tooPerception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="bba7c-107">È possibile abilitare l'utenti tooautomatically get connesso tooPerception United States (Non-UltiPro) (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bba7c-107">You can enable your users tooautomatically get signed-on tooPerception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bba7c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bba7c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="bba7c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bba7c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bba7c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bba7c-110">Prerequisites</span></span>

<span data-ttu-id="bba7c-111">integrazione di Azure AD con percezione United States (Non-UltiPro) tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="bba7c-111">tooconfigure Azure AD integration with Perception United States (Non-UltiPro), you need hello following items:</span></span>

- <span data-ttu-id="bba7c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bba7c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bba7c-113">Sottoscrizione di Perception United States (Non-UltiPro) abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bba7c-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bba7c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="bba7c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bba7c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="bba7c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bba7c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="bba7c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bba7c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bba7c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bba7c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="bba7c-118">Scenario description</span></span>
<span data-ttu-id="bba7c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="bba7c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bba7c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="bba7c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bba7c-121">Aggiunta di percezione United States (Non-UltiPro) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bba7c-121">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
2. <span data-ttu-id="bba7c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bba7c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a><span data-ttu-id="bba7c-123">Aggiunta di percezione United States (Non-UltiPro) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bba7c-123">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
<span data-ttu-id="bba7c-124">integrazione di hello di tooconfigure di percezione italy (Non-UltiPro) in Azure AD, è necessario tooadd percezione United States (Non-UltiPro) dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="bba7c-124">tooconfigure hello integration of Perception United States (Non-UltiPro) into Azure AD, you need tooadd Perception United States (Non-UltiPro) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bba7c-125">**tooadd percezione italy (Non-UltiPro) dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bba7c-125">**tooadd Perception United States (Non-UltiPro) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bba7c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="bba7c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="bba7c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bba7c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="bba7c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bba7c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="bba7c-133">Nella casella di ricerca hello, digitare **percezione United States (Non-UltiPro)**selezionare **percezione United States (Non-UltiPro)** dal pannello risultati quindi fare clic su **Aggiungi** tooadd pulsante applicazione Hello.</span><span class="sxs-lookup"><span data-stu-id="bba7c-133">In hello search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Stati Uniti di percezione (Non-UltiPro) nell'elenco risultati hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bba7c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bba7c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bba7c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Perception United States (Non-UltiPro) usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bba7c-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bba7c-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello percezione United States (Non-UltiPro) è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bba7c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Perception United States (Non-UltiPro) is tooa user in Azure AD.</span></span> <span data-ttu-id="bba7c-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello percezione United States (Non-UltiPro) richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="bba7c-138">In other words, a link relationship between an Azure AD user and hello related user in Perception United States (Non-UltiPro) needs toobe established.</span></span>

<span data-ttu-id="bba7c-139">Nella visualizzazione degli Stati Uniti (Non-UltiPro), assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="bba7c-139">In Perception United States (Non-UltiPro), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bba7c-140">tooconfigure e test di Azure AD single sign-on con percezione United States (Non-UltiPro), è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="bba7c-140">tooconfigure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bba7c-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bba7c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bba7c-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bba7c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bba7c-143">**[Creare un utente test percezione United States (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave un equivalente di Britta Simon in percezione Stati Uniti (Non-UltiPro) che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="bba7c-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - toohave a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bba7c-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bba7c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bba7c-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="bba7c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bba7c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bba7c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bba7c-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione percezione United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="bba7c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="bba7c-148">**tooconfigure Azure AD accesso single sign-on con percezione United States (Non-UltiPro), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bba7c-148">**tooconfigure Azure AD single sign-on with Perception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="bba7c-149">Nel portale di Azure su hello hello **percezione United States (Non-UltiPro)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-149">In hello Azure portal, on hello **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="bba7c-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bba7c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="bba7c-153">In hello **dominio percezione United States (Non-UltiPro) e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bba7c-153">On hello **Perception United States (Non-UltiPro) Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="bba7c-155">a.</span><span class="sxs-lookup"><span data-stu-id="bba7c-155">a.</span></span> <span data-ttu-id="bba7c-156">In hello **identificatore** casella di testo, digitare l'URL hello:`https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="bba7c-156">In hello **Identifier** textbox, type hello URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="bba7c-157">b.</span><span class="sxs-lookup"><span data-stu-id="bba7c-157">b.</span></span> <span data-ttu-id="bba7c-158">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="bba7c-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bba7c-159">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="bba7c-159">hello value is not real.</span></span> <span data-ttu-id="bba7c-160">È possibile aggiornare il valore di hello con URL risposta effettivo hello illustrato più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="bba7c-160">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="bba7c-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="bba7c-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="bba7c-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="bba7c-163">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bba7c-165">In hello **configurazione percezione United States (Non-UltiPro)** fare clic su **configurare percezione United States (Non-UltiPro)** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="bba7c-165">On hello **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bba7c-166">Hello copia **ID entità SAML** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="bba7c-166">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="bba7c-167">a.</span><span class="sxs-lookup"><span data-stu-id="bba7c-167">a.</span></span> <span data-ttu-id="bba7c-168">Hello **percezione United States (Non-UltiPro)** richiede l'applicazione hello **ID entità SAML** valore, che è stato copiato, toobe uri codificato.</span><span class="sxs-lookup"><span data-stu-id="bba7c-168">hello **Perception United States (Non-UltiPro)** application requires hello **SAML Entity ID** value, which you have copied, toobe uri encoded.</span></span> <span data-ttu-id="bba7c-169">valore dell'uri con codificata hello tooget, seguente di hello utilizzo collegamento:**http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-169">tooget hello uri encoded value, use hello following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="bba7c-170">b.</span><span class="sxs-lookup"><span data-stu-id="bba7c-170">b.</span></span> <span data-ttu-id="bba7c-171">Dopo aver ottenuto l'uri di hello valore codificato si combinarla con hello **URL di risposta** come indicato di seguito</span><span class="sxs-lookup"><span data-stu-id="bba7c-171">After getting hello uri encoded value combine it with hello **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="bba7c-172">c.</span><span class="sxs-lookup"><span data-stu-id="bba7c-172">c.</span></span> <span data-ttu-id="bba7c-173">Hello Incolla sopra valore hello **URL di risposta** nella casella di testo **dominio percezione United States (Non-UltiPro) e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="bba7c-173">Paste hello above value in hello **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Configurazione di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="bba7c-175">In un'altra finestra del browser, accedere come amministratore nel sito della società di tooyour percezione United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="bba7c-175">In another browser window, sign on tooyour Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="bba7c-176">Nella barra degli strumenti principale hello, fare clic su **impostazioni Account**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-176">In hello main toolbar, click **Account Settings**.</span></span>

    ![Utente di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="bba7c-178">In hello **impostazioni Account** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bba7c-178">On hello **Account Settings** page, perform hello following steps:</span></span>

    ![Utente di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="bba7c-180">a.</span><span class="sxs-lookup"><span data-stu-id="bba7c-180">a.</span></span> <span data-ttu-id="bba7c-181">In hello **nome società** casella di testo, nome del tipo hello di hello **società**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-181">In hello **Company Name** textbox, type hello name of hello **Company**.</span></span>
    
    <span data-ttu-id="bba7c-182">b.</span><span class="sxs-lookup"><span data-stu-id="bba7c-182">b.</span></span> <span data-ttu-id="bba7c-183">In hello **nome Account** casella di testo, nome del tipo hello di hello **Account**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-183">In hello **Account Name** textbox, type hello name of hello **Account**.</span></span>

    <span data-ttu-id="bba7c-184">c.</span><span class="sxs-lookup"><span data-stu-id="bba7c-184">c.</span></span> <span data-ttu-id="bba7c-185">In **predefinito Reply-tooEmail** casella di testo, hello di tipo valido **posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-185">In **Default Reply-tooEmail** text box, type hello valid **Email**.</span></span>

    <span data-ttu-id="bba7c-186">d.</span><span class="sxs-lookup"><span data-stu-id="bba7c-186">d.</span></span> <span data-ttu-id="bba7c-187">Per **SSO Identity Provider** (Provider di identità SSO) selezionare **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="bba7c-188">In hello **configurazione di SSO** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bba7c-188">On hello **SSO Configuration** page, perform hello following steps:</span></span>

    ![Configurazione SSO di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="bba7c-190">a.</span><span class="sxs-lookup"><span data-stu-id="bba7c-190">a.</span></span> <span data-ttu-id="bba7c-191">Per **SAML NameID Type** (Tipo ID nome SAML) selezionare **EMAIL** (POSTA ELETTRONICA).</span><span class="sxs-lookup"><span data-stu-id="bba7c-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="bba7c-192">b.</span><span class="sxs-lookup"><span data-stu-id="bba7c-192">b.</span></span> <span data-ttu-id="bba7c-193">In hello **nome di configurazione di SSO** casella di testo, hello del tipo il **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-193">In hello **SSO Configuration Name** textbox, type hello name of your **Configuration**.</span></span>
    
    <span data-ttu-id="bba7c-194">c.</span><span class="sxs-lookup"><span data-stu-id="bba7c-194">c.</span></span> <span data-ttu-id="bba7c-195">In **nome Provider di identità** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bba7c-195">In **Identity Provider Name** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="bba7c-196">d.</span><span class="sxs-lookup"><span data-stu-id="bba7c-196">d.</span></span> <span data-ttu-id="bba7c-197">In **dominio SAML textbox**, immettere il dominio hello come  **@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="bba7c-197">In **SAML Domain textbox**, enter hello domain like **@contoso.com**.</span></span>

    <span data-ttu-id="bba7c-198">e.</span><span class="sxs-lookup"><span data-stu-id="bba7c-198">e.</span></span> <span data-ttu-id="bba7c-199">Fare clic su **caricare nuovamente** hello tooupload **Metadata XML** file.</span><span class="sxs-lookup"><span data-stu-id="bba7c-199">Click on **Upload Again** tooupload hello **Metadata XML** file.</span></span>

    <span data-ttu-id="bba7c-200">f.</span><span class="sxs-lookup"><span data-stu-id="bba7c-200">f.</span></span> <span data-ttu-id="bba7c-201">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="bba7c-202">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="bba7c-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bba7c-203">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="bba7c-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bba7c-204">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bba7c-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bba7c-205">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bba7c-205">Create an Azure AD test user</span></span>

<span data-ttu-id="bba7c-206">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="bba7c-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="bba7c-208">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bba7c-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bba7c-209">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="bba7c-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bba7c-211">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bba7c-213">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bba7c-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bba7c-215">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bba7c-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bba7c-217">a.</span><span class="sxs-lookup"><span data-stu-id="bba7c-217">a.</span></span> <span data-ttu-id="bba7c-218">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bba7c-219">b.</span><span class="sxs-lookup"><span data-stu-id="bba7c-219">b.</span></span> <span data-ttu-id="bba7c-220">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bba7c-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="bba7c-221">c.</span><span class="sxs-lookup"><span data-stu-id="bba7c-221">c.</span></span> <span data-ttu-id="bba7c-222">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="bba7c-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="bba7c-223">d.</span><span class="sxs-lookup"><span data-stu-id="bba7c-223">d.</span></span> <span data-ttu-id="bba7c-224">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="bba7c-225">Creare un utente di test di Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="bba7c-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="bba7c-226">In questa sezione viene creato un utente di nome Britta Simon in Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="bba7c-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="bba7c-227">Lavorare con [team di supporto percezione United States (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) utenti hello tooadd nella piattaforma di hello percezione United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="bba7c-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello users in hello Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bba7c-228">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bba7c-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="bba7c-229">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPerception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="bba7c-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerception United States (Non-UltiPro).</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="bba7c-231">**tooassign Britta Simon tooPerception United States (Non-UltiPro), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bba7c-231">**tooassign Britta Simon tooPerception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="bba7c-232">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="bba7c-234">Nell'elenco di applicazioni hello, selezionare **percezione United States (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-234">In hello applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![collegamento di Hello percezione United States (Non-UltiPro) nell'elenco delle applicazioni hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="bba7c-236">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="bba7c-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-238">Click **Add** button.</span></span> <span data-ttu-id="bba7c-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="bba7c-241">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="bba7c-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bba7c-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bba7c-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bba7c-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bba7c-244">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bba7c-244">Test single sign-on</span></span>

<span data-ttu-id="bba7c-245">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="bba7c-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bba7c-246">Quando si fa clic su riquadro percezione United States (Non-UltiPro) hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione percezione United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="bba7c-246">When you click hello Perception United States (Non-UltiPro) tile in hello Access Panel, you should get automatically signed-on tooyour Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="bba7c-247">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bba7c-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bba7c-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bba7c-248">Additional resources</span></span>

* [<span data-ttu-id="bba7c-249">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bba7c-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bba7c-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bba7c-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

