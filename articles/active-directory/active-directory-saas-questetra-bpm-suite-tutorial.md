---
title: 'Esercitazione: Integrazione di Azure Active Directory con Questetra BPM Suite | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Questetra Business Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="e79ec-103">Esercitazione: Integrazione di Azure Active Directory con Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="e79ec-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="e79ec-104">obiettivo di Hello di questa esercitazione è tooshow è come toointegrate Questetra BPM Suite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e79ec-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="e79ec-105">Integrazione Questetra BPM Suite con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="e79ec-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="e79ec-106">È possibile controllare in Azure AD che ha accesso tooQuestetra Business Suite</span><span class="sxs-lookup"><span data-stu-id="e79ec-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="e79ec-107">È possibile abilitare l'utenti tooautomatically get connesso tooQuestetra Suite BPM (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="e79ec-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="e79ec-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="e79ec-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="e79ec-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e79ec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e79ec-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e79ec-110">Prerequisites</span></span>
<span data-ttu-id="e79ec-111">integrazione di Azure AD con Questetra BPM Suite tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="e79ec-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="e79ec-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e79ec-112">An Azure AD subscription</span></span>
* <span data-ttu-id="e79ec-113">Sottoscrizione di [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e79ec-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e79ec-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e79ec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="e79ec-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="e79ec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="e79ec-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e79ec-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="e79ec-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e79ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="e79ec-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e79ec-118">Scenario Description</span></span>
<span data-ttu-id="e79ec-119">obiettivo di Hello di questa esercitazione è tooenable si tootest AD Azure single sign-on in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e79ec-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="e79ec-120">scenario di Hello descritto in questa esercitazione è composto da tre componenti principali:</span><span class="sxs-lookup"><span data-stu-id="e79ec-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="e79ec-121">Aggiunta gruppo BPM Questetra dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e79ec-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="e79ec-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e79ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="e79ec-123">Aggiunta gruppo BPM Questetra dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e79ec-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="e79ec-124">integrazione hello tooconfigure di Questetra Business Suite in Azure AD, è necessario tooadd Questetra BPM gruppo dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e79ec-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e79ec-125">**tooadd Questetra BPM Suite dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e79ec-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e79ec-126">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="e79ec-128">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="e79ec-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="e79ec-129">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="e79ec-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applicazioni][2]

4. <span data-ttu-id="e79ec-131">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="e79ec-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applicazioni][3]

5. <span data-ttu-id="e79ec-133">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applicazioni][4]

6. <span data-ttu-id="e79ec-135">Nella casella di ricerca hello, digitare **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![Applicazioni][5]

7. <span data-ttu-id="e79ec-137">Nel riquadro risultati hello selezionare **Questetra BPM Suite**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e79ec-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e79ec-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e79ec-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e79ec-139">obiettivo di Hello di questa sezione è tooshow come tooconfigure e prova AD Azure single sign-on con Questetra BPM Suite basato su un utente di test denominato "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e79ec-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e79ec-140">Per toowork di accesso singolo, Azure AD deve tooknow è quale utente controparte hello utente tooan Questetra Business Suite in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e79ec-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="e79ec-141">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello Questetra Business Suite deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="e79ec-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="e79ec-142">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Questetra Business Suite.</span><span class="sxs-lookup"><span data-stu-id="e79ec-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="e79ec-143">tooconfigure e prova AD Azure single sign-on con Questetra Business Suite, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="e79ec-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e79ec-144">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e79ec-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e79ec-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e79ec-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e79ec-146">**[Creazione di un utente test Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  -toohave un equivalente di Britta Simon Questetra BPM Suite rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e79ec-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="e79ec-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e79ec-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e79ec-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="e79ec-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e79ec-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e79ec-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="e79ec-150">obiettivo di Hello di questa sezione è tooenable AD Azure single sign-on nel portale di Azure classico hello e tooconfigure single sign-on nell'applicazione Questetra Business Suite.</span><span class="sxs-lookup"><span data-stu-id="e79ec-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="e79ec-151">**tooconfigure AD Azure single sign-on con Questetra Business Suite, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e79ec-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="e79ec-152">Nel portale di Azure classico, in hello hello **Questetra BPM Suite** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**  finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e79ec-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][8]

2. <span data-ttu-id="e79ec-154">In hello **come si sarebbe ad esempio utenti toosign su tooQuestetra BPM Suite** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][9]

3. <span data-ttu-id="e79ec-156">In un'altra finestra del Web browser accedere al sito aziendale di **Questetra BPM Suite** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e79ec-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="e79ec-157">Scegliere dal menu hello in primo piano hello **le impostazioni di sistema**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][10]

5. <span data-ttu-id="e79ec-159">hello tooopen **SingleSignOnSAML** pagina, fare clic su **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][11]

