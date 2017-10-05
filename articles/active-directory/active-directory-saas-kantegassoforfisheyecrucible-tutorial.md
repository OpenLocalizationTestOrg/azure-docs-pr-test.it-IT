---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kantega SSO for FishEye/Crucible | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Kantega SSO for FishEye/Crucible.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9eaa2ec661a3488b0bef1f6b7cc7a82290720054
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a><span data-ttu-id="d7a77-103">Esercitazione: Integrazione di Azure Active Directory con Kantega SSO for FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="d7a77-103">Tutorial: Azure Active Directory integration with Kantega SSO for FishEye/Crucible</span></span>

<span data-ttu-id="d7a77-104">Questa esercitazione descrive come integrare Kantega SSO for FishEye/Crucible con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7a77-104">In this tutorial, you learn how to integrate Kantega SSO for FishEye/Crucible with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7a77-105">L'integrazione di Kantega SSO for FishEye/Crucible con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d7a77-105">Integrating Kantega SSO for FishEye/Crucible with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d7a77-106">È possibile controllare in Azure AD chi può accedere a Kantega SSO for FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="d7a77-106">You can control in Azure AD who has access to Kantega SSO for FishEye/Crucible</span></span>
- <span data-ttu-id="d7a77-107">È possibile abilitare gli utenti per l'accesso automatico a Kantega SSO for FishEye/Crucible (Single Sign-On) con gli account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a77-107">You can enable your users to automatically get signed-on to Kantega SSO for FishEye/Crucible (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7a77-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a77-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d7a77-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7a77-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7a77-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d7a77-110">Prerequisites</span></span>

<span data-ttu-id="d7a77-111">Per configurare l'integrazione di Azure AD con Kantega SSO for FishEye/Crucible, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d7a77-111">To configure Azure AD integration with Kantega SSO for FishEye/Crucible, you need the following items:</span></span>

- <span data-ttu-id="d7a77-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7a77-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7a77-113">Sottoscrizione di Kantega SSO for FishEye/Crucible abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d7a77-113">A Kantega SSO for FishEye/Crucible single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7a77-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d7a77-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7a77-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d7a77-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7a77-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d7a77-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7a77-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7a77-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7a77-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d7a77-118">Scenario description</span></span>
<span data-ttu-id="d7a77-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d7a77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7a77-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d7a77-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7a77-121">Aggiunta di Kantega SSO for FishEye/Crucible dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d7a77-121">Adding Kantega SSO for FishEye/Crucible from the gallery</span></span>
2. <span data-ttu-id="d7a77-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a77-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-fisheyecrucible-from-the-gallery"></a><span data-ttu-id="d7a77-123">Aggiunta di Kantega SSO for FishEye/Crucible dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d7a77-123">Adding Kantega SSO for FishEye/Crucible from the gallery</span></span>
<span data-ttu-id="d7a77-124">Per configurare l'integrazione di Kantega SSO for FishEye/Crucible in Azure AD, è necessario aggiungere Kantega SSO for FishEye/Crucible dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d7a77-124">To configure the integration of Kantega SSO for FishEye/Crucible into Azure AD, you need to add Kantega SSO for FishEye/Crucible from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d7a77-125">**Per aggiungere Kantega SSO for FishEye/Crucible dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d7a77-125">**To add Kantega SSO for FishEye/Crucible from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d7a77-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d7a77-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d7a77-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d7a77-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d7a77-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d7a77-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d7a77-133">Nella casella di ricerca digitare **Kantega SSO for FishEye/Crucible**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-133">In the search box, type **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. <span data-ttu-id="d7a77-135">Nel pannello dei risultati selezionare **Kantega SSO for FishEye/Crucible** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d7a77-135">In the results panel, select **Kantega SSO for FishEye/Crucible**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7a77-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a77-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7a77-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kantega SSO for FishEye/Crucible mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d7a77-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d7a77-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve individuare l'utente di Kantega SSO for FishEye/Crucible corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7a77-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for FishEye/Crucible is to a user in Azure AD.</span></span> <span data-ttu-id="d7a77-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Kantega SSO for FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="d7a77-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for FishEye/Crucible needs to be established.</span></span>

