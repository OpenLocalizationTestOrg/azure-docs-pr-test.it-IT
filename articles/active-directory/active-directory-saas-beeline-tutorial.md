---
title: 'Esercitazione: Integrazione di Azure Active Directory con BeeLine | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e BeeLine.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 92f228d33980c21ad934185ab89d73795f7f69bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="b345f-103">Esercitazione: Integrazione di Azure Active Directory con BeeLine</span><span class="sxs-lookup"><span data-stu-id="b345f-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="b345f-104">In questa esercitazione, è illustrato come toointegrate BeeLine con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b345f-104">In this tutorial, you learn how toointegrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b345f-105">Integrazione BeeLine con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b345f-105">Integrating BeeLine with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b345f-106">È possibile controllare in Azure AD che ha accesso tooBeeLine</span><span class="sxs-lookup"><span data-stu-id="b345f-106">You can control in Azure AD who has access tooBeeLine</span></span>
- <span data-ttu-id="b345f-107">È possibile abilitare l'utenti tooautomatically get connesso tooBeeLine (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b345f-107">You can enable your users tooautomatically get signed-on tooBeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b345f-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b345f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b345f-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b345f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b345f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b345f-110">Prerequisites</span></span>

<span data-ttu-id="b345f-111">integrazione di Azure AD con BeeLine tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b345f-111">tooconfigure Azure AD integration with BeeLine, you need hello following items:</span></span>

- <span data-ttu-id="b345f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b345f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b345f-113">Sottoscrizione di BeeLine abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b345f-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b345f-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b345f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b345f-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="b345f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b345f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b345f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b345f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b345f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b345f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b345f-118">Scenario description</span></span>
<span data-ttu-id="b345f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b345f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b345f-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="b345f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b345f-121">Aggiunta di BeeLine dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b345f-121">Adding BeeLine from hello gallery</span></span>
2. <span data-ttu-id="b345f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b345f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-hello-gallery"></a><span data-ttu-id="b345f-123">Aggiunta di BeeLine dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b345f-123">Adding BeeLine from hello gallery</span></span>
<span data-ttu-id="b345f-124">integrazione hello tooconfigure di BeeLine in Azure AD, è necessario tooadd BeeLine dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b345f-124">tooconfigure hello integration of BeeLine into Azure AD, you need tooadd BeeLine from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b345f-125">**tooadd BeeLine dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b345f-125">**tooadd BeeLine from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b345f-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b345f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b345f-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b345f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b345f-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b345f-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b345f-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b345f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b345f-133">Nella casella di ricerca hello, digitare **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="b345f-133">In hello search box, type **BeeLine**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="b345f-135">Nel riquadro dei risultati hello, selezionare **BeeLine**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b345f-135">In hello results panel, select **BeeLine**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b345f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b345f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b345f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BeeLine usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b345f-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b345f-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in BeeLine è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b345f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BeeLine is tooa user in Azure AD.</span></span> <span data-ttu-id="b345f-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in BeeLine deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="b345f-140">In other words, a link relationship between an Azure AD user and hello related user in BeeLine needs toobe established.</span></span>

