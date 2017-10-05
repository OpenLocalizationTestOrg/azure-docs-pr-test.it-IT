---
title: 'Esercitazione: Integrazione di Azure Active Directory con NetDocuments | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e NetDocuments.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 87c3338d611daa837aa5f079c4b68e0e6fc58455
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="60bd2-103">Esercitazione: Integrazione di Azure Active Directory con NetDocuments</span><span class="sxs-lookup"><span data-stu-id="60bd2-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="60bd2-104">Questa esercitazione descrive come integrare NetDocuments con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60bd2-104">In this tutorial, you learn how to integrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60bd2-105">L'integrazione di NetDocuments con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="60bd2-105">Integrating NetDocuments with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60bd2-106">È possibile controllare in Azure AD chi può accedere a NetDocuments</span><span class="sxs-lookup"><span data-stu-id="60bd2-106">You can control in Azure AD who has access to NetDocuments</span></span>
- <span data-ttu-id="60bd2-107">È possibile abilitare gli utenti per l'accesso automatico a NetDocuments (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="60bd2-107">You can enable your users to automatically get signed-on to NetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60bd2-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60bd2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="60bd2-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="60bd2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60bd2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="60bd2-110">Prerequisites</span></span>

<span data-ttu-id="60bd2-111">Per configurare l'integrazione di Azure AD con NetDocuments, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="60bd2-111">To configure Azure AD integration with NetDocuments, you need the following items:</span></span>

- <span data-ttu-id="60bd2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60bd2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60bd2-113">Sottoscrizione di NetDocuments abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="60bd2-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60bd2-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="60bd2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60bd2-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="60bd2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60bd2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="60bd2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60bd2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60bd2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60bd2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="60bd2-118">Scenario description</span></span>
<span data-ttu-id="60bd2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="60bd2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60bd2-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="60bd2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60bd2-121">Aggiunta di NetDocuments dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="60bd2-121">Adding NetDocuments from the gallery</span></span>
2. <span data-ttu-id="60bd2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60bd2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-the-gallery"></a><span data-ttu-id="60bd2-123">Aggiunta di NetDocuments dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="60bd2-123">Adding NetDocuments from the gallery</span></span>
<span data-ttu-id="60bd2-124">Per configurare l'integrazione di NetDocuments in Azure AD, è necessario aggiungere NetDocuments dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="60bd2-124">To configure the integration of NetDocuments into Azure AD, you need to add NetDocuments from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60bd2-125">**Per aggiungere NetDocuments dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="60bd2-125">**To add NetDocuments from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60bd2-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="60bd2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="60bd2-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60bd2-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="60bd2-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="60bd2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="60bd2-133">Nella casella di ricerca digitare **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-133">In the search box, type **NetDocuments**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="60bd2-135">Nel pannello dei risultati selezionare **NetDocuments** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="60bd2-135">In the results panel, select **NetDocuments**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60bd2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60bd2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60bd2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con NetDocuments usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="60bd2-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="60bd2-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di NetDocuments corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60bd2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in NetDocuments is to a user in Azure AD.</span></span> <span data-ttu-id="60bd2-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="60bd2-140">In other words, a link relationship between an Azure AD user and the related user in NetDocuments needs to be established.</span></span>