<span data-ttu-id="d7a77-141">Per stabilire la relazione di collegamento, in Kantega SSO for FishEye/Crucible assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="d7a77-141">In Kantega SSO for FishEye/Crucible, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d7a77-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Kantega SSO for FishEye/Crucible, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d7a77-142">To configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d7a77-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d7a77-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d7a77-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7a77-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7a77-145">**[Creazione di un utente test di Kantega SSO for FishEye/Crucible](#creating-a-kantega-sso-for-fisheyecrucible-test-user)**: per avere una controparte di Britta Simon in Kantega SSO for FishEye/Crucible collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7a77-145">**[Creating a Kantega SSO for FishEye/Crucible test user](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for FishEye/Crucible that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7a77-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7a77-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7a77-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d7a77-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7a77-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a77-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7a77-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Kantega SSO for FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="d7a77-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for FishEye/Crucible application.</span></span>

<span data-ttu-id="d7a77-150">**Per configurare l'accesso Single Sign-On di Azure AD con Kantega SSO for FishEye/Crucible, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d7a77-150">**To configure Azure AD single sign-on with Kantega SSO for FishEye/Crucible, perform the following steps:**</span></span>

1. <span data-ttu-id="d7a77-151">Nella pagina di integrazione dell'applicazione **Kantega SSO for FishEye/Crucible** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-151">In the Azure portal, on the **Kantega SSO for FishEye/Crucible** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d7a77-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d7a77-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. <span data-ttu-id="d7a77-155">In modalità avviata **IDP** nella sezione **URL e dominio Kantega SSO for FishEye/Crucible** eseguire l'operazione seguente:</span><span class="sxs-lookup"><span data-stu-id="d7a77-155">In **IDP** initiated mode, on the **Kantega SSO for FishEye/Crucible Domain and URLs** section perform the following step :</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    <span data-ttu-id="d7a77-157">a.</span><span class="sxs-lookup"><span data-stu-id="d7a77-157">a.</span></span> <span data-ttu-id="d7a77-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="d7a77-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="d7a77-159">b.</span><span class="sxs-lookup"><span data-stu-id="d7a77-159">b.</span></span> <span data-ttu-id="d7a77-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="d7a77-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="d7a77-161">In modalità avviata **SP** selezionare **Mostra impostazioni URL avanzate** ed eseguire l'operazione seguente:</span><span class="sxs-lookup"><span data-stu-id="d7a77-161">In **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    <span data-ttu-id="d7a77-163">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="d7a77-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d7a77-164">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d7a77-164">These values are not real.</span></span> <span data-ttu-id="d7a77-165">aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="d7a77-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d7a77-166">Questi valori vengono ricevuti durante la configurazione del plug-in FishEye/Crucible descritto più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d7a77-166">These values are recieved during the configuration of FishEye/Crucible plugin which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="d7a77-167">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="d7a77-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. <span data-ttu-id="d7a77-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d7a77-169">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d7a77-171">In un'altra finestra del Web browser accedere al server locale FishEye/Crucible come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d7a77-171">In a different web browser window, log in to your FishEye/Crucible on premise server as an administrator.</span></span>

8. <span data-ttu-id="d7a77-172">Passare il puntatore del mouse sulla rotellina e scegliere **Add-ons** (Componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="d7a77-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. <span data-ttu-id="d7a77-174">Nella sezione System Settings (Impostazioni di sistema) fare clic su **Find new add-ons** (Trova nuovi componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="d7a77-174">Under System Settings section, click **Find new add-ons**.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. <span data-ttu-id="d7a77-176">Cercare **Kantega SSO for Crucible** e fare clic su **Install** (Installa) per installare il nuovo plug-in di SAML.</span><span class="sxs-lookup"><span data-stu-id="d7a77-176">Search **Kantega SSO for Crucible** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. <span data-ttu-id="d7a77-178">Viene avviata l'installazione del plug-in.</span><span class="sxs-lookup"><span data-stu-id="d7a77-178">The plugin installation starts.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. <span data-ttu-id="d7a77-180">Al termine dell'installazione,</span><span class="sxs-lookup"><span data-stu-id="d7a77-180">Once the installation is complete.</span></span> <span data-ttu-id="d7a77-181">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-181">Click **Close**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. <span data-ttu-id="d7a77-183">Fare clic su **Manage**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-183">Click **Manage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. <span data-ttu-id="d7a77-185">Fare clic su **Configure** (Configura) per configurare il nuovo plug-in.</span><span class="sxs-lookup"><span data-stu-id="d7a77-185">Click **Configure** to configure the new plugin.</span></span>    

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. <span data-ttu-id="d7a77-187">Nella sezione **SAML**</span><span class="sxs-lookup"><span data-stu-id="d7a77-187">In the **SAML** section.</span></span> <span data-ttu-id="d7a77-188">Selezionare **Azure Active Directory (Azure AD)** dall'elenco a discesa **Add identity provider** (Aggiungi provider di identità).</span><span class="sxs-lookup"><span data-stu-id="d7a77-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. <span data-ttu-id="d7a77-190">Selezionare il livello di sottoscrizione **Basic** (Di base).</span><span class="sxs-lookup"><span data-stu-id="d7a77-190">Select subscription level as **Basic**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. <span data-ttu-id="d7a77-192">Nella sezione **App properties** (Proprietà app) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d7a77-192">On the **App properties** section, perform following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    <span data-ttu-id="d7a77-194">a.</span><span class="sxs-lookup"><span data-stu-id="d7a77-194">a.</span></span> <span data-ttu-id="d7a77-195">Copiare il valore **URI ID app** e usarlo come **Identificatore, URL di risposta e URL di accesso** nella sezione **URL e dominio Kantega SSO for FishEye/Crucible** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a77-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for FishEye/Crucible Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="d7a77-196">b.</span><span class="sxs-lookup"><span data-stu-id="d7a77-196">b.</span></span> <span data-ttu-id="d7a77-197">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-197">Click **Next**.</span></span>

18. <span data-ttu-id="d7a77-198">Nella sezione **Metadata import** (Importazione metadati) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d7a77-198">On the **Metadata import** section, perform following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    <span data-ttu-id="d7a77-200">a.</span><span class="sxs-lookup"><span data-stu-id="d7a77-200">a.</span></span> <span data-ttu-id="d7a77-201">Selezionare **Metadata file on my computer** (File metadati in questo computer) e caricare il file di metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a77-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="d7a77-202">b.</span><span class="sxs-lookup"><span data-stu-id="d7a77-202">b.</span></span> <span data-ttu-id="d7a77-203">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-203">Click **Next**.</span></span>

19. <span data-ttu-id="d7a77-204">Nella sezione **Name and SSO location** (Nome e percorso SSO) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d7a77-204">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    <span data-ttu-id="d7a77-206">a.</span><span class="sxs-lookup"><span data-stu-id="d7a77-206">a.</span></span> <span data-ttu-id="d7a77-207">Aggiungere il nome del provider di identità nella casella di testo **Identity provider name** (Nome provider di identità), ad esempio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7a77-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="d7a77-208">b.</span><span class="sxs-lookup"><span data-stu-id="d7a77-208">b.</span></span> <span data-ttu-id="d7a77-209">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-209">Click **Next**.</span></span>

20. <span data-ttu-id="d7a77-210">Verificare il certificato di firma e fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="d7a77-210">Verify the Signing certificate and click **Next**.</span></span>  

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. <span data-ttu-id="d7a77-212">Nella sezione **FishEye user accounts** (Account utente FishEye) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d7a77-212">On the **FishEye user accounts** section, perform following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    <span data-ttu-id="d7a77-214">a.</span><span class="sxs-lookup"><span data-stu-id="d7a77-214">a.</span></span> <span data-ttu-id="d7a77-215">Selezionare **Create users in FishEye's internal Directory if needed** (Crea utenti nella directory interna di FishEye se necessario) e immettere il nome appropriato del gruppo per gli utenti (è possibile specificare più</span><span class="sxs-lookup"><span data-stu-id="d7a77-215">Select **Create users in FishEye's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="d7a77-216">gruppi separati da virgola).</span><span class="sxs-lookup"><span data-stu-id="d7a77-216">of groups separated by comma).</span></span>

    <span data-ttu-id="d7a77-217">b.</span><span class="sxs-lookup"><span data-stu-id="d7a77-217">b.</span></span> <span data-ttu-id="d7a77-218">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-218">Click **Next**.</span></span>

22. <span data-ttu-id="d7a77-219">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-219">Click **Finish**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. <span data-ttu-id="d7a77-221">Nella sezione **Known domains for Azure AD** (Domini noti per Azure AD) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d7a77-221">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    <span data-ttu-id="d7a77-223">a.</span><span class="sxs-lookup"><span data-stu-id="d7a77-223">a.</span></span> <span data-ttu-id="d7a77-224">Selezionare **Known domains** (Domini noti) dal pannello sinistro della pagina.</span><span class="sxs-lookup"><span data-stu-id="d7a77-224">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="d7a77-225">b.</span><span class="sxs-lookup"><span data-stu-id="d7a77-225">b.</span></span> <span data-ttu-id="d7a77-226">Immettere il nome di dominio nella casella di testo **Known domains** (Domini noti).</span><span class="sxs-lookup"><span data-stu-id="d7a77-226">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="d7a77-227">c.</span><span class="sxs-lookup"><span data-stu-id="d7a77-227">c.</span></span> <span data-ttu-id="d7a77-228">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-228">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="d7a77-229">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d7a77-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d7a77-230">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d7a77-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d7a77-231">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7a77-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7a77-232">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a77-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7a77-233">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a77-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d7a77-235">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d7a77-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d7a77-236">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d7a77-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7a77-238">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d7a77-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7a77-240">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7a77-242">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d7a77-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7a77-244">a.</span><span class="sxs-lookup"><span data-stu-id="d7a77-244">a.</span></span> <span data-ttu-id="d7a77-245">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7a77-246">b.</span><span class="sxs-lookup"><span data-stu-id="d7a77-246">b.</span></span> <span data-ttu-id="d7a77-247">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d7a77-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7a77-248">c.</span><span class="sxs-lookup"><span data-stu-id="d7a77-248">c.</span></span> <span data-ttu-id="d7a77-249">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d7a77-250">d.</span><span class="sxs-lookup"><span data-stu-id="d7a77-250">d.</span></span> <span data-ttu-id="d7a77-251">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a><span data-ttu-id="d7a77-252">Creazione di un utente test di Kantega SSO for FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="d7a77-252">Creating a Kantega SSO for FishEye/Crucible test user</span></span>

<span data-ttu-id="d7a77-253">Per consentire agli utenti di Azure AD di accedere a FishEye/Crucible, è necessario eseguire il provisioning degli utenti in FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="d7a77-253">To enable Azure AD users to log in to FishEye/Crucible, they must be provisioned into FishEye/Crucible.</span></span> <span data-ttu-id="d7a77-254">In Kantega SSO for FishEye/Crucible il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="d7a77-254">In Kantega SSO for FishEye/Crucible, provisioning is a manual task.</span></span>

<span data-ttu-id="d7a77-255">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d7a77-255">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d7a77-256">Accedere al server locale Crucible come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d7a77-256">Log in to your Crucible on premise server as an administrator.</span></span>

2. <span data-ttu-id="d7a77-257">Passare il puntatore del mouse sull'ingranaggio e fare clic su **Users** (Utenti).</span><span class="sxs-lookup"><span data-stu-id="d7a77-257">Hover on cog and click the **Users**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. <span data-ttu-id="d7a77-259">Nella scheda **Users** (Utenti) fare clic su **Add user** (Aggiungi utente).</span><span class="sxs-lookup"><span data-stu-id="d7a77-259">Under **Users** tab section, click **Add user**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. <span data-ttu-id="d7a77-261">Nella pagina della finestra di dialogo **Add New User** (Aggiungi nuovo utente) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d7a77-261">On the **Add New User** dialog page, perform the following steps:</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    <span data-ttu-id="d7a77-263">a.</span><span class="sxs-lookup"><span data-stu-id="d7a77-263">a.</span></span> <span data-ttu-id="d7a77-264">Nella casella di testo **Username** (Nome utente) digitare l'indirizzo di posta elettronica di un utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d7a77-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="d7a77-265">b.</span><span class="sxs-lookup"><span data-stu-id="d7a77-265">b.</span></span> <span data-ttu-id="d7a77-266">Nella casella di testo **Display Name** (Nome visualizzato) digitare il nome visualizzato dell'utente, ad esempio Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7a77-266">In the **Display Name** textbox, type display name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="d7a77-267">c.</span><span class="sxs-lookup"><span data-stu-id="d7a77-267">c.</span></span> <span data-ttu-id="d7a77-268">Nella casella di testo **Email address** (Indirizzo di posta elettronica) digitare l'indirizzo di posta elettronica dell'utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d7a77-268">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="d7a77-269">d.</span><span class="sxs-lookup"><span data-stu-id="d7a77-269">d.</span></span> <span data-ttu-id="d7a77-270">Nella casella di testo **Password** digitare la password dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d7a77-270">In the **Password** textbox, type the password of user.</span></span>  

    <span data-ttu-id="d7a77-271">e.</span><span class="sxs-lookup"><span data-stu-id="d7a77-271">e.</span></span> <span data-ttu-id="d7a77-272">Nella casella di testo **Confirm Password** (Conferma password) digitare di nuovo la password dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d7a77-272">In the **Confirm Password** textbox, reenter the password of user.</span></span>

    <span data-ttu-id="d7a77-273">f.</span><span class="sxs-lookup"><span data-stu-id="d7a77-273">f.</span></span> <span data-ttu-id="d7a77-274">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-274">Click **Add**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d7a77-275">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7a77-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d7a77-276">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Kantega SSO for FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="d7a77-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for FishEye/Crucible.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d7a77-278">**Per assegnare Britta Simon a Kantega SSO for FishEye/Crucible, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d7a77-278">**To assign Britta Simon to Kantega SSO for FishEye/Crucible, perform the following steps:**</span></span>

1. <span data-ttu-id="d7a77-279">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d7a77-281">Nell'elenco di applicazioni selezionare **Kantega SSO for FishEye/Crucible**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-281">In the applications list, select **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. <span data-ttu-id="d7a77-283">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d7a77-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d7a77-285">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-285">Click **Add** button.</span></span> <span data-ttu-id="d7a77-286">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d7a77-288">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d7a77-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d7a77-289">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7a77-290">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d7a77-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d7a77-291">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d7a77-291">Testing single sign-on</span></span>

<span data-ttu-id="d7a77-292">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d7a77-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d7a77-293">Quando si fa clic sul riquadro Kantega SSO for FishEye/Crucible nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Kantega SSO for FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="d7a77-293">When you click the Kantega SSO for FishEye/Crucible tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for FishEye/Crucible application.</span></span>
<span data-ttu-id="d7a77-294">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d7a77-294">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d7a77-295">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d7a77-295">Additional resources</span></span>

* [<span data-ttu-id="d7a77-296">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7a77-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7a77-297">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7a77-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

