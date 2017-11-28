---
title: 'Esercitazione: Integrazione di Azure Active Directory con Mimecast Admin Console | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Mimecast Admin Console.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="cfdd3-103">Esercitazione: Integrazione di Azure Active Directory con Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="cfdd3-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="cfdd3-104">In questa esercitazione, è illustrato come toointegrate Mimecast Admin Console con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cfdd3-104">In this tutorial, you learn how toointegrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfdd3-105">Integrazione di Mimecast Admin Console con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="cfdd3-105">Integrating Mimecast Admin Console with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cfdd3-106">È possibile controllare in Azure AD che ha accesso tooMimecast Console di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-106">You can control in Azure AD who has access tooMimecast Admin Console.</span></span>
- <span data-ttu-id="cfdd3-107">È possibile abilitare l'utenti tooautomatically get connesso tooMimecast Console di amministrazione (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-107">You can enable your users tooautomatically get signed-on tooMimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cfdd3-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="cfdd3-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cfdd3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfdd3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cfdd3-110">Prerequisites</span></span>

<span data-ttu-id="cfdd3-111">integrazione di Azure AD con Mimecast Admin Console tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="cfdd3-111">tooconfigure Azure AD integration with Mimecast Admin Console, you need hello following items:</span></span>

- <span data-ttu-id="cfdd3-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cfdd3-113">Sottoscrizione di Mimecast Admin Console abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cfdd3-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cfdd3-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cfdd3-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="cfdd3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cfdd3-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cfdd3-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cfdd3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfdd3-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cfdd3-118">Scenario description</span></span>
<span data-ttu-id="cfdd3-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cfdd3-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="cfdd3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfdd3-121">Aggiunta di Mimecast Admin Console dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cfdd3-121">Adding Mimecast Admin Console from hello gallery</span></span>
2. <span data-ttu-id="cfdd3-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfdd3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a><span data-ttu-id="cfdd3-123">Aggiunta di Mimecast Admin Console dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cfdd3-123">Adding Mimecast Admin Console from hello gallery</span></span>
<span data-ttu-id="cfdd3-124">integrazione hello tooconfigure di Mimecast Admin Console in Azure AD, è necessario tooadd Mimecast Admin Console dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-124">tooconfigure hello integration of Mimecast Admin Console into Azure AD, you need tooadd Mimecast Admin Console from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cfdd3-125">**tooadd Mimecast Admin Console dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfdd3-125">**tooadd Mimecast Admin Console from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfdd3-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="cfdd3-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cfdd3-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="cfdd3-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="cfdd3-133">Nella casella di ricerca hello, digitare **Mimecast Admin Console**selezionare **Mimecast Admin Console** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-133">In hello search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Mimecast Admin Console nell'elenco risultati hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cfdd3-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfdd3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cfdd3-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Mimecast Admin Console con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cfdd3-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cfdd3-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Mimecast Admin Console è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Admin Console is tooa user in Azure AD.</span></span> <span data-ttu-id="cfdd3-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Mimecast Admin Console richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-138">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Admin Console needs toobe established.</span></span>

<span data-ttu-id="cfdd3-139">Nella Console di amministrazione di Mimecast, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-139">In Mimecast Admin Console, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cfdd3-140">tooconfigure e prova AD Azure single sign-on con Mimecast Admin Console, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="cfdd3-140">tooconfigure and test Azure AD single sign-on with Mimecast Admin Console, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cfdd3-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cfdd3-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cfdd3-143">**[Creare un utente test Mimecast Admin Console](#create-a-mimecast-admin-console-test-user)**  -toohave un equivalente di Britta Simon in Mimecast Admin Console che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - toohave a counterpart of Britta Simon in Mimecast Admin Console that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cfdd3-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cfdd3-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cfdd3-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfdd3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cfdd3-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="cfdd3-148">**tooconfigure Azure single sign-on AD Mimecast Admin console, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfdd3-148">**tooconfigure Azure AD single sign-on with Mimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfdd3-149">Nel portale di Azure su hello hello **Mimecast Admin Console** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-149">In hello Azure portal, on hello **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="cfdd3-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="cfdd3-153">In hello **Mimecast Admin Console dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfdd3-153">On hello **Mimecast Admin Console Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="cfdd3-155">In hello **Sign-on URL** casella di testo, digitare l'URL hello:</span><span class="sxs-lookup"><span data-stu-id="cfdd3-155">In hello **Sign-on URL** textbox, type hello URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="cfdd3-156">URL di accesso Hello è specifico dell'area.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-156">hello sign on URL is region specific.</span></span>

