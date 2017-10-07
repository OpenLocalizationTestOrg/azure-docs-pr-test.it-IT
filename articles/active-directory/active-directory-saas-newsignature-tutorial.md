---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cloud Management Portal for Microsoft Azure | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e il portale di gestione di Cloud di Microsoft Azure.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9596826e3dc1289b95009bf01ec8b86f823ef345
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="03c5b-103">Esercitazione: Integrazione di Azure Active Directory con Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="03c5b-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="03c5b-104">In questa esercitazione, è illustrato come toointegrate portale di gestione di Cloud di Microsoft Azure con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03c5b-104">In this tutorial, you learn how toointegrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03c5b-105">Integrazione di portale di gestione di Cloud di Microsoft Azure con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="03c5b-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="03c5b-106">È possibile controllare in Azure AD che ha accesso tooCloud portale di gestione per Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="03c5b-106">You can control in Azure AD who has access tooCloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="03c5b-107">È possibile abilitare l'utenti tooautomatically get connesso tooCloud portale di gestione per Microsoft Azure (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c5b-107">You can enable your users tooautomatically get signed-on tooCloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="03c5b-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="03c5b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="03c5b-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="03c5b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03c5b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="03c5b-110">Prerequisites</span></span>

<span data-ttu-id="03c5b-111">tooconfigure integrazione di Azure AD con il portale di gestione di Cloud di Microsoft Azure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="03c5b-111">tooconfigure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need hello following items:</span></span>

- <span data-ttu-id="03c5b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03c5b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="03c5b-113">Sottoscrizione abilitata di Cloud Management Portal per Microsoft Azure Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="03c5b-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03c5b-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="03c5b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03c5b-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="03c5b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03c5b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="03c5b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03c5b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03c5b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03c5b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="03c5b-118">Scenario description</span></span>
<span data-ttu-id="03c5b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="03c5b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03c5b-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="03c5b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03c5b-121">Aggiungere il portale di gestione di Cloud di Microsoft Azure dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="03c5b-121">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
2. <span data-ttu-id="03c5b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c5b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-hello-gallery"></a><span data-ttu-id="03c5b-123">Aggiungere il portale di gestione di Cloud di Microsoft Azure dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="03c5b-123">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
<span data-ttu-id="03c5b-124">tooconfigure hello integrazione del portale di gestione di Cloud di Microsoft Azure AD Azure, è necessario tooadd il portale di gestione di Cloud di Microsoft Azure dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="03c5b-124">tooconfigure hello integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need tooadd Cloud Management Portal for Microsoft Azure from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="03c5b-125">**Portale di gestione di Cloud di Microsoft Azure dalla raccolta di hello, tooadd eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="03c5b-125">**tooadd Cloud Management Portal for Microsoft Azure from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="03c5b-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="03c5b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="03c5b-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="03c5b-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="03c5b-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="03c5b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="03c5b-133">Nella casella di ricerca hello, digitare **portale di gestione di Cloud di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-133">In hello search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="03c5b-135">Nel riquadro dei risultati hello, selezionare **portale di gestione di Cloud di Microsoft Azure**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="03c5b-135">In hello results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="03c5b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c5b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="03c5b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cloud Management Portal for Microsoft Azure mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="03c5b-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="03c5b-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nel portale di gestione di Cloud per Microsoft Azure è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03c5b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cloud Management Portal for Microsoft Azure is tooa user in Azure AD.</span></span> <span data-ttu-id="03c5b-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello nel portale di gestione di Cloud per Microsoft Azure deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="03c5b-140">In other words, a link relationship between an Azure AD user and hello related user in Cloud Management Portal for Microsoft Azure needs toobe established.</span></span>

