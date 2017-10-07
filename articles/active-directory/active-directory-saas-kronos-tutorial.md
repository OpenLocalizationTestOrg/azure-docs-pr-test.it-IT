---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kronos | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Kronos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 16fd5c203162d10b78f51b00d79017adaf8632c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="00a80-103">Esercitazione: Integrazione di Azure Active Directory con Kronos</span><span class="sxs-lookup"><span data-stu-id="00a80-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="00a80-104">In questa esercitazione, è illustrato come toointegrate Kronos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="00a80-104">In this tutorial, you learn how toointegrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="00a80-105">Integrazione Kronos con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="00a80-105">Integrating Kronos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="00a80-106">È possibile controllare in Azure AD che ha accesso tooKronos</span><span class="sxs-lookup"><span data-stu-id="00a80-106">You can control in Azure AD who has access tooKronos</span></span>
- <span data-ttu-id="00a80-107">È possibile abilitare l'utenti tooautomatically get connesso tooKronos (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="00a80-107">You can enable your users tooautomatically get signed-on tooKronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="00a80-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="00a80-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="00a80-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00a80-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00a80-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="00a80-110">Prerequisites</span></span>

<span data-ttu-id="00a80-111">integrazione di Azure AD con Kronos tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="00a80-111">tooconfigure Azure AD integration with Kronos, you need hello following items:</span></span>

- <span data-ttu-id="00a80-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00a80-112">An Azure AD subscription</span></span>
- <span data-ttu-id="00a80-113">Sottoscrizione di **Kronos Workforce Central** abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="00a80-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="00a80-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="00a80-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="00a80-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="00a80-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="00a80-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="00a80-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="00a80-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00a80-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="00a80-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="00a80-118">Scenario description</span></span>
<span data-ttu-id="00a80-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="00a80-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="00a80-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="00a80-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="00a80-121">Aggiunta di Kronos dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="00a80-121">Adding Kronos from hello gallery</span></span>
2. <span data-ttu-id="00a80-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="00a80-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-hello-gallery"></a><span data-ttu-id="00a80-123">Aggiunta di Kronos dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="00a80-123">Adding Kronos from hello gallery</span></span>
<span data-ttu-id="00a80-124">integrazione hello tooconfigure di Kronos in Azure AD, è necessario tooadd Kronos dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="00a80-124">tooconfigure hello integration of Kronos into Azure AD, you need tooadd Kronos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="00a80-125">**tooadd Kronos dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="00a80-125">**tooadd Kronos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="00a80-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="00a80-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="00a80-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="00a80-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="00a80-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="00a80-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="00a80-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="00a80-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="00a80-133">Nella casella di ricerca hello, digitare **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="00a80-133">In hello search box, type **Kronos**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="00a80-135">Nel riquadro dei risultati hello, selezionare **Kronos**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="00a80-135">In hello results panel, select **Kronos**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="00a80-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="00a80-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="00a80-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kronos usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="00a80-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="00a80-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Kronos è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00a80-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kronos is tooa user in Azure AD.</span></span> <span data-ttu-id="00a80-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello Kronos deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="00a80-140">In other words, a link relationship between an Azure AD user and hello related user in Kronos needs toobe established.</span></span>

<span data-ttu-id="00a80-141">In Kronos, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="00a80-141">In Kronos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="00a80-142">tooconfigure e prova AD Azure single sign-on con Kronos, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="00a80-142">tooconfigure and test Azure AD single sign-on with Kronos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="00a80-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="00a80-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="00a80-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00a80-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="00a80-145">**[Creazione di un utente test Kronos](#creating-a-kronos-test-user)**  -toohave un equivalente di Britta Simon in Kronos che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="00a80-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - toohave a counterpart of Britta Simon in Kronos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="00a80-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="00a80-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="00a80-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="00a80-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="00a80-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="00a80-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="00a80-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Kronos.</span><span class="sxs-lookup"><span data-stu-id="00a80-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="00a80-150">**Azure AD tooconfigure single sign-on con Kronos, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="00a80-150">**tooconfigure Azure AD single sign-on with Kronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="00a80-151">Nel portale di Azure su hello hello **Kronos** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="00a80-151">In hello Azure portal, on hello **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="00a80-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="00a80-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="00a80-155">In hello **Kronos dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="00a80-155">On hello **Kronos Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="00a80-157">a.</span><span class="sxs-lookup"><span data-stu-id="00a80-157">a.</span></span> <span data-ttu-id="00a80-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="00a80-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="00a80-159">b.</span><span class="sxs-lookup"><span data-stu-id="00a80-159">b.</span></span> <span data-ttu-id="00a80-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="00a80-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="00a80-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="00a80-161">These values are not real.</span></span> <span data-ttu-id="00a80-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="00a80-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="00a80-163">Contatto [Kronos team di supporto](https://www.kronos.in/contact/en-in/form) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="00a80-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) tooget these values.</span></span>
 