4. <span data-ttu-id="cfdd3-157">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="cfdd3-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cfdd3-159">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cfdd3-161">In hello **Mimecast Admin Console configurazione** fare clic su **configurare Mimecast Admin Console** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-161">On hello **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cfdd3-162">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="cfdd3-162">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="cfdd3-164">In un'altra finestra del Web browser accedere a Mimecast Admin Console come amministratore.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="cfdd3-165">Andare troppo**servizi \> applicazione**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-165">Go too**Services \> Application**.</span></span>

    <span data-ttu-id="cfdd3-166">![Servizi](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Servizi")</span><span class="sxs-lookup"><span data-stu-id="cfdd3-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="cfdd3-167">Fare clic su **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="cfdd3-168">![Profili di autenticazione](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Profili di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="cfdd3-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="cfdd3-169">Fare clic su **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="cfdd3-170">![Nuovi profili di autenticazione](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Nuovi profili di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="cfdd3-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="cfdd3-171">In hello **Authentication Profile** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfdd3-171">In hello **Authentication Profile** section, perform hello following steps:</span></span>

    <span data-ttu-id="cfdd3-172">![Profilo di autenticazione](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Profilo di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="cfdd3-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="cfdd3-173">a.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-173">a.</span></span> <span data-ttu-id="cfdd3-174">In hello **descrizione** casella di testo, digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-174">In hello **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="cfdd3-175">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-175">b.</span></span> <span data-ttu-id="cfdd3-176">Selezionare **Enforce SAML Authentication for Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="cfdd3-177">c.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-177">c.</span></span> <span data-ttu-id="cfdd3-178">Come **Provider** selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="cfdd3-179">d.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-179">d.</span></span> <span data-ttu-id="cfdd3-180">Incolla **ID entità SAML**, che è stato copiato dal portale di Azure hello in hello **URL autorità di certificazione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-180">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="cfdd3-181">e.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-181">e.</span></span> <span data-ttu-id="cfdd3-182">Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure hello in hello **URL di accesso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-182">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Login URL** textbox.</span></span>

    <span data-ttu-id="cfdd3-183">f.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-183">f.</span></span> <span data-ttu-id="cfdd3-184">Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure hello in hello **Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-184">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="cfdd3-185">Hello URL di accesso e valore hello Logout URL sono per hello Mimecast Admin Console hello stesso.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-185">hello Login URL value and hello Logout URL value are for hello Mimecast Admin Console hello same.</span></span>
    
    <span data-ttu-id="cfdd3-186">g.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-186">g.</span></span> <span data-ttu-id="cfdd3-187">Aprire il certificato in base 64 scaricato dal portale di Azure nel blocco note, rimuovere prima riga hello ("*--*") e l'ultima riga hello ("*--*"), hello copia rimanente contenuto di esso negli Appunti e quindi incollarlo toohello **Identity Provider Certificate (Metadata)** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove hello first line (“*--*“) and hello last line (“*--*“), copy hello remaining content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="cfdd3-188">h.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-188">h.</span></span> <span data-ttu-id="cfdd3-189">Selezionare **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="cfdd3-190">i.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-190">i.</span></span> <span data-ttu-id="cfdd3-191">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cfdd3-192">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="cfdd3-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cfdd3-193">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cfdd3-194">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cfdd3-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cfdd3-195">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfdd3-195">Create an Azure AD test user</span></span>

<span data-ttu-id="cfdd3-196">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="cfdd3-198">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfdd3-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfdd3-199">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-199">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cfdd3-201">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-201">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cfdd3-203">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-203">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cfdd3-205">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfdd3-205">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cfdd3-207">a.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-207">a.</span></span> <span data-ttu-id="cfdd3-208">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cfdd3-209">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-209">b.</span></span> <span data-ttu-id="cfdd3-210">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-210">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="cfdd3-211">c.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-211">c.</span></span> <span data-ttu-id="cfdd3-212">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-212">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="cfdd3-213">d.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-213">d.</span></span> <span data-ttu-id="cfdd3-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="cfdd3-215">Creare un utente test di Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="cfdd3-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="cfdd3-216">In ordine tooenable Azure AD utenti toolog in Mimecast Admin Console, è necessario eseguirne il provisioning in Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-216">In order tooenable Azure AD users toolog into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="cfdd3-217">Nel caso di hello di Mimecast Admin Console, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-217">In hello case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="cfdd3-218">Prima di poter creare utenti, è necessario tooregister un dominio.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-218">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="cfdd3-219">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfdd3-219">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfdd3-220">Accesso tooyour **Mimecast Admin Console** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-220">Sign on tooyour **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="cfdd3-221">Andare troppo**directory \> interno**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-221">Go too**Directories \> Internal**.</span></span>
   
   <span data-ttu-id="cfdd3-222">![Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directory")</span><span class="sxs-lookup"><span data-stu-id="cfdd3-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="cfdd3-223">Fare clic su **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="cfdd3-224">![Registra nuovo dominio](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Registra nuovo dominio")</span><span class="sxs-lookup"><span data-stu-id="cfdd3-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="cfdd3-225">Dopo aver creato il nuovo dominio, fare clic su **New Address**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="cfdd3-226">![Nuovo indirizzo](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "Nuovo indirizzo")</span><span class="sxs-lookup"><span data-stu-id="cfdd3-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="cfdd3-227">In hello indirizzo finestra di dialogo Nuovo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfdd3-227">In hello new address dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="cfdd3-228">![Salvare](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Salvare")</span><span class="sxs-lookup"><span data-stu-id="cfdd3-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="cfdd3-229">a.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-229">a.</span></span> <span data-ttu-id="cfdd3-230">Hello tipo **indirizzo di posta elettronica**, **nome globale**, **Password**, e **Conferma Password** gli attributi di un annuncio di Azure valido account si vuole tooprovision in hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-230">Type hello **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>

   <span data-ttu-id="cfdd3-231">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-231">b.</span></span> <span data-ttu-id="cfdd3-232">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="cfdd3-233">È possibile utilizzare qualsiasi altro strumento di creazione di account utente Mimecast Admin Console o le API fornite da account utente di Azure AD tooprovision Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console tooprovision Azure AD user accounts.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="cfdd3-234">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfdd3-234">Assign hello Azure AD test user</span></span>

<span data-ttu-id="cfdd3-235">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooMimecast Console di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Admin Console.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="cfdd3-237">**tooassign Britta Simon tooMimecast Console di amministrazione, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfdd3-237">**tooassign Britta Simon tooMimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfdd3-238">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cfdd3-240">Nell'elenco di applicazioni hello, selezionare **Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-240">In hello applications list, select **Mimecast Admin Console**.</span></span>

    ![collegamento di Mimecast Admin Console Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="cfdd3-242">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="cfdd3-244">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-244">Click **Add** button.</span></span> <span data-ttu-id="cfdd3-245">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="cfdd3-247">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cfdd3-248">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cfdd3-249">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cfdd3-250">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cfdd3-250">Test single sign-on</span></span>

<span data-ttu-id="cfdd3-251">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cfdd3-252">Quando si fa clic su riquadro Mimecast Admin Console hello in hello Pannello di accesso, è necessario ottenere applicazione Mimecast Admin Console tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="cfdd3-252">When you click hello Mimecast Admin Console tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Admin Console application.</span></span>
<span data-ttu-id="cfdd3-253">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cfdd3-253">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cfdd3-254">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cfdd3-254">Additional resources</span></span>

* [<span data-ttu-id="cfdd3-255">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfdd3-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cfdd3-256">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfdd3-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

