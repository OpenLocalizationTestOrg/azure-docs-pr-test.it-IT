---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cerner Central | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Cerner Central.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 77b5fb94cdfa5722081198aabc59fbf86229c2b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="7e594-103">Esercitazione: Integrazione di Azure Active Directory con Central Desktop</span><span class="sxs-lookup"><span data-stu-id="7e594-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="7e594-104">Questa esercitazione descrive come integrare Cerner Central con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e594-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e594-105">L'integrazione di Cerner Central con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e594-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7e594-106">È possibile controllare in Azure AD chi può accedere a Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="7e594-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="7e594-107">È possibile abilitare gli utenti per l'accesso automatico a Cerner Central (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e594-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7e594-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e594-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7e594-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e594-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e594-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7e594-110">Prerequisites</span></span>

<span data-ttu-id="7e594-111">Per configurare l'integrazione di Azure AD con Cerner Central, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e594-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="7e594-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e594-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e594-113">Account di sistema Cerner Central approvato</span><span class="sxs-lookup"><span data-stu-id="7e594-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="7e594-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7e594-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e594-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e594-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e594-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7e594-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e594-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e594-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e594-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7e594-118">Scenario description</span></span>
<span data-ttu-id="7e594-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7e594-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e594-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e594-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e594-121">Aggiunta di Cerner Central dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7e594-121">Adding Cerner Central from the gallery</span></span>
2. <span data-ttu-id="7e594-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e594-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="7e594-123">Aggiunta di Cerner Central dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7e594-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="7e594-124">Per configurare l'integrazione di Cerner Central in Azure AD, è necessario aggiungere Cerner Central dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7e594-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7e594-125">**Per aggiungere Cerner Central dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7e594-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7e594-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7e594-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7e594-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7e594-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7e594-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7e594-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7e594-131">Per aggiungere una nuova applicazione, fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7e594-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7e594-133">Nella casella di ricerca digitare **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="7e594-133">In the search box, type **Cerner Central**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="7e594-135">Nel pannello dei risultati selezionare **Cerner Central** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7e594-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7e594-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e594-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7e594-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Cerner Central in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7e594-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7e594-139">Per il corretto funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Cerner Central che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e594-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="7e594-140">Deve essere stabilita, in altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="7e594-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="7e594-141">Per configurare e testare l'accesso Single Sign-On di Azure AD con Cerner Central, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e594-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7e594-142">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7e594-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7e594-143">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e594-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e594-144">**[Creazione di un utente di test Cerner Central](#creating-a-cerner-central-test-user)**: per avere una controparte di Britta Simon in Cerner Central collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e594-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="7e594-145">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e594-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e594-146">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="7e594-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7e594-147">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e594-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7e594-148">In questa sezione si abilita l'accesso Single Sign-On di Azure AD nel portale di Azure e si configura l'accesso Single Sign-On nell'applicazione Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="7e594-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="7e594-149">**Per configurare l'accesso Single Sign-On di Azure AD con Cerner Central, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7e594-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="7e594-150">Nella pagina di integrazione dell'applicazione **Cerner Central** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7e594-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7e594-152">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7e594-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="7e594-154">Nella sezione **URL e dominio Cerner Central** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7e594-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="7e594-156">a.</span><span class="sxs-lookup"><span data-stu-id="7e594-156">a.</span></span> <span data-ttu-id="7e594-157">Nella casella di testo **Identificatore** digitare il valore adottando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="7e594-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="7e594-158">b.</span><span class="sxs-lookup"><span data-stu-id="7e594-158">b.</span></span> <span data-ttu-id="7e594-159">Nella casella di testo **URL di risposta** digitare l'URL usando i modelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e594-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="7e594-160">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="7e594-160">These values are not the real.</span></span> <span data-ttu-id="7e594-161">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="7e594-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="7e594-162">Per ottenere questi valori, contattare il [team di supporto di Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="7e594-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>
 
4. <span data-ttu-id="7e594-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7e594-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="7e594-165">Per generare l'URL dei **metadati**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7e594-165">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="7e594-166">a.</span><span class="sxs-lookup"><span data-stu-id="7e594-166">a.</span></span> <span data-ttu-id="7e594-167">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="7e594-167">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="7e594-169">b.</span><span class="sxs-lookup"><span data-stu-id="7e594-169">b.</span></span> <span data-ttu-id="7e594-170">Fare clic su **Endpoint** per aprire la finestra di dialogo **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="7e594-170">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="7e594-172">c.</span><span class="sxs-lookup"><span data-stu-id="7e594-172">c.</span></span> <span data-ttu-id="7e594-173">Fare clic sul pulsante Copia per copiare l'URL del **DOCUMENTO METADATI FEDERAZIONE** e incollarlo nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="7e594-173">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="7e594-175">d.</span><span class="sxs-lookup"><span data-stu-id="7e594-175">d.</span></span> <span data-ttu-id="7e594-176">Passare ora alla pagina delle proprietà di **Cerner Central** e copiare l'**ID applicazione** usando il pulsante **Copia** e incollarlo nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="7e594-176">Now go to the property page of **Cerner Central** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="7e594-178">e.</span><span class="sxs-lookup"><span data-stu-id="7e594-178">e.</span></span> <span data-ttu-id="7e594-179">Generare l'**URL dei metadati** usando il modello seguente: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="7e594-179">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="7e594-180">Per configurare l'accesso Single Sign-On sul lato **Cerner Central**, occorre inviare l'**URL dei metadati** al [Supporto di Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="7e594-180">To configure single sign-on on **Cerner Central** side, you need to send the **Metadata URL** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="7e594-181">Il supporto configura l'accesso SSO sul lato applicazione per completare l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="7e594-181">They configure the SSO on application side to complete the integration.</span></span>

> [!TIP]
> <span data-ttu-id="7e594-182">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="7e594-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7e594-183">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="7e594-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7e594-184">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e594-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7e594-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e594-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="7e594-186">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e594-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span> 

![Creare un utente di Azure AD][100]

<span data-ttu-id="7e594-188">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7e594-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7e594-189">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7e594-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7e594-191">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="7e594-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7e594-193">Per aprire la finestra di dialogo **Utente**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7e594-193">To open the **User** dialog, click **Add**.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7e594-195">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7e594-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7e594-197">a.</span><span class="sxs-lookup"><span data-stu-id="7e594-197">a.</span></span> <span data-ttu-id="7e594-198">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e594-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e594-199">b.</span><span class="sxs-lookup"><span data-stu-id="7e594-199">b.</span></span> <span data-ttu-id="7e594-200">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e594-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="7e594-201">c.</span><span class="sxs-lookup"><span data-stu-id="7e594-201">c.</span></span> <span data-ttu-id="7e594-202">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="7e594-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7e594-203">d.</span><span class="sxs-lookup"><span data-stu-id="7e594-203">d.</span></span> <span data-ttu-id="7e594-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7e594-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="7e594-205">Creazione di un utente test di Cerner Central</span><span class="sxs-lookup"><span data-stu-id="7e594-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="7e594-206">L'applicazione **Cerner Central** consente l'autenticazione da qualsiasi provider di identità federato.</span><span class="sxs-lookup"><span data-stu-id="7e594-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="7e594-207">Se un utente è in grado di accedere alla home page dell'applicazione, viene federato e non è più necessario il provisioning manuale.</span><span class="sxs-lookup"><span data-stu-id="7e594-207">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7e594-208">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e594-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7e594-209">In questa sezione si abilita Britta Simon per l'uso dell'accesso Single Sign-On di Azure, concedendole l'accesso a Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="7e594-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7e594-211">**Per assegnare Britta Simon a Cerner Central, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7e594-211">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="7e594-212">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7e594-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7e594-214">Nell'elenco delle applicazioni selezionare **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="7e594-214">In the applications list, select **Cerner Central**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="7e594-216">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7e594-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7e594-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7e594-218">Click **Add** button.</span></span> <span data-ttu-id="7e594-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7e594-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7e594-221">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="7e594-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7e594-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7e594-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e594-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7e594-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7e594-224">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7e594-224">Testing single sign-on</span></span>

<span data-ttu-id="7e594-225">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7e594-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7e594-226">Quando si fa clic sul riquadro Cerner Central nel pannello di accesso, si accede automaticamente all'applicazione Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="7e594-226">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="7e594-227">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e594-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e594-228">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7e594-228">Additional resources</span></span>

* [<span data-ttu-id="7e594-229">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e594-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e594-230">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e594-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

