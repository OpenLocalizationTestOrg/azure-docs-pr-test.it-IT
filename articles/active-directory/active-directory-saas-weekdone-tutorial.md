---
title: 'Esercitazione: Integrazione di Azure Active Directory con Weekdone | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Weekdone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f997f1b49ff1aa0659a2409fdd945c6f96413b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="0d2f4-103">Esercitazione: Integrazione di Azure Active Directory con Weekdone</span><span class="sxs-lookup"><span data-stu-id="0d2f4-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="0d2f4-104">In questa esercitazione, è illustrato come toointegrate Weekdone con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d2f4-104">In this tutorial, you learn how toointegrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d2f4-105">Integrazione Weekdone con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0d2f4-105">Integrating Weekdone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0d2f4-106">È possibile controllare in Azure AD che ha accesso tooWeekdone</span><span class="sxs-lookup"><span data-stu-id="0d2f4-106">You can control in Azure AD who has access tooWeekdone</span></span>
- <span data-ttu-id="0d2f4-107">È possibile abilitare l'utenti tooautomatically get connesso tooWeekdone (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d2f4-107">You can enable your users tooautomatically get signed-on tooWeekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0d2f4-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0d2f4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0d2f4-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d2f4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d2f4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0d2f4-110">Prerequisites</span></span>

<span data-ttu-id="0d2f4-111">integrazione di Azure AD con Weekdone tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0d2f4-111">tooconfigure Azure AD integration with Weekdone, you need hello following items:</span></span>

- <span data-ttu-id="0d2f4-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d2f4-113">Sottoscrizione di Weekdone abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0d2f4-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d2f4-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d2f4-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="0d2f4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d2f4-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d2f4-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d2f4-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d2f4-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0d2f4-118">Scenario description</span></span>
<span data-ttu-id="0d2f4-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d2f4-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="0d2f4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d2f4-121">Aggiunta di Weekdone dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0d2f4-121">Adding Weekdone from hello gallery</span></span>
2. <span data-ttu-id="0d2f4-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d2f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-hello-gallery"></a><span data-ttu-id="0d2f4-123">Aggiunta di Weekdone dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0d2f4-123">Adding Weekdone from hello gallery</span></span>
<span data-ttu-id="0d2f4-124">integrazione hello tooconfigure di Weekdone in Azure AD, è necessario tooadd Weekdone dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-124">tooconfigure hello integration of Weekdone into Azure AD, you need tooadd Weekdone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0d2f4-125">**tooadd Weekdone dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0d2f4-125">**tooadd Weekdone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d2f4-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0d2f4-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0d2f4-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0d2f4-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0d2f4-133">Nella casella di ricerca hello, digitare **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-133">In hello search box, type **Weekdone**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="0d2f4-135">Nel riquadro dei risultati hello, selezionare **Weekdone**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-135">In hello results panel, select **Weekdone**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0d2f4-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d2f4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0d2f4-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Weekdone in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0d2f4-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0d2f4-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Weekdone è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Weekdone is tooa user in Azure AD.</span></span> <span data-ttu-id="0d2f4-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Weekdone deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-140">In other words, a link relationship between an Azure AD user and hello related user in Weekdone needs toobe established.</span></span>

