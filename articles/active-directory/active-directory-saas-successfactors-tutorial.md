---
title: 'Esercitazione: Integrazione di Azure Active Directory con SuccessFactors | Microsoft Docs'
description: Informazioni su come toouse SuccessFactors con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="30118-103">Esercitazione: Integrazione di Azure Active Directory con SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="30118-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="30118-104">obiettivo di Hello di questa esercitazione è tooshow è come toointegrate SuccessFactors con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30118-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30118-105">Integrazione di SuccessFactors con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="30118-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="30118-106">È possibile controllare in Azure AD che ha accesso tooSuccessFactors</span><span class="sxs-lookup"><span data-stu-id="30118-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="30118-107">È possibile abilitare l'utenti tooautomatically get connesso tooSuccessFactors (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="30118-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="30118-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="30118-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="30118-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="30118-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30118-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="30118-110">Prerequisites</span></span>
<span data-ttu-id="30118-111">integrazione di Azure AD con SuccessFactors tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="30118-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="30118-112">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="30118-112">A valid Azure subscription</span></span>
* <span data-ttu-id="30118-113">Un tenant in SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="30118-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="30118-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="30118-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="30118-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="30118-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="30118-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="30118-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="30118-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30118-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30118-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="30118-118">Scenario description</span></span>
<span data-ttu-id="30118-119">obiettivo di Hello di questa esercitazione è tooenable si tootest AD Azure single sign-on in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="30118-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="30118-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="30118-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30118-121">Aggiunta di SuccessFactors dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="30118-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="30118-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30118-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="30118-123">Aggiunta di SuccessFactors dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="30118-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="30118-124">integrazione hello tooconfigure di SuccessFactors in Azure AD, è necessario tooadd SuccessFactors dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="30118-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="30118-125">**tooadd SuccessFactors dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="30118-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="30118-126">Nel portale di Azure classico, nel riquadro di navigazione sinistro hello hello fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30118-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][1]
2. <span data-ttu-id="30118-128">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="30118-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="30118-129">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="30118-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][2]
4. <span data-ttu-id="30118-131">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="30118-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applicazioni][3]
5. <span data-ttu-id="30118-133">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="30118-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][4]
6. <span data-ttu-id="30118-135">In hello **casella di ricerca**, tipo **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="30118-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][5]
7. <span data-ttu-id="30118-137">Nel riquadro dei risultati hello, selezionare **SuccessFactors**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="30118-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="30118-139">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30118-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="30118-140">obiettivo di Hello di questa sezione è tooshow come tooconfigure e prova AD Azure single sign-on con SuccessFactors basato su un utente di test denominato "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="30118-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="30118-141">Per toowork di accesso singolo, Azure AD deve tooknow è quale utente controparte hello in SuccessFactors tooan utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30118-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="30118-142">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SuccessFactors deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="30118-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="30118-143">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="30118-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="30118-144">tooconfigure e prova AD Azure single sign-on con SuccessFactors, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="30118-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="30118-145">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="30118-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="30118-146">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30118-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30118-147">**[Creazione di un utente test SuccessFactors](#creating-a-successfactors-test-user)**  -toohave un equivalente di Britta Simon in SuccessFactors toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="30118-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="30118-148">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="30118-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30118-149">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="30118-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="30118-150">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30118-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="30118-151">In questa sezione, si abilita Azure AD single sign-on nel portale classico hello e configurare l'accesso single sign-on nell'applicazione SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="30118-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="30118-152">**Azure AD tooconfigure single sign-on con SuccessFactors, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="30118-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="30118-153">Nel portale di Azure classico, in hello hello **SuccessFactors** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="30118-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][7]
2. <span data-ttu-id="30118-155">In hello **come si sarebbe ad esempio utenti toosign su tooSuccessFactors** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="30118-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][8]
3. <span data-ttu-id="30118-157">In hello **Configura URL App** pagina, eseguire hello alla procedura seguente e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="30118-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][9]
   
    <span data-ttu-id="30118-159">a.</span><span class="sxs-lookup"><span data-stu-id="30118-159">a.</span></span> <span data-ttu-id="30118-160">In hello **URL di accesso** casella di testo, digitare un URL utilizzando uno dei hello seguenti motivi:</span><span class="sxs-lookup"><span data-stu-id="30118-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="30118-161">b.</span><span class="sxs-lookup"><span data-stu-id="30118-161">b.</span></span> <span data-ttu-id="30118-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando uno dei hello seguenti motivi:</span><span class="sxs-lookup"><span data-stu-id="30118-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="30118-163">c.</span><span class="sxs-lookup"><span data-stu-id="30118-163">c.</span></span> <span data-ttu-id="30118-164">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="30118-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="30118-165">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="30118-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="30118-166">È necessario tooupdate questi valori con hello URL di URL di accesso e di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="30118-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="30118-167">Questi valori, contattare il tooget [team di supporto di SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="30118-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="30118-168">In hello **Configura accesso single sign-on in SuccessFactors** pagina, fare clic su **Scarica certificato**e quindi salvare il file di certificato hello in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="30118-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][10]

2. <span data-ttu-id="30118-170">In un'altra finestra del Web browser accedere al **portale di amministrazione di SuccessFactors** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="30118-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="30118-171">Visitare **sicurezza delle applicazioni** e native troppo**funzione accesso singolo**.</span><span class="sxs-lookup"><span data-stu-id="30118-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="30118-172">Inserire un valore in hello **Reimposta Token** e fare clic su **salvare Token** tooenable SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="30118-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On sul lato app][11]

    > [!NOTE] 
    > <span data-ttu-id="30118-174">Questo valore viene utilizzato solo come hello opzione on/off.</span><span class="sxs-lookup"><span data-stu-id="30118-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="30118-175">Se qualsiasi valore viene salvato, hello SAML SSO è impostata su ON.</span><span class="sxs-lookup"><span data-stu-id="30118-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="30118-176">Se un valore vuoto viene salvato hello SAML SSO è impostata su OFF.</span><span class="sxs-lookup"><span data-stu-id="30118-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="30118-177">Schermata di toobelow native ed eseguire hello seguenti azioni.</span><span class="sxs-lookup"><span data-stu-id="30118-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On sul lato app][12]
   
    <span data-ttu-id="30118-179">a.</span><span class="sxs-lookup"><span data-stu-id="30118-179">a.</span></span> <span data-ttu-id="30118-180">Seleziona hello **SAML SSO v2** pulsante di opzione</span><span class="sxs-lookup"><span data-stu-id="30118-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="30118-181">b.</span><span class="sxs-lookup"><span data-stu-id="30118-181">b.</span></span> <span data-ttu-id="30118-182">Impostare hello SAML asserzione entità Name(e.g. SAml issuer + company name).</span><span class="sxs-lookup"><span data-stu-id="30118-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="30118-183">c.</span><span class="sxs-lookup"><span data-stu-id="30118-183">c.</span></span> <span data-ttu-id="30118-184">In hello **autorità di certificazione SAML** casella di testo inserire il valore di hello di **URL autorità di certificazione** dalla configurazione guidata di Azure AD applicazione.</span><span class="sxs-lookup"><span data-stu-id="30118-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="30118-185">d.</span><span class="sxs-lookup"><span data-stu-id="30118-185">d.</span></span> <span data-ttu-id="30118-186">Selezionare **Response(Customer Generated/IdP/AP)** (Risposta - Generata da cliente/IdP/AP) per **Require Mandatory Signature** (Richiedi firma obbligatoria).</span><span class="sxs-lookup"><span data-stu-id="30118-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="30118-187">e.</span><span class="sxs-lookup"><span data-stu-id="30118-187">e.</span></span> <span data-ttu-id="30118-188">Selezionare **Abilitato** per **Enable SAML Flag** (Abilita flag SAML).</span><span class="sxs-lookup"><span data-stu-id="30118-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="30118-189">f.</span><span class="sxs-lookup"><span data-stu-id="30118-189">f.</span></span> <span data-ttu-id="30118-190">Selezionare **No** per **Login Request Signature(SF Generated/SP/RP)** (Firma richiesta di accesso - Generata da SF/SP/RP).</span><span class="sxs-lookup"><span data-stu-id="30118-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="30118-191">g.</span><span class="sxs-lookup"><span data-stu-id="30118-191">g.</span></span> <span data-ttu-id="30118-192">Selezionare **Browser/Post Profile** (Profilo browser/post) per **SAML Profile** (Profilo SAML).</span><span class="sxs-lookup"><span data-stu-id="30118-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="30118-193">h.</span><span class="sxs-lookup"><span data-stu-id="30118-193">h.</span></span> <span data-ttu-id="30118-194">Selezionare **No** per **Enforce Certificate Valid Period** (Applicare periodo di validità certificato).</span><span class="sxs-lookup"><span data-stu-id="30118-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="30118-195">i.</span><span class="sxs-lookup"><span data-stu-id="30118-195">i.</span></span> <span data-ttu-id="30118-196">Copiare il contenuto di hello hello scaricato del file di certificato e quindi incollarlo hello **certificato di verifica SAML** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="30118-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="30118-197">contenuto del certificato Hello devono avere certificato e fine certificato i tag di inizio.</span><span class="sxs-lookup"><span data-stu-id="30118-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="30118-198">Passare tooSAML V2 e quindi eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="30118-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![Configurazione dell'accesso Single Sign-On sul lato app][13]
   
    <span data-ttu-id="30118-200">a.</span><span class="sxs-lookup"><span data-stu-id="30118-200">a.</span></span> <span data-ttu-id="30118-201">Selezionare **Sì** per **Support SP-initiated Global Logout** (Supporto disconnessione globale avviata da SP).</span><span class="sxs-lookup"><span data-stu-id="30118-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="30118-202">b.</span><span class="sxs-lookup"><span data-stu-id="30118-202">b.</span></span> <span data-ttu-id="30118-203">In hello **globale Logout URL del servizio (destinazione LogoutRequest)** casella di testo inserire il valore di hello di **URL disconnessione remota** dalla configurazione guidata di Azure AD applicazione.</span><span class="sxs-lookup"><span data-stu-id="30118-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="30118-204">c.</span><span class="sxs-lookup"><span data-stu-id="30118-204">c.</span></span> <span data-ttu-id="30118-205">Selezionare **No** per **Require sp must encrypt all NameID element** (Richiesta a sp di crittografare tutti gli elementi NameID).</span><span class="sxs-lookup"><span data-stu-id="30118-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="30118-206">d.</span><span class="sxs-lookup"><span data-stu-id="30118-206">d.</span></span> <span data-ttu-id="30118-207">Selezionare **non specificato** per **NameID Format** (Formato NameID).</span><span class="sxs-lookup"><span data-stu-id="30118-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="30118-208">e.</span><span class="sxs-lookup"><span data-stu-id="30118-208">e.</span></span> <span data-ttu-id="30118-209">Selezionare **Sì** per **Enable sp initiated login (AuthnRequest)** (Abilita accesso avviato da sp - AuthnRequest).</span><span class="sxs-lookup"><span data-stu-id="30118-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="30118-210">f.</span><span class="sxs-lookup"><span data-stu-id="30118-210">f.</span></span> <span data-ttu-id="30118-211">In hello **richiesta di invio da autorità di certificazione aziendale** casella di testo inserire il valore di hello di **URL accesso remoto** dalla configurazione guidata di Azure AD applicazione.</span><span class="sxs-lookup"><span data-stu-id="30118-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="30118-212">Eseguire questi passaggi se si desidera che i nomi utente di accesso hello toomake maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="30118-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="30118-213">a.</span><span class="sxs-lookup"><span data-stu-id="30118-213">a.</span></span> <span data-ttu-id="30118-214">Visitare **impostazioni società**(vicino alla parte inferiore di hello).</span><span class="sxs-lookup"><span data-stu-id="30118-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="30118-215">b.</span><span class="sxs-lookup"><span data-stu-id="30118-215">b.</span></span> <span data-ttu-id="30118-216">Selezionare la casella di controllo accanto alla **Enable Non-Case-Sensitive Username**(Abilita nome utente senza distinzione maiuscole/minuscole).</span><span class="sxs-lookup"><span data-stu-id="30118-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="30118-217">c.Fare clic su **Save**(Salva).</span><span class="sxs-lookup"><span data-stu-id="30118-217">c.Click **Save**.</span></span>
   
    ![Configura accesso Single Sign-On][29]

    > [!NOTE] 
    > <span data-ttu-id="30118-219">Se si esegue questa tooenable, sistema di hello controlla se verrà creato automaticamente un nome di account di accesso SAML duplicato.</span><span class="sxs-lookup"><span data-stu-id="30118-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="30118-220">Se, ad esempio hello cliente dispone di nomi utente User1 e user1.</span><span class="sxs-lookup"><span data-stu-id="30118-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="30118-221">L'annullamento della distinzione maiuscole/minuscole crea questi duplicati.</span><span class="sxs-lookup"><span data-stu-id="30118-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="30118-222">sistema di Hello verrà visualizzato un messaggio di errore e non viene abilitata la funzionalità di hello.</span><span class="sxs-lookup"><span data-stu-id="30118-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="30118-223">Hello il cliente dovrà toochange uno dei nomi utente hello in modo sia stato digitato in realtà diversi.</span><span class="sxs-lookup"><span data-stu-id="30118-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="30118-224">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="30118-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![Applicazioni][14]
