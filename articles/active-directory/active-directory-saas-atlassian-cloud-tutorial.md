---
title: 'Esercitazione: Integrazione di Azure Active Directory con Atlassian Cloud | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e il Atlassian Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="b17d4-103">Esercitazione: Integrazione di Azure Active Directory con Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="b17d4-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="b17d4-104">In questa esercitazione, è illustrato come toointegrate Atlassian Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b17d4-104">In this tutorial, you learn how toointegrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b17d4-105">Integrazione di Atlassian Cloud con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b17d4-105">Integrating Atlassian Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b17d4-106">È possibile controllare in Azure AD che ha accesso tooAtlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="b17d4-106">You can control in Azure AD who has access tooAtlassian Cloud</span></span>
- <span data-ttu-id="b17d4-107">È possibile abilitare l'utenti tooautomatically get connesso tooAtlassian Cloud (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b17d4-107">You can enable your users tooautomatically get signed-on tooAtlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b17d4-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b17d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b17d4-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b17d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b17d4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b17d4-110">Prerequisites</span></span>

<span data-ttu-id="b17d4-111">integrazione di Azure AD con Atlassian Cloud tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b17d4-111">tooconfigure Azure AD integration with Atlassian Cloud, you need hello following items:</span></span>

- <span data-ttu-id="b17d4-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b17d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b17d4-113">Sottoscrizione di Atlassian Cloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b17d4-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b17d4-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b17d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b17d4-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="b17d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b17d4-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b17d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b17d4-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b17d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b17d4-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b17d4-118">Scenario description</span></span>
<span data-ttu-id="b17d4-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b17d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b17d4-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="b17d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b17d4-121">Aggiunta di Atlassian Cloud dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b17d4-121">Adding Atlassian Cloud from hello gallery</span></span>
2. <span data-ttu-id="b17d4-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b17d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-hello-gallery"></a><span data-ttu-id="b17d4-123">Aggiunta di Atlassian Cloud dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b17d4-123">Adding Atlassian Cloud from hello gallery</span></span>
<span data-ttu-id="b17d4-124">integrazione hello tooconfigure di Atlassian Cloud in Azure AD, è necessario tooadd Atlassian Cloud dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b17d4-124">tooconfigure hello integration of Atlassian Cloud into Azure AD, you need tooadd Atlassian Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b17d4-125">**tooadd Atlassian Cloud dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b17d4-125">**tooadd Atlassian Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b17d4-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b17d4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b17d4-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b17d4-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b17d4-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b17d4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b17d4-133">Nella casella di ricerca hello, digitare **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-133">In hello search box, type **Atlassian Cloud**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="b17d4-135">Nel riquadro dei risultati hello, selezionare **Atlassian Cloud**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b17d4-135">In hello results panel, select **Atlassian Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b17d4-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b17d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b17d4-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Atlassian Cloud con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b17d4-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b17d4-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nel Atlassian Cloud è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b17d4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atlassian Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="b17d4-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nel Atlassian Cloud deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="b17d4-140">In other words, a link relationship between an Azure AD user and hello related user in Atlassian Cloud needs toobe established.</span></span>

<span data-ttu-id="b17d4-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nel Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="b17d4-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="b17d4-142">tooconfigure e test Azure single sign-on AD Atlassian cloud, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="b17d4-142">tooconfigure and test Azure AD single sign-on with Atlassian Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b17d4-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b17d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b17d4-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b17d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b17d4-145">**[Creazione di un utente test Atlassian Cloud](#creating-an-atlassian-cloud-test-user)**  -toohave un equivalente di Britta Simon in Atlassian Cloud toohello collegato AD Azure rappresentazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b17d4-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - toohave a counterpart of Britta Simon in Atlassian Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b17d4-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b17d4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b17d4-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="b17d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b17d4-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b17d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b17d4-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="b17d4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="b17d4-150">**Azure AD tooconfigure single sign-on con Atlassian Cloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b17d4-150">**tooconfigure Azure AD single sign-on with Atlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="b17d4-151">Nel portale di Azure su hello hello **Atlassian Cloud** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-151">In hello Azure portal, on hello **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b17d4-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b17d4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="b17d4-155">In hello **Atlassian Cloud dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="b17d4-155">On hello **Atlassian Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="b17d4-157">a.</span><span class="sxs-lookup"><span data-stu-id="b17d4-157">a.</span></span> <span data-ttu-id="b17d4-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="b17d4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="b17d4-159">b.</span><span class="sxs-lookup"><span data-stu-id="b17d4-159">b.</span></span> <span data-ttu-id="b17d4-160">In hello **URL di risposta** casella di testo, digitare un URL come:`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="b17d4-160">In hello **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="b17d4-161">Controllare **Mostra URL impostazioni avanzate** ed eseguire hello riportata dopo il passaggio se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="b17d4-161">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="b17d4-163">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="b17d4-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b17d4-164">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b17d4-164">These values are not real.</span></span> <span data-ttu-id="b17d4-165">Aggiornare questi valori con hello effettivo identificatore e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b17d4-165">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="b17d4-166">È possibile ottenere i valori esatti hello dalla schermata di configurazione SAML del Cloud Atlassian.</span><span class="sxs-lookup"><span data-stu-id="b17d4-166">You can get hello exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="b17d4-167">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b17d4-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="b17d4-169">In hello **configurazione Cloud Atlassian** fare clic su **configurare Atlassian Cloud** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="b17d4-169">On hello **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b17d4-170">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b17d4-170">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="b17d4-172">tooget SSO configurato per l'applicazione, account di accesso toohello Atlassian portale usando i diritti di amministratore hello.</span><span class="sxs-lookup"><span data-stu-id="b17d4-172">tooget SSO configured for your application, login toohello Atlassian Portal using hello administrator rights.</span></span>