<span data-ttu-id="b345f-141">In BeeLine, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="b345f-141">In BeeLine, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b345f-142">tooconfigure e prova AD Azure single sign-on con BeeLine, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="b345f-142">tooconfigure and test Azure AD single sign-on with BeeLine, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b345f-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b345f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b345f-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b345f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b345f-145">**[Creazione di un utente test BeeLine](#creating-a-beeline-test-user)**  -toohave un equivalente di Britta Simon in BeeLine che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b345f-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - toohave a counterpart of Britta Simon in BeeLine that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b345f-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b345f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b345f-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="b345f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b345f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b345f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b345f-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione BeeLine.</span><span class="sxs-lookup"><span data-stu-id="b345f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="b345f-150">**Azure AD tooconfigure single sign-on con BeeLine, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b345f-150">**tooconfigure Azure AD single sign-on with BeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="b345f-151">Nel portale di Azure su hello hello **BeeLine** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b345f-151">In hello Azure portal, on hello **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b345f-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b345f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="b345f-155">In hello **BeeLine dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b345f-155">On hello **BeeLine Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="b345f-157">a.</span><span class="sxs-lookup"><span data-stu-id="b345f-157">a.</span></span> <span data-ttu-id="b345f-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="b345f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="b345f-159">b.</span><span class="sxs-lookup"><span data-stu-id="b345f-159">b.</span></span> <span data-ttu-id="b345f-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="b345f-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="b345f-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b345f-161">These values are not real.</span></span> <span data-ttu-id="b345f-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="b345f-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="b345f-163">Contatto [team di supporto BeeLine](https://www.beeline.com/contact-us/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="b345f-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) tooget these values.</span></span>
 
4. <span data-ttu-id="b345f-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b345f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="b345f-166">L'applicazione Beeline prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="b345f-166">Your Beeline application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b345f-167">Rivolgersi [team di supporto BeeLine](https://www.beeline.com/contact-us/) tooidentify prima hello identificatore utente corretti che verrà eseguito il mapping in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b345f-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first tooidentify hello correct user identifier which will be mapped into hello application.</span></span> <span data-ttu-id="b345f-168">Attenersi alle linee guida hello anche [team di supporto BeeLine](https://www.beeline.com/contact-us/) su hello attributo che desiderano toouse per questo mapping.</span><span class="sxs-lookup"><span data-stu-id="b345f-168">Also please take hello guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about hello attribute which they want toouse for this mapping.</span></span> <span data-ttu-id="b345f-169">È possibile gestire il valore di hello di questo attributo dal hello **gli attributi utente** scheda dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b345f-169">You can manage hello value of this attribute from hello **User Attributes** tab of hello application.</span></span> <span data-ttu-id="b345f-170">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="b345f-170">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="b345f-171">Di seguito è stato eseguito il mapping hello **identificatore utente** un'attestazione con hello **userprincipalname** attributo, che fornisce ID utente univoco, che sarà inviato toohello Beeline applicazione hello ogni SAML corretta Risposta.</span><span class="sxs-lookup"><span data-stu-id="b345f-171">Here we have mapped hello **User Identifier** claim with hello **userprincipalname** attribute, which provides unique user ID, which will be sent toohello Beeline application in hello every successful SAML Response.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="b345f-173">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b345f-173">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b345f-175">In hello **BeeLine configurazione** fare clic su **configurare BeeLine** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="b345f-175">On hello **BeeLine Configuration** section, click **Configure BeeLine** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b345f-176">Hello copia **Sign-Out URL** e **ID entità SAML** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b345f-176">Copy hello **Sign-Out URL** and **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="b345f-178">tooconfigure single sign-on sul **BeeLine** lato, è necessario hello toosend scaricato **Metadata XML** e **ID entità SAML**, **Sign-Out URL**troppo[team di supporto BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="b345f-178">tooconfigure single sign-on on **BeeLine** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** too[BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="b345f-179">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="b345f-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b345f-180">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b345f-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b345f-181">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b345f-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b345f-182">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b345f-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="b345f-183">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b345f-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b345f-185">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b345f-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b345f-186">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b345f-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b345f-188">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b345f-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b345f-190">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="b345f-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b345f-192">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b345f-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b345f-194">a.</span><span class="sxs-lookup"><span data-stu-id="b345f-194">a.</span></span> <span data-ttu-id="b345f-195">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b345f-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b345f-196">b.</span><span class="sxs-lookup"><span data-stu-id="b345f-196">b.</span></span> <span data-ttu-id="b345f-197">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b345f-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b345f-198">c.</span><span class="sxs-lookup"><span data-stu-id="b345f-198">c.</span></span> <span data-ttu-id="b345f-199">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="b345f-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b345f-200">d.</span><span class="sxs-lookup"><span data-stu-id="b345f-200">d.</span></span> <span data-ttu-id="b345f-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b345f-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="b345f-202">Creazione di un utente di test di BeeLine</span><span class="sxs-lookup"><span data-stu-id="b345f-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="b345f-203">In questa sezione viene creato un utente di nome Britta Simon in Beeline.</span><span class="sxs-lookup"><span data-stu-id="b345f-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="b345f-204">Applicazione di beeline deve tutti toobe agli utenti di hello eseguito il provisioning in un'applicazione hello prima di eseguire Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b345f-204">Beeline application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="b345f-205">Pertanto, possono essere utilizzati con hello [team di supporto BeeLine](https://www.beeline.com/contact-us/) tooprovision tutti questi utenti in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b345f-205">So work with hello [BeeLine support team](https://www.beeline.com/contact-us/) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b345f-206">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b345f-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b345f-207">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBeeLine.</span><span class="sxs-lookup"><span data-stu-id="b345f-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBeeLine.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b345f-209">**tooassign Britta Simon tooBeeLine, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b345f-209">**tooassign Britta Simon tooBeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="b345f-210">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b345f-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b345f-212">Nell'elenco di applicazioni hello, selezionare **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="b345f-212">In hello applications list, select **BeeLine**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="b345f-214">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b345f-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b345f-216">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b345f-216">Click **Add** button.</span></span> <span data-ttu-id="b345f-217">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b345f-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b345f-219">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b345f-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b345f-220">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b345f-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b345f-221">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b345f-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b345f-222">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b345f-222">Testing single sign-on</span></span>

<span data-ttu-id="b345f-223">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b345f-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="b345f-224">Quando si fa clic su riquadro Beeline hello in hello Pannello di accesso, è necessario ottenere applicazione Beeline tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="b345f-224">When you click hello Beeline tile in hello Access Panel, you should get automatically signed-on tooyour Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b345f-225">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b345f-225">Additional resources</span></span>

* [<span data-ttu-id="b345f-226">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b345f-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b345f-227">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b345f-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

