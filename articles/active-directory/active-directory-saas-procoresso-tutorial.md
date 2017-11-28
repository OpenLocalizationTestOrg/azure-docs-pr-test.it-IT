---
title: 'Esercitazione: Integrazione di Azure Active Directory con Procore SSO | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Procore SSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="19e5e-103">Esercitazione: Integrazione di Azure Active Directory con Procore SSO</span><span class="sxs-lookup"><span data-stu-id="19e5e-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="19e5e-104">In questa esercitazione, è illustrato come toointegrate Procore SSO con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19e5e-104">In this tutorial, you learn how toointegrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19e5e-105">Integrazione Procore SSO con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="19e5e-105">Integrating Procore SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="19e5e-106">È possibile controllare in Azure AD che ha accesso tooProcore SSO</span><span class="sxs-lookup"><span data-stu-id="19e5e-106">You can control in Azure AD who has access tooProcore SSO</span></span>
- <span data-ttu-id="19e5e-107">È possibile abilitare l'utenti tooautomatically get connesso tooProcore SSO (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="19e5e-107">You can enable your users tooautomatically get signed-on tooProcore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19e5e-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="19e5e-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="19e5e-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19e5e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="19e5e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="19e5e-110">Prerequisites</span></span>

<span data-ttu-id="19e5e-111">integrazione di Azure AD con SSO Procore tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="19e5e-111">tooconfigure Azure AD integration with Procore SSO, you need hello following items:</span></span>

- <span data-ttu-id="19e5e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19e5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19e5e-113">Sottoscrizione di Procore SSO abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="19e5e-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19e5e-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="19e5e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19e5e-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="19e5e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19e5e-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="19e5e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="19e5e-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19e5e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19e5e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="19e5e-118">Scenario description</span></span>
<span data-ttu-id="19e5e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="19e5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19e5e-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="19e5e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19e5e-121">Aggiunta di SSO Procore dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="19e5e-121">Adding Procore SSO from hello gallery</span></span>
2. <span data-ttu-id="19e5e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="19e5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-hello-gallery"></a><span data-ttu-id="19e5e-123">Aggiunta di SSO Procore dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="19e5e-123">Adding Procore SSO from hello gallery</span></span>
<span data-ttu-id="19e5e-124">integrazione hello tooconfigure di SSO Procore in Azure AD, è necessario tooadd SSO Procore dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="19e5e-124">tooconfigure hello integration of Procore SSO into Azure AD, you need tooadd Procore SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="19e5e-125">**tooadd Procore SSO dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="19e5e-125">**tooadd Procore SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="19e5e-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="19e5e-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="19e5e-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="19e5e-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="19e5e-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="19e5e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="19e5e-133">Nella casella di ricerca hello, digitare **SSO Procore**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-133">In hello search box, type **Procore SSO**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="19e5e-135">Nel riquadro dei risultati hello, selezionare **SSO Procore**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="19e5e-135">In hello results panel, select **Procore SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="19e5e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="19e5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="19e5e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Procore SSO con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="19e5e-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="19e5e-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SSO Procore è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19e5e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Procore SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="19e5e-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Procore SSO richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="19e5e-140">In other words, a link relationship between an Azure AD user and hello related user in Procore SSO needs toobe established.</span></span>

<span data-ttu-id="19e5e-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="19e5e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Procore SSO.</span></span>