4. <span data-ttu-id="00a80-164">L'applicazione Kronos prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="00a80-164">Your Kronos application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="00a80-165">Lavorare con [Kronos team di supporto](https://www.kronos.in/contact/en-in/form) prima tooidentify hello corretto identificatore utente, che viene eseguito il mapping in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="00a80-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first tooidentify hello correct user identifier, which is mapped into hello application.</span></span> <span data-ttu-id="00a80-166">Anche effettuare istruzioni hello sull'attributo hello, che desiderano toouse per questo mapping.</span><span class="sxs-lookup"><span data-stu-id="00a80-166">Also please take hello guidance about hello attribute, which they want toouse for this mapping.</span></span>
 
     <span data-ttu-id="00a80-167">Microsoft consiglia di usare hello **"NameIdentifier"** attributo come identificatore utente.</span><span class="sxs-lookup"><span data-stu-id="00a80-167">Microsoft recommends using hello **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="00a80-168">È possibile gestire i valori hello di questi attributi da hello **"Attributi utente"** sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="00a80-168">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="00a80-169">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="00a80-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="00a80-170">Di seguito è stato eseguito il mapping hello **identificatore utente (nameid)** con **ExtractMailPrefix()** funzione **User**.</span><span class="sxs-lookup"><span data-stu-id="00a80-170">Here we have mapped hello **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="00a80-171">In questo modo il valore di prefisso hello messaggi di posta elettronica dell'utente hello che è hello ID utente univoco.</span><span class="sxs-lookup"><span data-stu-id="00a80-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="00a80-172">Applicazione Kronos toohello viene inviato in ogni risposta con esito positivo.</span><span class="sxs-lookup"><span data-stu-id="00a80-172">This is sent toohello Kronos application in every successful response.</span></span> 
     
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="00a80-174">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="00a80-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="00a80-175">a.</span><span class="sxs-lookup"><span data-stu-id="00a80-175">a.</span></span> <span data-ttu-id="00a80-176">Nell'elenco a discesa di hello identificatore utente, selezionare **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="00a80-176">In hello User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="00a80-177">b.</span><span class="sxs-lookup"><span data-stu-id="00a80-177">b.</span></span> <span data-ttu-id="00a80-178">In hello **posta** elenco a discesa, seleziona **User**.</span><span class="sxs-lookup"><span data-stu-id="00a80-178">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="00a80-179">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="00a80-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="00a80-181">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="00a80-181">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="00a80-183">tooconfigure single sign-on sul **Kronos** lato, è necessario hello toosend scaricato **Metadata XML** troppo[Kronos team di supporto](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="00a80-183">tooconfigure single sign-on on **Kronos** side, you need toosend hello downloaded **Metadata XML** too[Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="00a80-184">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="00a80-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="00a80-185">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="00a80-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="00a80-186">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="00a80-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="00a80-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="00a80-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="00a80-188">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="00a80-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="00a80-190">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="00a80-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="00a80-191">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="00a80-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="00a80-193">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="00a80-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="00a80-195">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="00a80-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="00a80-197">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="00a80-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="00a80-199">a.</span><span class="sxs-lookup"><span data-stu-id="00a80-199">a.</span></span> <span data-ttu-id="00a80-200">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="00a80-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="00a80-201">b.</span><span class="sxs-lookup"><span data-stu-id="00a80-201">b.</span></span> <span data-ttu-id="00a80-202">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="00a80-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="00a80-203">c.</span><span class="sxs-lookup"><span data-stu-id="00a80-203">c.</span></span> <span data-ttu-id="00a80-204">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="00a80-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="00a80-205">d.</span><span class="sxs-lookup"><span data-stu-id="00a80-205">d.</span></span> <span data-ttu-id="00a80-206">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="00a80-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="00a80-207">Creazione di un utente test di Kronos</span><span class="sxs-lookup"><span data-stu-id="00a80-207">Creating a Kronos test user</span></span>

<span data-ttu-id="00a80-208">In questa sezione viene creato un utente chiamato Britta Simon in Kronos.</span><span class="sxs-lookup"><span data-stu-id="00a80-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="00a80-209">Applicazione di Kronos deve tutti toobe agli utenti di hello eseguito il provisioning in un'applicazione hello prima di eseguire SSO.</span><span class="sxs-lookup"><span data-stu-id="00a80-209">Kronos application needs all hello users toobe provisioned in hello application before doing SSO.</span></span> 

<span data-ttu-id="00a80-210">Lavorare con hello [Kronos team di supporto](https://www.kronos.in/contact/en-in/form) tooprovision tutti questi utenti in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="00a80-210">Work with hello [Kronos support team](https://www.kronos.in/contact/en-in/form) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="00a80-211">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="00a80-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="00a80-212">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooKronos.</span><span class="sxs-lookup"><span data-stu-id="00a80-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKronos.</span></span>

![Assegna utente][200] 

<span data-ttu-id="00a80-214">**tooassign Britta Simon tooKronos, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="00a80-214">**tooassign Britta Simon tooKronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="00a80-215">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="00a80-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="00a80-217">Nell'elenco di applicazioni hello, selezionare **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="00a80-217">In hello applications list, select **Kronos**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="00a80-219">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="00a80-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="00a80-221">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="00a80-221">Click **Add** button.</span></span> <span data-ttu-id="00a80-222">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="00a80-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="00a80-224">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="00a80-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="00a80-225">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="00a80-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="00a80-226">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="00a80-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="00a80-227">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="00a80-227">Testing single sign-on</span></span>

<span data-ttu-id="00a80-228">In questa sezione è verificare la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="00a80-228">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="00a80-229">Quando si fa clic hello Kronos riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Kronos applicazione.</span><span class="sxs-lookup"><span data-stu-id="00a80-229">When you click hello Kronos tile in hello Access Panel, you should get automatically signed-on tooyour Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="00a80-230">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="00a80-230">Additional resources</span></span>

* [<span data-ttu-id="00a80-231">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00a80-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="00a80-232">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00a80-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