<span data-ttu-id="60bd2-141">Per stabilire la relazione di collegamento, in NetDocuments assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="60bd2-141">In NetDocuments, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="60bd2-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con NetDocuments, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="60bd2-142">To configure and test Azure AD single sign-on with NetDocuments, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60bd2-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="60bd2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="60bd2-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60bd2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60bd2-145">**[Creazione di un utente di test di NetDocuments](#creating-a-netdocuments-test-user)**: per avere una controparte di Britta Simon in NetDocuments collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60bd2-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - to have a counterpart of Britta Simon in NetDocuments that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="60bd2-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60bd2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60bd2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="60bd2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60bd2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60bd2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60bd2-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="60bd2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="60bd2-150">**Per configurare l'accesso Single Sign-On di Azure AD con NetDocuments, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="60bd2-150">**To configure Azure AD single sign-on with NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="60bd2-151">Nella pagina di integrazione dell'applicazione **NetDocuments** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-151">In the Azure portal, on the **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="60bd2-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="60bd2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="60bd2-155">Nella sezione **URL e dominio NetDocuments** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="60bd2-155">On the **NetDocuments Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="60bd2-157">a.</span><span class="sxs-lookup"><span data-stu-id="60bd2-157">a.</span></span> <span data-ttu-id="60bd2-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`.</span><span class="sxs-lookup"><span data-stu-id="60bd2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="60bd2-159">b.</span><span class="sxs-lookup"><span data-stu-id="60bd2-159">b.</span></span> <span data-ttu-id="60bd2-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="60bd2-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="60bd2-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="60bd2-161">These values are not real.</span></span> <span data-ttu-id="60bd2-162">è necessario aggiornarli con l'URL di accesso e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="60bd2-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="60bd2-163">Per ottenere questi valori, contattare il [team di supporto clienti di NetDocuments](https://support.netdocuments.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="60bd2-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) to get these values.</span></span>
 
4. <span data-ttu-id="60bd2-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="60bd2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="60bd2-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="60bd2-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="60bd2-168">In un'altra finestra del Web browser accedere al sito aziendale di NetDocuments come amministratore.</span><span class="sxs-lookup"><span data-stu-id="60bd2-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="60bd2-169">Passare alla pagina **Admin**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-169">Go to **Admin**.</span></span>

8. <span data-ttu-id="60bd2-170">Fare clic su **Aggiungi e rimuovi utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="60bd2-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span><span class="sxs-lookup"><span data-stu-id="60bd2-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="60bd2-172">Fare clic su **Configura opzioni di autenticazione avanzata**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="60bd2-173">![Configurare opzioni di autenticazione avanzata](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configurare opzioni di autenticazione avanzata")</span><span class="sxs-lookup"><span data-stu-id="60bd2-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="60bd2-174">Nella finestra di dialogo della **identità federata** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="60bd2-174">On the **Federated Identity** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="60bd2-175">![Identità federata](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identità federata")</span><span class="sxs-lookup"><span data-stu-id="60bd2-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="60bd2-176">a.</span><span class="sxs-lookup"><span data-stu-id="60bd2-176">a.</span></span> <span data-ttu-id="60bd2-177">Come **Federated identity server type** (Tipo di server identità federata) selezionare **Active Directory Federation Services**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="60bd2-178">b.</span><span class="sxs-lookup"><span data-stu-id="60bd2-178">b.</span></span> <span data-ttu-id="60bd2-179">Fare clic su **Choose File** (Scegli file) per caricare il file di metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60bd2-179">Click **Choose file**, to upload the downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="60bd2-180">c.</span><span class="sxs-lookup"><span data-stu-id="60bd2-180">c.</span></span> <span data-ttu-id="60bd2-181">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="60bd2-182">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="60bd2-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="60bd2-183">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="60bd2-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="60bd2-184">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60bd2-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60bd2-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60bd2-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="60bd2-186">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60bd2-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="60bd2-188">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="60bd2-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60bd2-189">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="60bd2-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60bd2-191">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="60bd2-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60bd2-193">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60bd2-195">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="60bd2-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60bd2-197">a.</span><span class="sxs-lookup"><span data-stu-id="60bd2-197">a.</span></span> <span data-ttu-id="60bd2-198">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60bd2-199">b.</span><span class="sxs-lookup"><span data-stu-id="60bd2-199">b.</span></span> <span data-ttu-id="60bd2-200">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="60bd2-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60bd2-201">c.</span><span class="sxs-lookup"><span data-stu-id="60bd2-201">c.</span></span> <span data-ttu-id="60bd2-202">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="60bd2-203">d.</span><span class="sxs-lookup"><span data-stu-id="60bd2-203">d.</span></span> <span data-ttu-id="60bd2-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="60bd2-205">Creazione di un utente di test di NetDocuments</span><span class="sxs-lookup"><span data-stu-id="60bd2-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="60bd2-206">Per consentire agli utenti di Azure AD di accedere a NetDocuments, è necessario effettuarne il provisioning in NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="60bd2-206">To enable Azure AD users to log in to NetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="60bd2-207">Nel caso di NetDocuments, il provisioning è un’attività manuale.</span><span class="sxs-lookup"><span data-stu-id="60bd2-207">In the case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="60bd2-208">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="60bd2-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="60bd2-209">Accedere al sito aziendale di **NetDocuments** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="60bd2-209">Sing on to your **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="60bd2-210">Nel menu in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-210">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="60bd2-211">![Amministratore](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="60bd2-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="60bd2-212">Fare clic su **Aggiungi e rimuovi utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="60bd2-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span><span class="sxs-lookup"><span data-stu-id="60bd2-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="60bd2-214">Nella casella di testo **Email Address** (Indirizzo di posta elettronica) digitare l'indirizzo di posta elettronica di un account valido di Azure Active Directory di cui eseguire il provisioning, quindi fare clic su **Add User** (Aggiungi utente).</span><span class="sxs-lookup"><span data-stu-id="60bd2-214">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="60bd2-215">![Indirizzo di posta elettronica](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Indirizzo di posta elettronica")</span><span class="sxs-lookup"><span data-stu-id="60bd2-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="60bd2-216">Il titolare dell'account di Azure Active Directory riceverà un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="60bd2-216">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span></span> <span data-ttu-id="60bd2-217">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da NetDocuments per eseguire il provisioning degli account utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60bd2-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="60bd2-218">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60bd2-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="60bd2-219">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="60bd2-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetDocuments.</span></span>

![Assegna utente][200] 

<span data-ttu-id="60bd2-221">**Per assegnare Britta Simon a NetDocuments, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="60bd2-221">**To assign Britta Simon to NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="60bd2-222">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="60bd2-224">Nell'elenco delle applicazioni selezionare **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-224">In the applications list, select **NetDocuments**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="60bd2-226">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="60bd2-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="60bd2-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-228">Click **Add** button.</span></span> <span data-ttu-id="60bd2-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="60bd2-231">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="60bd2-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="60bd2-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60bd2-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="60bd2-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="60bd2-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="60bd2-234">Testing single sign-on</span></span>

<span data-ttu-id="60bd2-235">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="60bd2-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60bd2-236">Quando si fa clic sul riquadro NetDocuments nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="60bd2-236">When you click the NetDocuments tile in the Access Panel, you should get automatically signed-on to your NetDocuments application.</span></span>
<span data-ttu-id="60bd2-237">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="60bd2-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60bd2-238">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="60bd2-238">Additional resources</span></span>

* [<span data-ttu-id="60bd2-239">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60bd2-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60bd2-240">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60bd2-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