2. <span data-ttu-id="30118-226">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="30118-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Applicazioni][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="30118-228">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="30118-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="30118-229">obiettivo di Hello di questa sezione è toocreate un utente di test nel portale classico di hello chiamato Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30118-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][16]

<span data-ttu-id="30118-231">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="30118-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="30118-232">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30118-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD][17]
2. <span data-ttu-id="30118-234">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="30118-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="30118-235">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="30118-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD][18]
4. <span data-ttu-id="30118-237">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="30118-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Creazione di un utente test di Azure AD][19]
5. <span data-ttu-id="30118-239">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="30118-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD][20]
   
    <span data-ttu-id="30118-241">a.</span><span class="sxs-lookup"><span data-stu-id="30118-241">a.</span></span> <span data-ttu-id="30118-242">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="30118-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="30118-243">b.</span><span class="sxs-lookup"><span data-stu-id="30118-243">b.</span></span> <span data-ttu-id="30118-244">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30118-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="30118-245">c.</span><span class="sxs-lookup"><span data-stu-id="30118-245">c.</span></span> <span data-ttu-id="30118-246">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="30118-246">Click **Next**.</span></span>
6. <span data-ttu-id="30118-247">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="30118-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD][21]
   
    <span data-ttu-id="30118-249">a.</span><span class="sxs-lookup"><span data-stu-id="30118-249">a.</span></span> <span data-ttu-id="30118-250">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="30118-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="30118-251">b.</span><span class="sxs-lookup"><span data-stu-id="30118-251">b.</span></span> <span data-ttu-id="30118-252">In hello **cognome** casella di testo, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="30118-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="30118-253">c.</span><span class="sxs-lookup"><span data-stu-id="30118-253">c.</span></span> <span data-ttu-id="30118-254">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="30118-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="30118-255">d.</span><span class="sxs-lookup"><span data-stu-id="30118-255">d.</span></span> <span data-ttu-id="30118-256">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="30118-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="30118-257">e.</span><span class="sxs-lookup"><span data-stu-id="30118-257">e.</span></span> <span data-ttu-id="30118-258">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="30118-258">Click **Next**.</span></span>