<span data-ttu-id="03c5b-141">Nel portale di gestione di Cloud per Microsoft Azure, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="03c5b-141">In Cloud Management Portal for Microsoft Azure, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="03c5b-142">tooconfigure e test con il portale di gestione di Cloud AD Azure single sign-on a Microsoft Azure, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="03c5b-142">tooconfigure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="03c5b-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="03c5b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="03c5b-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03c5b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="03c5b-145">**[Creazione di un portale di gestione di Cloud di Microsoft Azure test](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)**  -toohave un equivalente di Britta Simon nel portale di gestione di Cloud per Microsoft Azure che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="03c5b-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - toohave a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="03c5b-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="03c5b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="03c5b-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="03c5b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="03c5b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c5b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="03c5b-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nel portale di gestione del Cloud per l'applicazione di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="03c5b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="03c5b-150">**tooconfigure AD Azure single sign-on con il portale di gestione di Cloud di Microsoft Azure, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="03c5b-150">**tooconfigure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="03c5b-151">Nel portale di Azure su hello hello **portale di gestione di Cloud di Microsoft Azure** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-151">In hello Azure portal, on hello **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="03c5b-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="03c5b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="03c5b-155">In hello **portale di gestione di Cloud per dominio di Microsoft Azure e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="03c5b-155">On hello **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="03c5b-157">a.</span><span class="sxs-lookup"><span data-stu-id="03c5b-157">a.</span></span> <span data-ttu-id="03c5b-158">In hello **Sign-on URL** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="03c5b-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="03c5b-159">b.</span><span class="sxs-lookup"><span data-stu-id="03c5b-159">b.</span></span> <span data-ttu-id="03c5b-160">In hello **identificatore** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="03c5b-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="03c5b-161">c.</span><span class="sxs-lookup"><span data-stu-id="03c5b-161">c.</span></span> <span data-ttu-id="03c5b-162">In hello **URL di risposta** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="03c5b-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="03c5b-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="03c5b-163">These values are not real.</span></span> <span data-ttu-id="03c5b-164">Aggiornare questi valori con URL di risposta, identificatore e Sign-On URL effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="03c5b-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="03c5b-165">Contatto [portale di gestione per il team di supporto Client di Microsoft Azure Cloud](mailto:jczernuszka@newsignature.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="03c5b-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="03c5b-166">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="03c5b-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="03c5b-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="03c5b-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="03c5b-170">In hello **portale di gestione di Cloud per la configurazione di Microsoft Azure** fare clic su **configurare portale di gestione Cloud per Microsoft Azure** tooopen **Configura sign-on**finestra.</span><span class="sxs-lookup"><span data-stu-id="03c5b-170">On hello **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="03c5b-171">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="03c5b-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="03c5b-173">tooconfigure single sign-on sul **portale di gestione di Cloud di Microsoft Azure** lato, è necessario hello toosend scaricato **certificato**, **Sign-Out URL**, **SAML Single Sign-On Service URL** e **ID entità SAML** troppo[portale di gestione per il team di supporto di Microsoft Azure Cloud](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="03c5b-173">tooconfigure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="03c5b-174">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="03c5b-174">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="03c5b-175">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="03c5b-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="03c5b-176">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="03c5b-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="03c5b-177">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="03c5b-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="03c5b-178">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c5b-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="03c5b-179">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="03c5b-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="03c5b-181">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="03c5b-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="03c5b-182">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="03c5b-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="03c5b-184">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="03c5b-186">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="03c5b-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="03c5b-188">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="03c5b-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="03c5b-190">a.</span><span class="sxs-lookup"><span data-stu-id="03c5b-190">a.</span></span> <span data-ttu-id="03c5b-191">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03c5b-192">b.</span><span class="sxs-lookup"><span data-stu-id="03c5b-192">b.</span></span> <span data-ttu-id="03c5b-193">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="03c5b-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="03c5b-194">c.</span><span class="sxs-lookup"><span data-stu-id="03c5b-194">c.</span></span> <span data-ttu-id="03c5b-195">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="03c5b-196">d.</span><span class="sxs-lookup"><span data-stu-id="03c5b-196">d.</span></span> <span data-ttu-id="03c5b-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="03c5b-198">Creazione di un utente test di Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="03c5b-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="03c5b-199">obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon nel portale di gestione di Cloud di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="03c5b-199">hello objective of this section is toocreate a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="03c5b-200">Rivolgersi [portale di gestione per il team di supporto di Microsoft Azure Cloud](mailto:jczernuszka@newsignature.com) utenti hello tooadd hello portale di gestione di Cloud per l'account di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="03c5b-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) tooadd hello users in hello Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="03c5b-201">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="03c5b-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="03c5b-202">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCloud portale di gestione per Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="03c5b-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloud Management Portal for Microsoft Azure.</span></span>

![Assegna utente][200] 

<span data-ttu-id="03c5b-204">**tooassign Britta Simon tooCloud portale di gestione per Microsoft Azure, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="03c5b-204">**tooassign Britta Simon tooCloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="03c5b-205">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="03c5b-207">Nell'elenco di applicazioni hello, selezionare **portale di gestione di Cloud di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-207">In hello applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="03c5b-209">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="03c5b-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-211">Click **Add** button.</span></span> <span data-ttu-id="03c5b-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="03c5b-214">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="03c5b-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="03c5b-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="03c5b-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="03c5b-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="03c5b-217">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="03c5b-217">Testing single sign-on</span></span>

<span data-ttu-id="03c5b-218">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="03c5b-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="03c5b-219">Quando si fa clic hello portale di gestione di Cloud per il riquadro di Microsoft Azure in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato nel portale di gestione di Cloud per l'applicazione di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="03c5b-219">When you click hello Cloud Management Portal for Microsoft Azure tile in hello Access Panel, you should get automatically signed-on tooyour Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="03c5b-220">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03c5b-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03c5b-221">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="03c5b-221">Additional resources</span></span>

* [<span data-ttu-id="03c5b-222">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03c5b-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="03c5b-223">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03c5b-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