6. <span data-ttu-id="e79ec-161">Nel portale di Azure classico, in hello hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e79ec-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Configurare le impostazioni dell'app][13]
   
    <span data-ttu-id="e79ec-163">a.</span><span class="sxs-lookup"><span data-stu-id="e79ec-163">a.</span></span> <span data-ttu-id="e79ec-164">In è **Questetra BPM Suite** hello sezione SP informazioni del sito della società, hello copia **URL ACS**e quindi incollarlo hello **URL di accesso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e79ec-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="e79ec-165">b.</span><span class="sxs-lookup"><span data-stu-id="e79ec-165">b.</span></span> <span data-ttu-id="e79ec-166">In è **Questetra BPM Suite** hello sezione SP informazioni del sito della società, hello copia **ID entità**e quindi incollarlo hello **URL autorità di certificazione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e79ec-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="e79ec-167">c.</span><span class="sxs-lookup"><span data-stu-id="e79ec-167">c.</span></span> <span data-ttu-id="e79ec-168">In è **Questetra BPM Suite** hello sezione SP informazioni del sito della società, hello copia **URL ACS**e quindi incollarlo hello **URL di risposta** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e79ec-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="e79ec-169">d.</span><span class="sxs-lookup"><span data-stu-id="e79ec-169">d.</span></span> <span data-ttu-id="e79ec-170">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-170">Click **Next**.</span></span>

7. <span data-ttu-id="e79ec-171">In hello **Configura accesso single sign-on Questetra BPM Suite** pagina, fare clic su **Scarica certificato**e quindi salvare il file di certificato hello in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="e79ec-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Configura accesso Single Sign-On][14]

8. <span data-ttu-id="e79ec-173">In è **Questetra BPM Suite** sito della società, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e79ec-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![Configura accesso Single Sign-On][15]
   
    <span data-ttu-id="e79ec-175">a.</span><span class="sxs-lookup"><span data-stu-id="e79ec-175">a.</span></span> <span data-ttu-id="e79ec-176">Selezionare **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="e79ec-177">b.</span><span class="sxs-lookup"><span data-stu-id="e79ec-177">b.</span></span> <span data-ttu-id="e79ec-178">Nel portale di Azure classico hello, copiare hello **URL autorità di certificazione** valore e quindi incollarlo hello **ID entità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e79ec-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="e79ec-179">c.</span><span class="sxs-lookup"><span data-stu-id="e79ec-179">c.</span></span> <span data-ttu-id="e79ec-180">Nel portale di Azure classico hello, copiare hello **URL servizio Single Sign-On** valore e quindi incollarlo hello **accesso URL della pagina** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e79ec-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="e79ec-181">d.</span><span class="sxs-lookup"><span data-stu-id="e79ec-181">d.</span></span> <span data-ttu-id="e79ec-182">Nel portale di Azure classico hello, copiare hello **URL del servizio Single Sign-Out** valore e quindi incollarlo hello **URL pagina di disconnessione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e79ec-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="e79ec-183">e.</span><span class="sxs-lookup"><span data-stu-id="e79ec-183">e.</span></span> <span data-ttu-id="e79ec-184">In hello **NameID format** casella tipo **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="e79ec-185">f.</span><span class="sxs-lookup"><span data-stu-id="e79ec-185">f.</span></span> <span data-ttu-id="e79ec-186">Creare un file con codifica Base 64 dal certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="e79ec-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="e79ec-187">Per ulteriori informazioni, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="e79ec-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="e79ec-188">g.</span><span class="sxs-lookup"><span data-stu-id="e79ec-188">g.</span></span> <span data-ttu-id="e79ec-189">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo hello **certificato di convalida** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e79ec-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="e79ec-190">h.</span><span class="sxs-lookup"><span data-stu-id="e79ec-190">h.</span></span> <span data-ttu-id="e79ec-191">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-191">Click **Save**.</span></span>

1. <span data-ttu-id="e79ec-192">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Cos'è Azure AD Connect][17]

2. <span data-ttu-id="e79ec-194">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Cos'è Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e79ec-196">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e79ec-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="e79ec-197">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure classico chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e79ec-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="e79ec-198">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e79ec-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e79ec-199">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creare un utente test di Azure AD][100] 

2. <span data-ttu-id="e79ec-201">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="e79ec-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="e79ec-202">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creare un utente test di Azure AD][101] 

4. <span data-ttu-id="e79ec-204">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Creare un utente test di Azure AD][102] 

5. <span data-ttu-id="e79ec-206">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e79ec-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Creare un utente test di Azure AD][103]
   
    <span data-ttu-id="e79ec-208">a.</span><span class="sxs-lookup"><span data-stu-id="e79ec-208">a.</span></span> <span data-ttu-id="e79ec-209">In **Tipo di utente** selezionare **Nuovo utente nell'organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="e79ec-210">b.</span><span class="sxs-lookup"><span data-stu-id="e79ec-210">b.</span></span> <span data-ttu-id="e79ec-211">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="e79ec-212">c.</span><span class="sxs-lookup"><span data-stu-id="e79ec-212">c.</span></span> <span data-ttu-id="e79ec-213">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="e79ec-213">Click Next.</span></span>