8. <span data-ttu-id="b17d4-173">Nella sezione autenticazione hello di hello riquadro di spostamento sinistro fare clic su **domini**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-173">In hello Authentication section of hello left navigation click **Domains**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="b17d4-175">a.</span><span class="sxs-lookup"><span data-stu-id="b17d4-175">a.</span></span> <span data-ttu-id="b17d4-176">Nella casella di testo hello, digitare il nome di dominio e quindi fare clic su **Aggiungi dominio**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-176">In hello textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="b17d4-178">b.</span><span class="sxs-lookup"><span data-stu-id="b17d4-178">b.</span></span> <span data-ttu-id="b17d4-179">dominio hello tooverify, fare clic su **verificare**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-179">tooverify hello domain, click **Verify**.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="b17d4-181">c.</span><span class="sxs-lookup"><span data-stu-id="b17d4-181">c.</span></span> <span data-ttu-id="b17d4-182">Download di file html di verifica dominio hello, caricarlo toohello di cartella radice del sito Web del proprio dominio e quindi fare clic su **verifica dominio**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-182">Download hello domain verification html file, upload it toohello root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="b17d4-184">d.</span><span class="sxs-lookup"><span data-stu-id="b17d4-184">d.</span></span> <span data-ttu-id="b17d4-185">Una volta verificato il dominio di hello, hello valore hello **stato** campo **verificato**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-185">Once hello domain is verified, hello value of hello **Status** field is **Verified**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="b17d4-187">Nella barra di spostamento sinistra hello, fare clic su **SAML**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-187">In hello left navigation bar, click **SAML**.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="b17d4-189">Creare una configurazione di SAML e aggiungere una configurazione del provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="b17d4-189">Create a SAML Configuration and add hello Identity provider configuration.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="b17d4-191">a.</span><span class="sxs-lookup"><span data-stu-id="b17d4-191">a.</span></span> <span data-ttu-id="b17d4-192">In hello **provider di identità, ID entità** Incolla hello valore della casella di testo **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b17d4-192">In hello **Identity provider Entity ID** text box, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b17d4-193">b.</span><span class="sxs-lookup"><span data-stu-id="b17d4-193">b.</span></span> <span data-ttu-id="b17d4-194">In hello **Identity provider URL SSO** Incolla hello valore della casella di testo **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b17d4-194">In hello **Identity provider SSO URL** text box, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b17d4-195">c.</span><span class="sxs-lookup"><span data-stu-id="b17d4-195">c.</span></span> <span data-ttu-id="b17d4-196">Aprire il certificato di hello scaricato da Azure portal e copia hello valori senza hello inizio e fine delle linee e incollarlo in hello **X509 pubblico certificato** casella.</span><span class="sxs-lookup"><span data-stu-id="b17d4-196">Open hello downloaded certificate from Azure portal and copy hello values without hello Begin and End lines and paste it in hello **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="b17d4-197">d.</span><span class="sxs-lookup"><span data-stu-id="b17d4-197">d.</span></span> <span data-ttu-id="b17d4-198">Fare clic su **Salva la configurazione** impostazioni hello tooSave.</span><span class="sxs-lookup"><span data-stu-id="b17d4-198">Click **Save Configuration**  tooSave hello settings.</span></span>
     