7. <span data-ttu-id="30118-259">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="30118-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD][22]
8. <span data-ttu-id="30118-261">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="30118-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD][23]
   
    <span data-ttu-id="30118-263">a.</span><span class="sxs-lookup"><span data-stu-id="30118-263">a.</span></span> <span data-ttu-id="30118-264">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="30118-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="30118-265">b.</span><span class="sxs-lookup"><span data-stu-id="30118-265">b.</span></span> <span data-ttu-id="30118-266">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="30118-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="30118-267">Creazione di un utente test SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="30118-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="30118-268">In ordine tooenable Azure AD utenti toolog in SuccessFactors, è necessario eseguirne il provisioning in SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="30118-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="30118-269">Nel caso di hello di SuccessFactors, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="30118-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="30118-270">tooget degli utenti creati in SuccessFactors, è necessario hello toocontact [team di supporto di SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="30118-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="30118-271">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="30118-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="30118-272">obiettivo di Hello di questa sezione è tooenabling toouse Britta Simon single sign-on Azure concedendo tooSuccessFactors proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="30118-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![Assegna utente][24]

<span data-ttu-id="30118-274">**tooassign Britta Simon tooSuccessFactors, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="30118-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="30118-275">Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="30118-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Assegna utente][25]
2. <span data-ttu-id="30118-277">Nell'elenco di applicazioni hello, selezionare **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="30118-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![Configura accesso Single Sign-On][26]
3. <span data-ttu-id="30118-279">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="30118-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![Assegna utente][27]
4. <span data-ttu-id="30118-281">Nell'elenco di utenti hello, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="30118-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="30118-282">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="30118-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Assegna utente][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="30118-284">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="30118-284">Testing single sign-on</span></span>
<span data-ttu-id="30118-285">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="30118-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="30118-286">Quando si fa clic hello SuccessFactors riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="30118-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30118-287">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="30118-287">Additional resources</span></span>
* [<span data-ttu-id="30118-288">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30118-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30118-289">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30118-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