6. <span data-ttu-id="e79ec-214">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e79ec-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Creare un utente test di Azure AD][104] 
   
    <span data-ttu-id="e79ec-216">a.</span><span class="sxs-lookup"><span data-stu-id="e79ec-216">a.</span></span> <span data-ttu-id="e79ec-217">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="e79ec-218">b.</span><span class="sxs-lookup"><span data-stu-id="e79ec-218">b.</span></span> <span data-ttu-id="e79ec-219">In hello **cognome** casella di testo, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="e79ec-220">c.</span><span class="sxs-lookup"><span data-stu-id="e79ec-220">c.</span></span> <span data-ttu-id="e79ec-221">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="e79ec-222">d.</span><span class="sxs-lookup"><span data-stu-id="e79ec-222">d.</span></span> <span data-ttu-id="e79ec-223">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="e79ec-224">e.</span><span class="sxs-lookup"><span data-stu-id="e79ec-224">e.</span></span> <span data-ttu-id="e79ec-225">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-225">Click **Next**.</span></span>

7. <span data-ttu-id="e79ec-226">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creare un utente test di Azure AD][105]  

8. <span data-ttu-id="e79ec-228">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e79ec-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creare un utente test di Azure AD][106]   
   
    <span data-ttu-id="e79ec-230">a.</span><span class="sxs-lookup"><span data-stu-id="e79ec-230">a.</span></span> <span data-ttu-id="e79ec-231">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="e79ec-232">b.</span><span class="sxs-lookup"><span data-stu-id="e79ec-232">b.</span></span> <span data-ttu-id="e79ec-233">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="e79ec-234">Creazione di un utente test di Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="e79ec-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="e79ec-235">obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon Questetra Business Suite.</span><span class="sxs-lookup"><span data-stu-id="e79ec-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="e79ec-236">**un utente denominato Britta Simon Questetra Business Suite, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e79ec-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="e79ec-237">Sito dell'azienda Questetra BPM Suite tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e79ec-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="e79ec-238">Andare troppo**le impostazioni di sistema > elenco utenti > Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="e79ec-239">Nella finestra di dialogo Nuovo utente hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e79ec-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![Creare un utente test][300] 
   
    <span data-ttu-id="e79ec-241">a.</span><span class="sxs-lookup"><span data-stu-id="e79ec-241">a.</span></span> <span data-ttu-id="e79ec-242">In hello **nome** casella di testo, digitare nome utente di Laura in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e79ec-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="e79ec-243">b.</span><span class="sxs-lookup"><span data-stu-id="e79ec-243">b.</span></span> <span data-ttu-id="e79ec-244">In hello **posta elettronica** casella di testo, digitare nome utente di Laura in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e79ec-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="e79ec-245">c.</span><span class="sxs-lookup"><span data-stu-id="e79ec-245">c.</span></span> <span data-ttu-id="e79ec-246">In hello **Password** casella di testo, digitare una password.</span><span class="sxs-lookup"><span data-stu-id="e79ec-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="e79ec-247">Fare clic su **Add new user**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e79ec-248">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e79ec-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="e79ec-249">obiettivo di Hello di questa sezione è tooenabling toouse Britta Simon single sign-on Azure concedendo proprio tooQuestetra accesso Business Suite.</span><span class="sxs-lookup"><span data-stu-id="e79ec-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![Cos'è Azure AD Connect][200]

<span data-ttu-id="e79ec-251">**tooassign Britta Simon tooQuestetra Business Suite, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e79ec-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="e79ec-252">In hello Azure portale classico, visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="e79ec-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Cos'è Azure AD Connect][201]
2. <span data-ttu-id="e79ec-254">Nell'elenco di applicazioni hello, selezionare **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Cos'è Azure AD Connect][205]
3. <span data-ttu-id="e79ec-256">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![Cos'è Azure AD Connect][202]
4. <span data-ttu-id="e79ec-258">Nell'elenco di utenti hello, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Cos'è Azure AD Connect][203]
5. <span data-ttu-id="e79ec-260">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="e79ec-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Cos'è Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="e79ec-262">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e79ec-262">Testing Single Sign-On</span></span>
<span data-ttu-id="e79ec-263">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e79ec-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="e79ec-264">Quando si fa clic su riquadro Questetra BPM Suite hello in hello Pannello di accesso, è necessario ottenere un'applicazione Questetra BPM Suite tooyour automaticamente firmato in.</span><span class="sxs-lookup"><span data-stu-id="e79ec-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e79ec-265">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e79ec-265">Additional Resources</span></span>
* [<span data-ttu-id="e79ec-266">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e79ec-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e79ec-267">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e79ec-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
