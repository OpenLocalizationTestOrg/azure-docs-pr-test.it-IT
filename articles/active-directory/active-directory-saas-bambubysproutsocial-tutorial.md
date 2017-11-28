---
title: 'Esercitazione: Integrazione di Azure Active Directory con Bambu by Sprout Social | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Bambu da CAVOLI sociali.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c9998772c032476f9a18054873022f55b4bb78be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="b0208-103">Esercitazione: Integrazione di Azure Active Directory con Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="b0208-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="b0208-104">In questa esercitazione, è illustrato come toointegrate Bambu da CAVOLI Social con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0208-104">In this tutorial, you learn how toointegrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0208-105">Integrazione Bambu da CAVOLI Social con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b0208-105">Integrating Bambu by Sprout Social with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b0208-106">È possibile controllare in Azure AD che ha accesso tooBambu da CAVOLI di social networking</span><span class="sxs-lookup"><span data-stu-id="b0208-106">You can control in Azure AD who has access tooBambu by Sprout Social</span></span>
- <span data-ttu-id="b0208-107">È possibile abilitare l'utenti tooautomatically get connesso tooBambu da CAVOLI Social (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0208-107">You can enable your users tooautomatically get signed-on tooBambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0208-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b0208-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b0208-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0208-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Bambu by Sprout Social, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="b0208-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b0208-110">Prerequisites</span></span>

<span data-ttu-id="b0208-111">integrazione di Azure AD con Bambu da CAVOLI Social tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b0208-111">tooconfigure Azure AD integration with Bambu by Sprout Social, you need hello following items:</span></span>