11. <span data-ttu-id="b17d4-199">Aggiornare hello toomake le impostazioni di Azure AD che abbiano hello il programma di installazione di correggere l'URL dell'identificatore.</span><span class="sxs-lookup"><span data-stu-id="b17d4-199">Update hello Azure AD settings toomake sure that you have setup hello correct Identifier URL.</span></span>
  
    <span data-ttu-id="b17d4-200">a.</span><span class="sxs-lookup"><span data-stu-id="b17d4-200">a.</span></span> <span data-ttu-id="b17d4-201">Hello copia **ID identità SP** dalla hello SAML schermata e incollarlo in Azure AD come hello **identificatore** valore.</span><span class="sxs-lookup"><span data-stu-id="b17d4-201">Copy hello **SP Identity ID** from hello SAML screen and paste it in Azure AD as hello **Identifier** value.</span></span>

    <span data-ttu-id="b17d4-202">b.</span><span class="sxs-lookup"><span data-stu-id="b17d4-202">b.</span></span> <span data-ttu-id="b17d4-203">URL di accesso è l'URL del tenant del Atlassian Cloud hello.</span><span class="sxs-lookup"><span data-stu-id="b17d4-203">Sign On URL is hello tenant URL of your Atlassian Cloud.</span></span>     

     ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="b17d4-205">Nel portale di Azure hello, fare clic su **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="b17d4-205">In hello Azure portal, Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="b17d4-207">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="b17d4-207">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b17d4-208">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b17d4-208">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b17d4-209">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b17d4-209">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b17d4-210">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b17d4-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="b17d4-211">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b17d4-211">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b17d4-213">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b17d4-213">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b17d4-214">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b17d4-214">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b17d4-216">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-216">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b17d4-218">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="b17d4-218">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b17d4-220">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b17d4-220">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b17d4-222">a.</span><span class="sxs-lookup"><span data-stu-id="b17d4-222">a.</span></span> <span data-ttu-id="b17d4-223">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-223">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b17d4-224">b.</span><span class="sxs-lookup"><span data-stu-id="b17d4-224">b.</span></span> <span data-ttu-id="b17d4-225">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b17d4-225">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b17d4-226">c.</span><span class="sxs-lookup"><span data-stu-id="b17d4-226">c.</span></span> <span data-ttu-id="b17d4-227">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-227">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b17d4-228">d.</span><span class="sxs-lookup"><span data-stu-id="b17d4-228">d.</span></span> <span data-ttu-id="b17d4-229">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="b17d4-230">Creazione di un utente di test di Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="b17d4-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="b17d4-231">toolog agli utenti di Azure AD tooenable in tooAtlassian Cloud, è necessario eseguirne il provisioning in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="b17d4-231">tooenable Azure AD users toolog in tooAtlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="b17d4-232">Nel caso di Atlassian Cloud il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="b17d4-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="b17d4-233">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b17d4-233">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b17d4-234">Nella sezione Amministrazione sito hello, fare clic su hello **utenti** pulsante</span><span class="sxs-lookup"><span data-stu-id="b17d4-234">In hello Site administration section, click hello **Users** button</span></span>

    ![Creare l'utente di Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="b17d4-236">Fare clic su hello **Create User** pulsante toocreate un utente nel Atlassian Cloud hello</span><span class="sxs-lookup"><span data-stu-id="b17d4-236">Click hello **Create User** button toocreate a user in hello Atlassian Cloud</span></span>

    ![Creare l'utente di Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="b17d4-238">Immettere dell'utente hello **indirizzo di posta elettronica**, **Username**, e **nome completo** e assegnare l'accesso all'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b17d4-238">Enter hello user's **Email address**, **Username**, and **Full Name** and assign hello application access.</span></span> 

    ![Creare l'utente di Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="b17d4-240">Fare clic su **Create user** pulsante, questo invierà utente toohello invito tramite posta elettronica di hello e dopo aver accettato utente hello di invito hello saranno attivi nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="b17d4-240">Click **Create user** button, it will send hello email invitation toohello user and after accepting hello invitation hello user will be active in hello system.</span></span> 

>[!NOTE] 
><span data-ttu-id="b17d4-241">È anche possibile creare hello bulk utenti facendo clic su hello **Bulk creare** pulsante nella sezione utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b17d4-241">You can also create hello bulk users by clicking hello **Bulk Create** button in hello Users section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b17d4-242">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b17d4-242">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b17d4-243">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAtlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="b17d4-243">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtlassian Cloud.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b17d4-245">**tooassign Britta Simon tooAtlassian Cloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b17d4-245">**tooassign Britta Simon tooAtlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="b17d4-246">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-246">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b17d4-248">Nell'elenco di applicazioni hello, selezionare **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-248">In hello applications list, select **Atlassian Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="b17d4-250">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-250">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b17d4-252">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-252">Click **Add** button.</span></span> <span data-ttu-id="b17d4-253">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b17d4-255">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b17d4-255">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b17d4-256">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b17d4-257">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b17d4-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b17d4-258">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b17d4-258">Testing single sign-on</span></span>

<span data-ttu-id="b17d4-259">In questa sezione è verificare la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b17d4-259">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="b17d4-260">Quando si fa clic hello Atlassian Cloud riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="b17d4-260">When you click hello Atlassian Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Atlassian Cloud application.</span></span> <span data-ttu-id="b17d4-261">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b17d4-261">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b17d4-262">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b17d4-262">Additional resources</span></span>

* [<span data-ttu-id="b17d4-263">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b17d4-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b17d4-264">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b17d4-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