<span data-ttu-id="0d2f4-141">In Weekdone, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-141">In Weekdone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0d2f4-142">tooconfigure e prova AD Azure single sign-on con Weekdone, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="0d2f4-142">tooconfigure and test Azure AD single sign-on with Weekdone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0d2f4-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0d2f4-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d2f4-145">**[Creazione di un utente test Weekdone](#creating-a-weekdone-test-user)**  -toohave un equivalente di Britta Simon in Weekdone che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - toohave a counterpart of Britta Simon in Weekdone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d2f4-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d2f4-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0d2f4-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d2f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0d2f4-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Weekdone.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="0d2f4-150">**Azure AD tooconfigure single sign-on con Weekdone, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0d2f4-150">**tooconfigure Azure AD single sign-on with Weekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d2f4-151">Nel portale di Azure su hello hello **Weekdone** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-151">In hello Azure portal, on hello **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0d2f4-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="0d2f4-155">In hello **Weekdone dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="0d2f4-155">On hello **Weekdone Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="0d2f4-157">a.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-157">a.</span></span> <span data-ttu-id="0d2f4-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="0d2f4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="0d2f4-159">b.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-159">b.</span></span> <span data-ttu-id="0d2f4-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="0d2f4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="0d2f4-161">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="0d2f4-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="0d2f4-162">Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="0d2f4-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="0d2f4-164">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="0d2f4-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0d2f4-165">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0d2f4-165">These values are not real.</span></span> <span data-ttu-id="0d2f4-166">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="0d2f4-167">Contatto [team di supporto Weekdone Client](mailto:hello@weekdone.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) tooget these values.</span></span> 

5. <span data-ttu-id="0d2f4-168">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-168">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="0d2f4-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0d2f4-170">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="0d2f4-172">In hello **Weekdone configurazione** fare clic su **configurare Weekdone** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-172">On hello **Weekdone Configuration** section, click **Configure Weekdone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0d2f4-173">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="0d2f4-173">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="0d2f4-175">tooconfigure single sign-on sul **Weekdone** lato, è necessario hello toosend scaricato **Metadata XML, Sign-Out URL, ID entità SAML e SAML Single Sign-On Service URL** troppo[Weekdone supporto Team](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="0d2f4-175">tooconfigure single sign-on on **Weekdone** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="0d2f4-176">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="0d2f4-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0d2f4-177">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0d2f4-178">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0d2f4-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0d2f4-179">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d2f4-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="0d2f4-180">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0d2f4-182">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0d2f4-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d2f4-183">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0d2f4-185">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0d2f4-187">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0d2f4-189">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0d2f4-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0d2f4-191">a.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-191">a.</span></span> <span data-ttu-id="0d2f4-192">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d2f4-193">b.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-193">b.</span></span> <span data-ttu-id="0d2f4-194">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0d2f4-195">c.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-195">c.</span></span> <span data-ttu-id="0d2f4-196">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0d2f4-197">d.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-197">d.</span></span> <span data-ttu-id="0d2f4-198">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="0d2f4-199">Creazione di un utente test di Weekdone</span><span class="sxs-lookup"><span data-stu-id="0d2f4-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="0d2f4-200">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Weekdone toocreate.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-200">hello objective of this section is toocreate a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="0d2f4-201">Weekdone supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="0d2f4-202">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-202">There is no action item for you in this section.</span></span> <span data-ttu-id="0d2f4-203">Se non esiste ancora, durante un tooaccess tentativo Weekdone viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-203">A new user is created during an attempt tooaccess Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="0d2f4-204">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto Weekdone Client](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="0d2f4-204">If you need toocreate a user manually, you need toocontact hello [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0d2f4-205">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d2f4-205">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0d2f4-206">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWeekdone.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-206">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWeekdone.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0d2f4-208">**tooassign Britta Simon tooWeekdone, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0d2f4-208">**tooassign Britta Simon tooWeekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d2f4-209">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-209">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0d2f4-211">Nell'elenco di applicazioni hello, selezionare **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-211">In hello applications list, select **Weekdone**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="0d2f4-213">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-213">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0d2f4-215">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-215">Click **Add** button.</span></span> <span data-ttu-id="0d2f4-216">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0d2f4-218">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-218">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0d2f4-219">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d2f4-220">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0d2f4-221">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0d2f4-221">Testing single sign-on</span></span>

<span data-ttu-id="0d2f4-222">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-222">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0d2f4-223">Quando si fa clic su riquadro Weekdone hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Weekdone applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d2f4-223">When you click hello Weekdone tile in hello Access Panel, you should get automatically signed-on tooyour Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d2f4-224">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0d2f4-224">Additional resources</span></span>

* [<span data-ttu-id="0d2f4-225">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d2f4-225">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d2f4-226">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d2f4-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