- <span data-ttu-id="b0208-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0208-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0208-113">Sottoscrizione di Bambu by Sprout Social abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b0208-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0208-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b0208-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0208-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="b0208-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0208-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b0208-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b0208-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0208-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0208-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b0208-118">Scenario description</span></span>
<span data-ttu-id="b0208-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b0208-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0208-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="b0208-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0208-121">Aggiunta di Bambu da CAVOLI Social dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b0208-121">Adding Bambu by Sprout Social from hello gallery</span></span>
2. <span data-ttu-id="b0208-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0208-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-hello-gallery"></a><span data-ttu-id="b0208-123">Aggiunta di Bambu da CAVOLI Social dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b0208-123">Adding Bambu by Sprout Social from hello gallery</span></span>
<span data-ttu-id="b0208-124">integrazione hello tooconfigure di Bambu da CAVOLI sociali in Azure AD, è necessario tooadd Bambu da CAVOLI Social dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b0208-124">tooconfigure hello integration of Bambu by Sprout Social into Azure AD, you need tooadd Bambu by Sprout Social from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b0208-125">**tooadd Bambu da CAVOLI Social dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0208-125">**tooadd Bambu by Sprout Social from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0208-126">In hello  **[portale Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b0208-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b0208-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b0208-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b0208-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b0208-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b0208-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello di hello finestra di dialogo tooadd nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b0208-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b0208-133">Nella casella di ricerca hello, digitare **Bambu da CAVOLI Social**.</span><span class="sxs-lookup"><span data-stu-id="b0208-133">In hello search box, type **Bambu by Sprout Social**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="b0208-135">Nel riquadro dei risultati hello, selezionare **Bambu da CAVOLI Social**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b0208-135">In hello results panel, select **Bambu by Sprout Social**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b0208-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0208-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b0208-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Bambu by Sprout Social usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b0208-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0208-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Bambu da CAVOLI Social è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0208-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bambu by Sprout Social is tooa user in Azure AD.</span></span> <span data-ttu-id="b0208-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Bambu da CAVOLI Social deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="b0208-140">In other words, a link relationship between an Azure AD user and hello related user in Bambu by Sprout Social needs toobe established.</span></span>

<span data-ttu-id="b0208-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Bambu da CAVOLI sociali.</span><span class="sxs-lookup"><span data-stu-id="b0208-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="b0208-142">tooconfigure e test Azure AD single sign-on con Bambu da CAVOLI sociale, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="b0208-142">tooconfigure and test Azure AD single sign-on with Bambu by Sprout Social, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b0208-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b0208-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b0208-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0208-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0208-145">**[Creazione di un Bambu utente test CAVOLI Social](#creating-a-bambu-by-sprout-social-test-user)**  -toohave un equivalente di Britta Simon in Bambu da CAVOLI Social toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="b0208-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - toohave a counterpart of Britta Simon in Bambu by Sprout Social that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="b0208-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b0208-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0208-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="b0208-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b0208-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0208-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b0208-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel Bambu dall'applicazione CAVOLI sociali.</span><span class="sxs-lookup"><span data-stu-id="b0208-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="b0208-150">**tooconfigure AD Azure single sign-on con Bambu da CAVOLI di social networking, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0208-150">**tooconfigure Azure AD single sign-on with Bambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0208-151">Nel portale di Azure su hello hello **Bambu da CAVOLI Social** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b0208-151">In hello Azure portal, on hello **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b0208-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b0208-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="b0208-155">In hello **Bambu CAVOLI dominio sociale e gli URL** sezione, hello utente non dispone di tooperform tutte le operazioni come l'applicazione hello è già pre-integrata con Azure.</span><span class="sxs-lookup"><span data-stu-id="b0208-155">On hello **Bambu by Sprout Social Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="b0208-157">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b0208-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="b0208-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b0208-159">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b0208-161">In hello **Bambu dalla configurazione Social CAVOLI** fare clic su **configurare Bambu da CAVOLI Social** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="b0208-161">On hello **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b0208-162">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b0208-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="b0208-164">tooconfigure single sign-on sul **Bambu da CAVOLI Social** lato, è necessario hello toosend scaricato **Metadata XML** e **SAML Single Sign-On Service URL** troppo[Bambu dal supporto tecnico CAVOLI Social](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="b0208-164">tooconfigure single sign-on on **Bambu by Sprout Social** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="b0208-165">Verrà impostata questa in hello toohave ordine connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="b0208-165">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b0208-166">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="b0208-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b0208-167">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** sezione, è sufficiente fare clic su hello **Single Sign-On** hello scheda e l'accesso incorporato documentazione tramite hello **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b0208-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click on hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b0208-168">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0208-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

tooensure users can sign-in tooBambu by Sprout Social after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooBambu by Sprout Social in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b0208-169">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0208-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="b0208-170">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b0208-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b0208-172">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0208-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0208-173">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b0208-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0208-175">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="b0208-175">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0208-177">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b0208-177">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0208-179">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b0208-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0208-181">a.</span><span class="sxs-lookup"><span data-stu-id="b0208-181">a.</span></span> <span data-ttu-id="b0208-182">In hello **nome** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b0208-182">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="b0208-183">b.</span><span class="sxs-lookup"><span data-stu-id="b0208-183">b.</span></span> <span data-ttu-id="b0208-184">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0208-184">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b0208-185">c.</span><span class="sxs-lookup"><span data-stu-id="b0208-185">c.</span></span> <span data-ttu-id="b0208-186">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="b0208-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b0208-187">d.</span><span class="sxs-lookup"><span data-stu-id="b0208-187">d.</span></span> <span data-ttu-id="b0208-188">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b0208-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="b0208-189">Creare un utente test di Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="b0208-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="b0208-190">L'applicazione supporta solo in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti verrà creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b0208-190">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b0208-191">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0208-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b0208-192">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione tooBambu proprio accesso da CAVOLI sociale.</span><span class="sxs-lookup"><span data-stu-id="b0208-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBambu by Sprout Social.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b0208-194">**tooassign tooBambu Britta Simon da CAVOLI di social networking, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0208-194">**tooassign Britta Simon tooBambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0208-195">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b0208-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b0208-197">Nell'elenco di applicazioni hello, selezionare **Bambu da CAVOLI Social**.</span><span class="sxs-lookup"><span data-stu-id="b0208-197">In hello applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="b0208-199">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b0208-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b0208-201">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b0208-201">Click **Add** button.</span></span> <span data-ttu-id="b0208-202">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b0208-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b0208-204">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b0208-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b0208-205">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b0208-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0208-206">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b0208-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b0208-207">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b0208-207">Testing single sign-on</span></span>

<span data-ttu-id="b0208-208">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b0208-208">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b0208-209">Quando si fa clic hello Bambu dal riquadro CAVOLI sociali in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Bambu dall'applicazione CAVOLI sociali.</span><span class="sxs-lookup"><span data-stu-id="b0208-209">When you click hello Bambu by Sprout Social tile in hello Access Panel, you should get automatically signed-on tooyour Bambu by Sprout Social application.</span></span> <span data-ttu-id="b0208-210">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b0208-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b0208-211">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b0208-211">Additional resources</span></span>

* [<span data-ttu-id="b0208-212">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0208-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0208-213">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0208-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

