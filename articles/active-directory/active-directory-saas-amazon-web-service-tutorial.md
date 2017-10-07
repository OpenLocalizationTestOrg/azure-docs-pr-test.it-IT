---
title: 'Esercitazione: Integrazione di Azure Active Directory con Amazon Web Service (AWS) | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Amazon Web Services (AWS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="32c48-103">Esercitazione: Integrazione di Azure Active Directory con Amazon Web Service (AWS)</span><span class="sxs-lookup"><span data-stu-id="32c48-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="32c48-104">In questa esercitazione, è illustrato come toointegrate Amazon Web Services (AWS) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32c48-104">In this tutorial, you learn how toointegrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32c48-105">Integrazione di Amazon Web Services (AWS) con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="32c48-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32c48-106">È possibile controllare in Azure AD che ha accesso tooAmazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="32c48-106">You can control in Azure AD who has access tooAmazon Web Services (AWS)</span></span>
- <span data-ttu-id="32c48-107">È possibile abilitare l'utenti tooautomatically get connesso tooAmazon Web Services (AWS) (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="32c48-107">You can enable your users tooautomatically get signed-on tooAmazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32c48-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="32c48-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="32c48-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32c48-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="32c48-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="32c48-110">Prerequisites</span></span>

<span data-ttu-id="32c48-111">integrazione di Azure AD con Amazon Web Services (AWS) tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="32c48-111">tooconfigure Azure AD integration with Amazon Web Services (AWS), you need hello following items:</span></span>