<span data-ttu-id="19e5e-142">tooconfigure e prova AD Azure single sign-on con Procore SSO, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="19e5e-142">tooconfigure and test Azure AD single sign-on with Procore SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="19e5e-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="19e5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="19e5e-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19e5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19e5e-145">**[Creazione di un utente test SSO Procore](#creating-a-procore-sso-test-user)**  -toohave un equivalente di Britta Simon Procore SSO che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="19e5e-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - toohave a counterpart of Britta Simon in Procore SSO that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="19e5e-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="19e5e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19e5e-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="19e5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="19e5e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="19e5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="19e5e-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione SSO Procore.</span><span class="sxs-lookup"><span data-stu-id="19e5e-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="19e5e-150">**Azure AD tooconfigure single sign-on con Procore SSO, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="19e5e-150">**tooconfigure Azure AD single sign-on with Procore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="19e5e-151">Nel portale di gestione di Azure hello in hello **SSO Procore** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-151">In hello Azure Management portal, on hello **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="19e5e-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="19e5e-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="19e5e-155">In hello **Procore dominio SSO e gli URL** sezione, hello utente non dispone di tooperform tutte le operazioni come l'applicazione hello è già pre-integrata con Azure.</span><span class="sxs-lookup"><span data-stu-id="19e5e-155">On hello **Procore SSO Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="19e5e-157">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="19e5e-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="19e5e-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="19e5e-159">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="19e5e-161">In hello **Procore configurazione di SSO** fare clic su **configurare SSO Procore** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="19e5e-161">On hello **Procore SSO Configuration** section, click **Configure Procore SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="19e5e-162">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="19e5e-162">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="19e5e-164">tooconfigure single sign-on sul **Procore SSO** lato, sito aziendale procore tooyour di account di accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="19e5e-164">tooconfigure single sign-on on **Procore SSO** side, login tooyour procore company site as an administrator.</span></span>

8. <span data-ttu-id="19e5e-165">Elenco della casella degli strumenti hello verso il basso, fare clic su **Admin** pagina Impostazioni di tooopen hello SSO.</span><span class="sxs-lookup"><span data-stu-id="19e5e-165">From hello toolbox drop down, click on **Admin** tooopen hello SSO settings page.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="19e5e-167">Incolla hello valori nelle caselle hello come descritto sotto-</span><span class="sxs-lookup"><span data-stu-id="19e5e-167">Paste hello values in hello boxes as described below-</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="19e5e-169">a.</span><span class="sxs-lookup"><span data-stu-id="19e5e-169">a.</span></span> <span data-ttu-id="19e5e-170">In hello **Single Sign On Issuer URL** incollare hello ID entità SAML copiato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="19e5e-170">In hello **Single Sign On Issuer URL** box, paste hello SAML Entity ID copied from hello Azure portal.</span></span>

    <span data-ttu-id="19e5e-171">b.</span><span class="sxs-lookup"><span data-stu-id="19e5e-171">b.</span></span> <span data-ttu-id="19e5e-172">In hello **SAML destinazione URL di accesso** incollare hello SAML Single Sign-On Service URL copiato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="19e5e-172">In hello **SAML Sign On Target URL** box, paste hello SAML Single Sign-On Service URL copied from hello Azure portal.</span></span>

    <span data-ttu-id="19e5e-173">c.</span><span class="sxs-lookup"><span data-stu-id="19e5e-173">c.</span></span> <span data-ttu-id="19e5e-174">Aprire quindi hello **Metadata XML** scaricato in precedenza da hello portale di Azure e certificato hello copia nel tag hello denominato **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-174">Now open hello **Metadata XML** downloaded above from hello Azure portal and copy hello certficate in hello tag named **X509Certificate**.</span></span> <span data-ttu-id="19e5e-175">Valore hello Incolla copiato hello **Single Sign-On x509 certificato** casella.</span><span class="sxs-lookup"><span data-stu-id="19e5e-175">Paste hello copied value into hello **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="19e5e-176">Fare clic su **Save Changes** (Salva modifiche).</span><span class="sxs-lookup"><span data-stu-id="19e5e-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="19e5e-177">Dopo queste impostazioni, è necessario hello toosend **nome di dominio** (ad esempio **contoso.com**) tramite cui si effettua l'accesso toohello Procore [team di supporto Procore](https://support.procore.com/) e avrà attivare SSO federato per quel dominio.</span><span class="sxs-lookup"><span data-stu-id="19e5e-177">After these settings, you needs toosend hello **domain name** (e.g **contoso.com**) through which you are logging into Procore toohello [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="19e5e-178">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="19e5e-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="19e5e-179">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="19e5e-179">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="19e5e-181">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="19e5e-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="19e5e-182">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="19e5e-182">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="19e5e-184">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="19e5e-184">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="19e5e-186">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="19e5e-186">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19e5e-188">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="19e5e-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19e5e-190">a.</span><span class="sxs-lookup"><span data-stu-id="19e5e-190">a.</span></span> <span data-ttu-id="19e5e-191">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19e5e-192">b.</span><span class="sxs-lookup"><span data-stu-id="19e5e-192">b.</span></span> <span data-ttu-id="19e5e-193">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="19e5e-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19e5e-194">c.</span><span class="sxs-lookup"><span data-stu-id="19e5e-194">c.</span></span> <span data-ttu-id="19e5e-195">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="19e5e-196">d.</span><span class="sxs-lookup"><span data-stu-id="19e5e-196">d.</span></span> <span data-ttu-id="19e5e-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="19e5e-198">Creare un utente test di Procore SSO</span><span class="sxs-lookup"><span data-stu-id="19e5e-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="19e5e-199">Seguire hello seguito passaggi toocreate un utente test Procore sul relativo lato.</span><span class="sxs-lookup"><span data-stu-id="19e5e-199">Please follow hello below steps toocreate a Procore test user on their side.</span></span>

1. <span data-ttu-id="19e5e-200">Sito aziendale procore di tooyour account di accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="19e5e-200">Login tooyour procore company site as an administrator.</span></span>  

2. <span data-ttu-id="19e5e-201">Elenco della casella degli strumenti hello verso il basso, fare clic su **Directory** pagina directory della società tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="19e5e-201">From hello toolbox drop down, click on **Directory** tooopen hello company directory page.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="19e5e-203">Fare clic su **aggiungere una persona** opzione modulo hello tooopen e immettere eseguire le seguenti opzioni:</span><span class="sxs-lookup"><span data-stu-id="19e5e-203">Click on **Add a Person** option tooopen hello form and enter perform following options -</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="19e5e-205">a.</span><span class="sxs-lookup"><span data-stu-id="19e5e-205">a.</span></span> <span data-ttu-id="19e5e-206">In hello **nome** casella di testo, nome dell'utente del tipo come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-206">In hello **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="19e5e-207">b.</span><span class="sxs-lookup"><span data-stu-id="19e5e-207">b.</span></span> <span data-ttu-id="19e5e-208">In hello **cognome** casella di testo, cognome dell'utente del tipo come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-208">In hello **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="19e5e-209">c.</span><span class="sxs-lookup"><span data-stu-id="19e5e-209">c.</span></span> <span data-ttu-id="19e5e-210">In hello **indirizzo di posta elettronica** come indirizzo di posta elettronica dell'utente di tipo casella di testo,  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="19e5e-210">In hello **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="19e5e-211">d.</span><span class="sxs-lookup"><span data-stu-id="19e5e-211">d.</span></span> <span data-ttu-id="19e5e-212">Selezionare **Permission Template** (Modello di autorizzazione) per **Apply Permission Template Later** (Applica modello di autorizzazione più tardi).</span><span class="sxs-lookup"><span data-stu-id="19e5e-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="19e5e-213">e.</span><span class="sxs-lookup"><span data-stu-id="19e5e-213">e.</span></span> <span data-ttu-id="19e5e-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-214">Click **Create**.</span></span>

4. <span data-ttu-id="19e5e-215">Verificare e aggiornare i dettagli di hello hello appena aggiunto contatto.</span><span class="sxs-lookup"><span data-stu-id="19e5e-215">Check and update hello details for hello newly added contact.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="19e5e-217">Fare clic su **Salva e Invia invito** (se un invito tramite posta elettronica è obbligatorio) o **salvare** (salvare direttamente) registrazione dell'utente toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="19e5e-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) toocomplete hello user registration.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="19e5e-219">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="19e5e-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="19e5e-220">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooProcore accesso SSO.</span><span class="sxs-lookup"><span data-stu-id="19e5e-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooProcore SSO.</span></span>

![Assegna utente][200] 

<span data-ttu-id="19e5e-222">**tooassign Britta Simon tooProcore SSO, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="19e5e-222">**tooassign Britta Simon tooProcore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="19e5e-223">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="19e5e-225">Nell'elenco di applicazioni hello, selezionare **SSO Procore**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-225">In hello applications list, select **Procore SSO**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="19e5e-227">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="19e5e-229">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-229">Click **Add** button.</span></span> <span data-ttu-id="19e5e-230">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="19e5e-232">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="19e5e-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="19e5e-233">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="19e5e-234">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="19e5e-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="19e5e-235">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="19e5e-235">Testing single sign-on</span></span>

<span data-ttu-id="19e5e-236">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="19e5e-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="19e5e-237">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="19e5e-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="19e5e-238">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="19e5e-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="19e5e-239">Quando si fa clic su riquadro SSO Procore hello in hello Pannello di accesso, è necessario ottenere l'applicazione SSO Procore tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="19e5e-239">When you click hello Procore SSO tile in hello Access Panel, you should get automatically signed-on tooyour Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19e5e-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="19e5e-240">Additional resources</span></span>

* [<span data-ttu-id="19e5e-241">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19e5e-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19e5e-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19e5e-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

