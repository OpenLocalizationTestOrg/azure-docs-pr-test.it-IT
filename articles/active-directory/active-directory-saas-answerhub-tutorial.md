---
title: 'Esercitazione: Integrazione di Azure Active Directory con AnswerHub | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e AnswerHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="83b4f-103">Esercitazione: Integrazione di Azure Active Directory con AnswerHub</span><span class="sxs-lookup"><span data-stu-id="83b4f-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="83b4f-104">In questa esercitazione, è illustrato come toointegrate AnswerHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83b4f-104">In this tutorial, you learn how toointegrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83b4f-105">Integrazione di AnswerHub con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="83b4f-105">Integrating AnswerHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="83b4f-106">È possibile controllare in Azure AD che ha accesso tooAnswerHub</span><span class="sxs-lookup"><span data-stu-id="83b4f-106">You can control in Azure AD who has access tooAnswerHub</span></span>
- <span data-ttu-id="83b4f-107">È possibile abilitare l'utenti tooautomatically get connesso tooAnswerHub (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="83b4f-107">You can enable your users tooautomatically get signed-on tooAnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83b4f-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="83b4f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="83b4f-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83b4f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83b4f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="83b4f-110">Prerequisites</span></span>

<span data-ttu-id="83b4f-111">integrazione di Azure AD con AnswerHub tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="83b4f-111">tooconfigure Azure AD integration with AnswerHub, you need hello following items:</span></span>

- <span data-ttu-id="83b4f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83b4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83b4f-113">Sottoscrizione di AnswerHub abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="83b4f-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83b4f-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="83b4f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83b4f-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="83b4f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83b4f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="83b4f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83b4f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83b4f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83b4f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="83b4f-118">Scenario description</span></span>
<span data-ttu-id="83b4f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="83b4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83b4f-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="83b4f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83b4f-121">Aggiunta di AnswerHub dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="83b4f-121">Adding AnswerHub from hello gallery</span></span>
2. <span data-ttu-id="83b4f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="83b4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-hello-gallery"></a><span data-ttu-id="83b4f-123">Aggiunta di AnswerHub dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="83b4f-123">Adding AnswerHub from hello gallery</span></span>
<span data-ttu-id="83b4f-124">integrazione hello tooconfigure di AnswerHub in Azure AD, è necessario tooadd AnswerHub dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="83b4f-124">tooconfigure hello integration of AnswerHub into Azure AD, you need tooadd AnswerHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="83b4f-125">**tooadd AnswerHub dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="83b4f-125">**tooadd AnswerHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="83b4f-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="83b4f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83b4f-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="83b4f-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="83b4f-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="83b4f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="83b4f-133">Nella casella di ricerca hello, digitare **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-133">In hello search box, type **AnswerHub**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="83b4f-135">Nel riquadro dei risultati hello, selezionare **AnswerHub**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="83b4f-135">In hello results panel, select **AnswerHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83b4f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="83b4f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83b4f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con AnswerHub usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="83b4f-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="83b4f-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in AnswerHub è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83b4f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AnswerHub is tooa user in Azure AD.</span></span> <span data-ttu-id="83b4f-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in AnswerHub deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="83b4f-140">In other words, a link relationship between an Azure AD user and hello related user in AnswerHub needs toobe established.</span></span>