- <span data-ttu-id="32c48-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32c48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32c48-113">Sottoscrizione Amazon Web Service (AWS) abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="32c48-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32c48-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="32c48-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32c48-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="32c48-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32c48-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="32c48-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="32c48-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32c48-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32c48-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="32c48-118">Scenario description</span></span>
<span data-ttu-id="32c48-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="32c48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32c48-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="32c48-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32c48-121">Aggiunta di Amazon Web Services (AWS) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="32c48-121">Adding Amazon Web Services (AWS) from hello gallery</span></span>
2. <span data-ttu-id="32c48-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32c48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a><span data-ttu-id="32c48-123">Aggiunta di Amazon Web Services (AWS) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="32c48-123">Adding Amazon Web Services (AWS) from hello gallery</span></span>
<span data-ttu-id="32c48-124">integrazione di hello di tooconfigure di Amazon Web Services (AWS) in Azure AD, è necessario tooadd Amazon Web Services (AWS) dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="32c48-124">tooconfigure hello integration of Amazon Web Services (AWS) into Azure AD, you need tooadd Amazon Web Services (AWS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32c48-125">**tooadd Amazon Web Services (AWS) dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32c48-125">**tooadd Amazon Web Services (AWS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="32c48-126">In hello  **[portale Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="32c48-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32c48-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="32c48-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="32c48-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="32c48-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="32c48-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="32c48-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="32c48-133">Nella casella di ricerca hello, digitare **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="32c48-133">In hello search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="32c48-135">Nel riquadro dei risultati hello, selezionare **Amazon Web Services (AWS)**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="32c48-135">In hello results panel, select **Amazon Web Services (AWS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32c48-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32c48-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32c48-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Amazon Web Services (AWS) usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32c48-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32c48-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello Amazon Web Services (AWS) è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32c48-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Amazon Web Services (AWS) is tooa user in Azure AD.</span></span> <span data-ttu-id="32c48-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello Amazon Web Services (AWS) richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="32c48-140">In other words, a link relationship between an Azure AD user and hello related user in Amazon Web Services (AWS) needs toobe established.</span></span>

<span data-ttu-id="32c48-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="32c48-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="32c48-142">tooconfigure e test di Azure AD single sign-on con Amazon Web Services (AWS), è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="32c48-142">tooconfigure and test Azure AD single sign-on with Amazon Web Services (AWS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="32c48-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="32c48-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="32c48-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32c48-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32c48-145">**[Creazione di un utente di test di Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave un equivalente di Britta Simon Amazon Web Services (AWS) che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="32c48-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - toohave a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="32c48-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="32c48-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32c48-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="32c48-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32c48-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32c48-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32c48-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="32c48-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="32c48-150">**tooconfigure AD Azure single sign-on con Amazon Web Services (AWS), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32c48-150">**tooconfigure Azure AD single sign-on with Amazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="32c48-151">Nel portale di Azure, di hello in hello **Amazon Web Services (AWS)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="32c48-151">In hello Azure Portal, on hello **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="32c48-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="32c48-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="32c48-155">In hello **Amazon Web Services (AWS) dominio e gli URL** sezione, hello utente non dispone di tooperform tutte le operazioni come l'applicazione hello è già pre-integrata con Azure.</span><span class="sxs-lookup"><span data-stu-id="32c48-155">On hello **Amazon Web Services (AWS) Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="32c48-157">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="32c48-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="32c48-159">applicazione Software Amazon Web Services (AWS) Hello prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="32c48-159">hello Amazon Web Services (AWS) Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="32c48-160">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="32c48-160">Please configure hello following claims for this application.</span></span> <span data-ttu-id="32c48-161">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32c48-161">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="32c48-162">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="32c48-162">hello following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="32c48-164">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32c48-164">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="32c48-165">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="32c48-165">Attribute Name</span></span>  | <span data-ttu-id="32c48-166">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="32c48-166">Attribute Value</span></span> | <span data-ttu-id="32c48-167">Spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="32c48-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="32c48-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="32c48-168">RoleSessionName</span></span> | <span data-ttu-id="32c48-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="32c48-169">user.userprincipalname</span></span> | <span data-ttu-id="32c48-170">https://AWS.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="32c48-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="32c48-171">Ruolo</span><span class="sxs-lookup"><span data-stu-id="32c48-171">Role</span></span>            | <span data-ttu-id="32c48-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="32c48-172">user.assignedroles</span></span> |  <span data-ttu-id="32c48-173">https://AWS.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="32c48-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="32c48-174">È necessario il provisioning in Azure AD toofetch tutti i ruoli di hello dalla Console di AWS degli utenti tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="32c48-174">You need tooconfigure hello user provisioning in Azure AD toofetch all hello roles from AWS Console.</span></span> <span data-ttu-id="32c48-175">Consultare hello provisioning passaggi riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="32c48-175">Please refer hello provisioning steps below.</span></span>

    <span data-ttu-id="32c48-176">a.</span><span class="sxs-lookup"><span data-stu-id="32c48-176">a.</span></span> <span data-ttu-id="32c48-177">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="32c48-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="32c48-179">b.</span><span class="sxs-lookup"><span data-stu-id="32c48-179">b.</span></span> <span data-ttu-id="32c48-180">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="32c48-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="32c48-182">c.</span><span class="sxs-lookup"><span data-stu-id="32c48-182">c.</span></span> <span data-ttu-id="32c48-183">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="32c48-183">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="32c48-184">Aggiungere il valore di Namespace hello come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="32c48-184">Add hello Namespace value as given above.</span></span>
    
    <span data-ttu-id="32c48-185">d.</span><span class="sxs-lookup"><span data-stu-id="32c48-185">d.</span></span> <span data-ttu-id="32c48-186">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="32c48-186">Click **Ok**.</span></span>

7. <span data-ttu-id="32c48-187">Fare clic su **salvare** pulsante Impostazioni hello toosave in Azure.</span><span class="sxs-lookup"><span data-stu-id="32c48-187">Click **Save** button toosave hello settings on Azure.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="32c48-189">In un'altra finestra del browser del sito della società di Amazon Web Services (AWS) tooyour sign-on come amministratore.</span><span class="sxs-lookup"><span data-stu-id="32c48-189">In a different browser window, sign-on tooyour Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="32c48-190">Fare clic su **Console Home**.</span><span class="sxs-lookup"><span data-stu-id="32c48-190">Click **Console Home**.</span></span>
   
    ![Configura accesso Single Sign-On][11]

10. <span data-ttu-id="32c48-192">Fare clic su **IAM** dal servizio **Sicurezza, identità e conformità**.</span><span class="sxs-lookup"><span data-stu-id="32c48-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Configura accesso Single Sign-On][12]

11. <span data-ttu-id="32c48-194">Fare clic su **Provider di identità** e quindi fare clic su **Create Provider** (Crea provider).</span><span class="sxs-lookup"><span data-stu-id="32c48-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Configura accesso Single Sign-On][13]

12. <span data-ttu-id="32c48-196">In hello **configurare Provider** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32c48-196">On hello **Configure Provider** dialog page, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On][14]
 
    <span data-ttu-id="32c48-198">a.</span><span class="sxs-lookup"><span data-stu-id="32c48-198">a.</span></span> <span data-ttu-id="32c48-199">In **Tipo provider** selezionare **SAML**.</span><span class="sxs-lookup"><span data-stu-id="32c48-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="32c48-200">b.</span><span class="sxs-lookup"><span data-stu-id="32c48-200">b.</span></span> <span data-ttu-id="32c48-201">In hello **nome Provider** casella di testo, digitare un nome di provider (ad esempio: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="32c48-201">In hello **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="32c48-202">c.</span><span class="sxs-lookup"><span data-stu-id="32c48-202">c.</span></span> <span data-ttu-id="32c48-203">tooupload file di metadati scaricato, fare clic su **Scegli File**.</span><span class="sxs-lookup"><span data-stu-id="32c48-203">tooupload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="32c48-204">d.</span><span class="sxs-lookup"><span data-stu-id="32c48-204">d.</span></span> <span data-ttu-id="32c48-205">Fare clic su **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="32c48-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="32c48-206">In hello **verificare le informazioni sul Provider** nella pagina, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="32c48-206">On hello **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Configura accesso Single Sign-On][15]

14. <span data-ttu-id="32c48-208">Fare clic su **Ruoli** e quindi fare clic su **Crea nuovo ruolo**.</span><span class="sxs-lookup"><span data-stu-id="32c48-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Configura accesso Single Sign-On][16]

15. <span data-ttu-id="32c48-210">In hello **imposta il nome del ruolo** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32c48-210">On hello **Set Role Name** dialog, perform hello following steps:</span></span> 
    
    ![Configura accesso Single Sign-On][17] 

    <span data-ttu-id="32c48-212">a.</span><span class="sxs-lookup"><span data-stu-id="32c48-212">a.</span></span> <span data-ttu-id="32c48-213">In hello **nome ruolo** casella di testo, digitare un nome di ruolo (ad esempio: *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="32c48-213">In hello **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="32c48-214">b.</span><span class="sxs-lookup"><span data-stu-id="32c48-214">b.</span></span> <span data-ttu-id="32c48-215">Fare clic su **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="32c48-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="32c48-216">In hello **Seleziona tipo di ruolo** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32c48-216">On hello **Select Role Type** dialog, perform hello following steps:</span></span> 
    
    ![Configura accesso Single Sign-On][18] 

    <span data-ttu-id="32c48-218">a.</span><span class="sxs-lookup"><span data-stu-id="32c48-218">a.</span></span> <span data-ttu-id="32c48-219">Selezionare **Role For Identity Provider Access**.</span><span class="sxs-lookup"><span data-stu-id="32c48-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="32c48-220">b.</span><span class="sxs-lookup"><span data-stu-id="32c48-220">b.</span></span> <span data-ttu-id="32c48-221">In hello **Grant Web Single Sign-On (WebSSO) provider tooSAML accesso** fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="32c48-221">In hello **Grant Web Single Sign-On (WebSSO) access tooSAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="32c48-222">In hello **stabilire Trust** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32c48-222">On hello **Establish Trust** dialog, perform hello following steps:</span></span>  
    
    ![Configura accesso Single Sign-On][19] 

    <span data-ttu-id="32c48-224">a.</span><span class="sxs-lookup"><span data-stu-id="32c48-224">a.</span></span> <span data-ttu-id="32c48-225">Come provider SAML, selezionare provider SAML hello creato in precedenza (ad esempio: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="32c48-225">As SAML provider, select hello SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="32c48-226">b.</span><span class="sxs-lookup"><span data-stu-id="32c48-226">b.</span></span> <span data-ttu-id="32c48-227">Fare clic su **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="32c48-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="32c48-228">In hello **verificare Trust ruolo** finestra di dialogo, fare clic su **passaggio successivo**.</span><span class="sxs-lookup"><span data-stu-id="32c48-228">On hello **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Configura accesso Single Sign-On][32]

19. <span data-ttu-id="32c48-230">In hello **collegare criteri** finestra di dialogo, fare clic su **passaggio successivo**.</span><span class="sxs-lookup"><span data-stu-id="32c48-230">On hello **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Configura accesso Single Sign-On][33]

20. <span data-ttu-id="32c48-232">In hello **revisione** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32c48-232">On hello **Review** dialog, perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On][34]
 
    <span data-ttu-id="32c48-234">a.</span><span class="sxs-lookup"><span data-stu-id="32c48-234">a.</span></span> <span data-ttu-id="32c48-235">Fare clic su **Crea ruolo**.</span><span class="sxs-lookup"><span data-stu-id="32c48-235">Click **Create Role**.</span></span>

    <span data-ttu-id="32c48-236">b.</span><span class="sxs-lookup"><span data-stu-id="32c48-236">b.</span></span> <span data-ttu-id="32c48-237">Creare tutti i ruoli in base alle esigenze ed eseguirne il mapping toohello Provider di identità.</span><span class="sxs-lookup"><span data-stu-id="32c48-237">Create as many roles as needed and map them toohello Identity Provider.</span></span>

21. <span data-ttu-id="32c48-238">Configurare tutti i ruoli di hello di AWS toofetch il provisioning degli utenti hello</span><span class="sxs-lookup"><span data-stu-id="32c48-238">Now configure hello user provisioning toofetch all hello roles from AWS</span></span>

    <span data-ttu-id="32c48-239">a.</span><span class="sxs-lookup"><span data-stu-id="32c48-239">a.</span></span> <span data-ttu-id="32c48-240">In accesso alla Console di AWS hello con l'account radice</span><span class="sxs-lookup"><span data-stu-id="32c48-240">In hello AWS Console login with your root account</span></span>

    <span data-ttu-id="32c48-241">b.</span><span class="sxs-lookup"><span data-stu-id="32c48-241">b.</span></span> <span data-ttu-id="32c48-242">In hello angolo superiore destro, fare clic sul nome e quindi fare clic su hello **le credenziali di sicurezza personale** opzione.</span><span class="sxs-lookup"><span data-stu-id="32c48-242">In hello top right corner click your name and then click hello **My Security Credentials** option.</span></span> <span data-ttu-id="32c48-243">Verrà aperta una schermata come messaggio di avviso.</span><span class="sxs-lookup"><span data-stu-id="32c48-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="32c48-244">Fare clic sul pulsante hello **le credenziali di sicurezza** toopass pulsante hello dello schermo.</span><span class="sxs-lookup"><span data-stu-id="32c48-244">Click hello button **Security Credentials** button toopass hello screen.</span></span>
        
       ![Configura accesso Single Sign-On][36]

       ![Configura accesso Single Sign-On][37]

    <span data-ttu-id="32c48-247">c.</span><span class="sxs-lookup"><span data-stu-id="32c48-247">c.</span></span> <span data-ttu-id="32c48-248">In hello chiavi di accesso fare clic su hello **Crea nuova chiave di accesso** pulsante.</span><span class="sxs-lookup"><span data-stu-id="32c48-248">In hello Access Keys section click hello **Create New Access Key** button.</span></span> <span data-ttu-id="32c48-249">Questo genera hello ID chiave di accesso e un valore di token.</span><span class="sxs-lookup"><span data-stu-id="32c48-249">This generates hello Access Key ID and a token value.</span></span>
    
       ![Configura accesso Single Sign-On][38]

    <span data-ttu-id="32c48-251">d.</span><span class="sxs-lookup"><span data-stu-id="32c48-251">d.</span></span> <span data-ttu-id="32c48-252">Copiare entrambi questi valori e scaricarli, in modo da non perderli.</span><span class="sxs-lookup"><span data-stu-id="32c48-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="32c48-253">e.</span><span class="sxs-lookup"><span data-stu-id="32c48-253">e.</span></span> <span data-ttu-id="32c48-254">In hello portale di Azure, nella pagina di integrazione dell'applicazione hello Amazon Web Services (AWS), fare clic su **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="32c48-254">In hello Azure Portal, on hello Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Configura accesso Single Sign-On][35]

    <span data-ttu-id="32c48-256">f.</span><span class="sxs-lookup"><span data-stu-id="32c48-256">f.</span></span> <span data-ttu-id="32c48-257">Impostare la modalità di Provisioning hello troppo**automatico**</span><span class="sxs-lookup"><span data-stu-id="32c48-257">Set hello Provisioning mode too**Automatic**</span></span>
        
       ![Configura accesso Single Sign-On][39]

    <span data-ttu-id="32c48-259">g.</span><span class="sxs-lookup"><span data-stu-id="32c48-259">g.</span></span> <span data-ttu-id="32c48-260">Ora in hello **clientsecret** e **segreto Token** incollare hello corrispondenti valori che è stato copiato dalla Console di AWS.</span><span class="sxs-lookup"><span data-stu-id="32c48-260">Now in hello **clientsecret** and **Secret Token** paste hello corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="32c48-261">h.</span><span class="sxs-lookup"><span data-stu-id="32c48-261">h.</span></span> <span data-ttu-id="32c48-262">È possibile fare clic su hello **Test connessione** pulsante connettività hello tootest.</span><span class="sxs-lookup"><span data-stu-id="32c48-262">You can click hello **Test Connection** button tootest hello connectivity.</span></span> <span data-ttu-id="32c48-263">Una volta che ha esito positivo è possibile avviare hello provisioning connettore.</span><span class="sxs-lookup"><span data-stu-id="32c48-263">Once that is successful then you can start hello provisioning connector.</span></span>
       
       ![Configura accesso Single Sign-On][40]

    <span data-ttu-id="32c48-265">i.</span><span class="sxs-lookup"><span data-stu-id="32c48-265">i.</span></span> <span data-ttu-id="32c48-266">Ora abilitare lo stato di Provisioning hello troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="32c48-266">Now enable hello Provisioning Status too**On**.</span></span> <span data-ttu-id="32c48-267">Verrà avviato il recupero dei ruoli hello da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="32c48-267">This starts fetching hello roles from hello application.</span></span>

       ![Configura accesso Single Sign-On][41]

    > [!NOTE]
    > <span data-ttu-id="32c48-269">Viene eseguito il servizio Azure Provisioning AD ogni dopo alcuni ruoli di hello ora toosync da AWS.</span><span class="sxs-lookup"><span data-stu-id="32c48-269">Azure AD Provisioning service runs every after some time toosync hello roles from AWS.</span></span> <span data-ttu-id="32c48-270">Dovrebbe essere hello tutti i Provider di identità associati ruoli AWS in Azure AD e di utilizzarli durante l'assegnazione toousers applicazione hello o gruppi.</span><span class="sxs-lookup"><span data-stu-id="32c48-270">You should see all hello Identity Provider attached AWS roles into Azure AD and you can use them while assigning hello application toousers or groups.</span></span>

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32c48-271">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32c48-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="32c48-272">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="32c48-272">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="32c48-274">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32c48-274">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="32c48-275">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="32c48-275">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32c48-277">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="32c48-277">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32c48-279">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="32c48-279">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32c48-281">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32c48-281">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32c48-283">a.</span><span class="sxs-lookup"><span data-stu-id="32c48-283">a.</span></span> <span data-ttu-id="32c48-284">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32c48-284">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32c48-285">b.</span><span class="sxs-lookup"><span data-stu-id="32c48-285">b.</span></span> <span data-ttu-id="32c48-286">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32c48-286">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32c48-287">c.</span><span class="sxs-lookup"><span data-stu-id="32c48-287">c.</span></span> <span data-ttu-id="32c48-288">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="32c48-288">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="32c48-289">d.</span><span class="sxs-lookup"><span data-stu-id="32c48-289">d.</span></span> <span data-ttu-id="32c48-290">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="32c48-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="32c48-291">Creazione di un utente test in Amazon Web Service</span><span class="sxs-lookup"><span data-stu-id="32c48-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="32c48-292">In ordine tooenable Azure AD utenti toolog in tooAmazon Web Services (AWS), è necessario che eseguirne il provisioning in Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="32c48-292">In order tooenable Azure AD users toolog in tooAmazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="32c48-293">In caso di hello di Amazon Web Services (AWS), il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="32c48-293">In hello case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="32c48-294">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32c48-294">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="32c48-295">Accedi tooyour **Amazon Web Services (AWS)** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="32c48-295">Log in tooyour **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="32c48-296">Fare clic su hello **Home Console** icona.</span><span class="sxs-lookup"><span data-stu-id="32c48-296">Click hello **Console Home** icon.</span></span> 
   
    ![Configura accesso Single Sign-On][11]

3. <span data-ttu-id="32c48-298">Fare clic su Identity and Access Management.</span><span class="sxs-lookup"><span data-stu-id="32c48-298">Click Identity and Access Management.</span></span> 
   
    ![Configura accesso Single Sign-On][28]

4. <span data-ttu-id="32c48-300">In hello Dashboard, fare clic su **utenti**, quindi fare clic su **creare nuovi utenti**.</span><span class="sxs-lookup"><span data-stu-id="32c48-300">In hello Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Configura accesso Single Sign-On][29]

5. <span data-ttu-id="32c48-302">Nella finestra di dialogo Crea utente hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32c48-302">On hello Create User dialog, perform hello following steps:</span></span> 
   
    ![Configura accesso Single Sign-On][30]   
    
    <span data-ttu-id="32c48-304">a.</span><span class="sxs-lookup"><span data-stu-id="32c48-304">a.</span></span> <span data-ttu-id="32c48-305">In hello **immettere i nomi utente** nelle caselle di testo, digitare il nome utente Brita Simon (userprincipalname) in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32c48-305">In hello **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="32c48-306">b.</span><span class="sxs-lookup"><span data-stu-id="32c48-306">b.</span></span> <span data-ttu-id="32c48-307">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="32c48-307">Click **Create.**</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="32c48-308">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="32c48-308">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="32c48-309">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooAmazon accesso Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="32c48-309">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAmazon Web Services (AWS).</span></span>

![Assegna utente][200] 

<span data-ttu-id="32c48-311">**tooassign Britta Simon tooAmazon Web Services (AWS), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32c48-311">**tooassign Britta Simon tooAmazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="32c48-312">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="32c48-312">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="32c48-314">Nell'elenco di applicazioni hello, selezionare **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="32c48-314">In hello applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="32c48-316">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="32c48-316">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="32c48-318">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="32c48-318">Click **Add** button.</span></span> <span data-ttu-id="32c48-319">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="32c48-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="32c48-321">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="32c48-321">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="32c48-322">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="32c48-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32c48-323">In **selezionare il ruolo** scheda, ruolo appropriato di hello selezionare per utente hello.</span><span class="sxs-lookup"><span data-stu-id="32c48-323">On **Select Role** tab, select hello appropriate role for hello user.</span></span> <span data-ttu-id="32c48-324">Tutti i ruoli vengono visualizzati con il nome di ruolo hello e il nome del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="32c48-324">All these roles are shown with hello role name and identity provider name.</span></span> <span data-ttu-id="32c48-325">In questo modo è possibile identificare facilmente i ruoli di hello da AWS.</span><span class="sxs-lookup"><span data-stu-id="32c48-325">This way you can easily identify hello roles from AWS.</span></span>

8. <span data-ttu-id="32c48-326">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="32c48-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32c48-327">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="32c48-327">Testing single sign-on</span></span>

<span data-ttu-id="32c48-328">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="32c48-328">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="32c48-329">Quando si fa clic hello Amazon Web Services (AWS) riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="32c48-329">When you click hello Amazon Web Services (AWS) tile in hello Access Panel, you should get automatically signed-on tooyour Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="32c48-330">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="32c48-330">Additional resources</span></span>

* [<span data-ttu-id="32c48-331">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32c48-331">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32c48-332">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32c48-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