<span data-ttu-id="83b4f-141">In AnswerHub, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="83b4f-141">In AnswerHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="83b4f-142">tooconfigure e prova AD Azure single sign-on con AnswerHub, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="83b4f-142">tooconfigure and test Azure AD single sign-on with AnswerHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="83b4f-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="83b4f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="83b4f-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83b4f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83b4f-145">**[Creazione di un utente test AnswerHub](#creating-an-answerhub-test-user)**  -toohave un equivalente di Britta Simon in AnswerHub che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="83b4f-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - toohave a counterpart of Britta Simon in AnswerHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="83b4f-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="83b4f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83b4f-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="83b4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83b4f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="83b4f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83b4f-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="83b4f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="83b4f-150">**Azure AD tooconfigure single sign-on con AnswerHub, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="83b4f-150">**tooconfigure Azure AD single sign-on with AnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="83b4f-151">Nel portale di Azure su hello hello **AnswerHub** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-151">In hello Azure portal, on hello **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="83b4f-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="83b4f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="83b4f-155">In hello **AnswerHub dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="83b4f-155">On hello **AnswerHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="83b4f-157">a.</span><span class="sxs-lookup"><span data-stu-id="83b4f-157">a.</span></span> <span data-ttu-id="83b4f-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="83b4f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="83b4f-159">b.</span><span class="sxs-lookup"><span data-stu-id="83b4f-159">b.</span></span> <span data-ttu-id="83b4f-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="83b4f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="83b4f-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="83b4f-161">These values are not real.</span></span> <span data-ttu-id="83b4f-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="83b4f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="83b4f-163">Contatto [team di supporto Client di AnswerHub](mailto:success@answerhub.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="83b4f-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="83b4f-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="83b4f-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="83b4f-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="83b4f-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="83b4f-168">In hello **AnswerHub configurazione** fare clic su **configurare AnswerHub** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="83b4f-168">On hello **AnswerHub Configuration** section, click **Configure AnswerHub** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="83b4f-169">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="83b4f-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="83b4f-171">In un'altra finestra del Web browser accedere al sito aziendale di AnswerHub come amministratore.</span><span class="sxs-lookup"><span data-stu-id="83b4f-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="83b4f-172">Per ottenere assistenza nella configurazione di AnswerHub, contattare il [team di supporto di AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="83b4f-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="83b4f-173">Andare troppo**amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-173">Go too**Administration**.</span></span>

9. <span data-ttu-id="83b4f-174">Fare clic su hello **utenti e gruppi** scheda.</span><span class="sxs-lookup"><span data-stu-id="83b4f-174">Click hello **User and Group** tab.</span></span>

10. <span data-ttu-id="83b4f-175">Nel riquadro di spostamento hello sul lato sinistro, in hello hello **Social Settings** fare clic su **SAML Setup**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-175">In hello navigation pane on hello left side, in hello **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="83b4f-176">Fare clic sulla scheda **IDP Config** .</span><span class="sxs-lookup"><span data-stu-id="83b4f-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="83b4f-177">In hello **IDP Config** effettuare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="83b4f-177">On hello **IDP Config** tab, perform hello following steps:</span></span>

     <span data-ttu-id="83b4f-178">![Configurazione SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="83b4f-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="83b4f-179">a.</span><span class="sxs-lookup"><span data-stu-id="83b4f-179">a.</span></span> <span data-ttu-id="83b4f-180">Nella casella di testo **IDP Login URL** (URL di accesso IdP) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b4f-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="83b4f-181">b.</span><span class="sxs-lookup"><span data-stu-id="83b4f-181">b.</span></span> <span data-ttu-id="83b4f-182">Nella casella di testo **IDP Logout URL** (URL di disconnessione IdP) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b4f-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="83b4f-183">c.</span><span class="sxs-lookup"><span data-stu-id="83b4f-183">c.</span></span> <span data-ttu-id="83b4f-184">In **IDP Name Identifier Format** casella di testo, immettere nome utente hello identificatore stesso valore come selezionato nel portale di Azure in **gli attributi utente** sezione.</span><span class="sxs-lookup"><span data-stu-id="83b4f-184">In **IDP Name Identifier Format** textbox, enter hello user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="83b4f-185">d.</span><span class="sxs-lookup"><span data-stu-id="83b4f-185">d.</span></span> <span data-ttu-id="83b4f-186">Fare clic su **Keys and Certificates**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="83b4f-187">Nella scheda Keys and Certificates hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="83b4f-187">On hello Keys and Certificates tab, perform hello following steps:</span></span>
    
     <span data-ttu-id="83b4f-188">![Chiavi e certificati](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Chiavi e certificati")</span><span class="sxs-lookup"><span data-stu-id="83b4f-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="83b4f-189">a.</span><span class="sxs-lookup"><span data-stu-id="83b4f-189">a.</span></span> <span data-ttu-id="83b4f-190">Aprire il certificato con codifica base 64 che è stato scaricato dal portale di Azure nel blocco note, hello copia del contenuto di esso negli Appunti, e quindi incollarlo toohello **IDP Public Key (X509 Format)** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="83b4f-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="83b4f-191">b.</span><span class="sxs-lookup"><span data-stu-id="83b4f-191">b.</span></span> <span data-ttu-id="83b4f-192">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-192">Click **Save**.</span></span>

14. <span data-ttu-id="83b4f-193">In hello **IDP Config** scheda, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-193">On hello **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="83b4f-194">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="83b4f-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="83b4f-195">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="83b4f-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="83b4f-196">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83b4f-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83b4f-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="83b4f-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="83b4f-198">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="83b4f-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="83b4f-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="83b4f-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="83b4f-201">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="83b4f-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83b4f-203">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83b4f-205">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="83b4f-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83b4f-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="83b4f-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83b4f-209">a.</span><span class="sxs-lookup"><span data-stu-id="83b4f-209">a.</span></span> <span data-ttu-id="83b4f-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83b4f-211">b.</span><span class="sxs-lookup"><span data-stu-id="83b4f-211">b.</span></span> <span data-ttu-id="83b4f-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="83b4f-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83b4f-213">c.</span><span class="sxs-lookup"><span data-stu-id="83b4f-213">c.</span></span> <span data-ttu-id="83b4f-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="83b4f-215">d.</span><span class="sxs-lookup"><span data-stu-id="83b4f-215">d.</span></span> <span data-ttu-id="83b4f-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="83b4f-217">Creazione di un utente di test di AnswerHub</span><span class="sxs-lookup"><span data-stu-id="83b4f-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="83b4f-218">toolog agli utenti di Azure AD tooenable in tooAnswerHub, è necessario eseguirne il provisioning in AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="83b4f-218">tooenable Azure AD users toolog in tooAnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="83b4f-219">Nel caso di hello di AnswerHub, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="83b4f-219">In hello case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="83b4f-220">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="83b4f-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="83b4f-221">Accedi tooyour **AnswerHub** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="83b4f-221">Log in tooyour **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="83b4f-222">Andare troppo**amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-222">Go too**Administration**.</span></span>

3. <span data-ttu-id="83b4f-223">Fare clic su hello **utenti e gruppi** scheda.</span><span class="sxs-lookup"><span data-stu-id="83b4f-223">Click hello **Users & Groups** tab.</span></span>

4. <span data-ttu-id="83b4f-224">Nel riquadro di spostamento hello sul lato sinistro, in hello hello **Gestisci utenti** fare clic su **agli utenti di creare o importare**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-224">In hello navigation pane on hello left side, in hello **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="83b4f-225">![Utenti e gruppi](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Utenti e gruppi")</span><span class="sxs-lookup"><span data-stu-id="83b4f-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="83b4f-226">Hello tipo **indirizzo di posta elettronica**, **Username** e **Password** di Azure un valido account Active Directory si vuole tooprovision in hello relative caselle di testo e quindi scegliere  **Salvare**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-226">Type hello **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want tooprovision into hello related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="83b4f-227">È possibile usare qualsiasi altro AnswerHub utente account strumento di creazione o le API fornite da AnswerHub tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="83b4f-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="83b4f-228">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="83b4f-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="83b4f-229">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAnswerHub.</span><span class="sxs-lookup"><span data-stu-id="83b4f-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnswerHub.</span></span>

![Assegna utente][200] 

<span data-ttu-id="83b4f-231">**tooassign Britta Simon tooAnswerHub, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="83b4f-231">**tooassign Britta Simon tooAnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="83b4f-232">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="83b4f-234">Nell'elenco di applicazioni hello, selezionare **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-234">In hello applications list, select **AnswerHub**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="83b4f-236">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="83b4f-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-238">Click **Add** button.</span></span> <span data-ttu-id="83b4f-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="83b4f-241">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="83b4f-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="83b4f-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83b4f-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="83b4f-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83b4f-244">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="83b4f-244">Testing single sign-on</span></span>

<span data-ttu-id="83b4f-245">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="83b4f-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="83b4f-246">Quando si fa clic su riquadro AnswerHub hello in hello Pannello di accesso, è necessario ottenere applicazione AnswerHub tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="83b4f-246">When you click hello AnswerHub tile in hello Access Panel, you should get automatically signed-on tooyour AnswerHub application.</span></span>
<span data-ttu-id="83b4f-247">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="83b4f-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="83b4f-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="83b4f-248">Additional resources</span></span>

* [<span data-ttu-id="83b4f-249">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83b4f-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83b4f-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83b4f-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

