---
title: 'Esercitazione: Integrazione di Azure Active Directory con StatusPage | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e StatusPage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: fa16cdec7b89404c140435fe57d5aa4b08cfa985
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="5e3ff-103">Esercitazione Integrazione di Azure Active Directory con StatusPage</span><span class="sxs-lookup"><span data-stu-id="5e3ff-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="5e3ff-104">Questa esercitazione descrive come integrare StatusPage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e3ff-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5e3ff-105">L'integrazione di StatusPage con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e3ff-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5e3ff-106">È possibile controllare in Azure AD chi può accedere a StatusPage</span><span class="sxs-lookup"><span data-stu-id="5e3ff-106">You can control in Azure AD who has access to StatusPage</span></span>
- <span data-ttu-id="5e3ff-107">È possibile abilitare gli utenti per l'accesso automatico a StatusPage (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e3ff-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5e3ff-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5e3ff-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5e3ff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e3ff-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5e3ff-110">Prerequisites</span></span>

<span data-ttu-id="5e3ff-111">Per configurare l'integrazione di Azure AD con StatusPage, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e3ff-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

- <span data-ttu-id="5e3ff-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5e3ff-113">Sottoscrizione di StatusPage abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5e3ff-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5e3ff-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5e3ff-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e3ff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5e3ff-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5e3ff-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5e3ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5e3ff-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5e3ff-118">Scenario description</span></span>
<span data-ttu-id="5e3ff-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5e3ff-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e3ff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5e3ff-121">Aggiunta di StatusPage dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="5e3ff-121">Adding StatusPage from the gallery</span></span>
2. <span data-ttu-id="5e3ff-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e3ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-the-gallery"></a><span data-ttu-id="5e3ff-123">Aggiunta di StatusPage dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="5e3ff-123">Adding StatusPage from the gallery</span></span>
<span data-ttu-id="5e3ff-124">Per configurare l'integrazione di StatusPage in Azure AD, è necessario aggiungere StatusPage dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5e3ff-125">**Per aggiungere StatusPage dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5e3ff-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5e3ff-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5e3ff-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5e3ff-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5e3ff-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5e3ff-133">Nella casella di ricerca digitare **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-133">In the search box, type **StatusPage**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="5e3ff-135">Nel pannello dei risultati selezionare **StatusPage** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5e3ff-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e3ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5e3ff-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con StatusPage in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5e3ff-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5e3ff-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di StatusPage che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span></span> <span data-ttu-id="5e3ff-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in StatusPage.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="5e3ff-141">Per stabilire la relazione di collegamento, in StatusPage assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5e3ff-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con StatusPage, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e3ff-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5e3ff-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5e3ff-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5e3ff-145">**[Creazione di un utente di test per StatusPage](#creating-a-statuspage-test-user)**: per avere una controparte di Britta Simon in StatusPage collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5e3ff-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5e3ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5e3ff-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e3ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5e3ff-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione StatusPage.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="5e3ff-150">**Per configurare l'accesso Single Sign-On di Azure AD con StatusPage, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5e3ff-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="5e3ff-151">Nella pagina di integrazione dell'applicazione **StatusPage** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5e3ff-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="5e3ff-155">Nella sezione **URL e dominio StatusPage** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5e3ff-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="5e3ff-157">a.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-157">a.</span></span> <span data-ttu-id="5e3ff-158">Nella casella di testo **Identificatore** digitare l'URL adottando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="5e3ff-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="5e3ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-159">b.</span></span> <span data-ttu-id="5e3ff-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="5e3ff-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="5e3ff-161">Per richiedere i metadati necessari per configurare l'accesso Single Sign-On, contattare il team di supporto di StatusPage all'indirizzo [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io).</span><span class="sxs-lookup"><span data-stu-id="5e3ff-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
    >
    ><span data-ttu-id="5e3ff-162">a.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-162">a.</span></span> <span data-ttu-id="5e3ff-163">Dal file di metadati, copiare il valore relativo all'autorità di certificazione e quindi incollarlo nella casella di testo **Identificatore** .</span><span class="sxs-lookup"><span data-stu-id="5e3ff-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="5e3ff-164">b.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-164">b.</span></span> <span data-ttu-id="5e3ff-165">Dal file di metadati copiare il valore relativo all'URL di risposta e quindi incollarlo nella casella di testo **Reply URL** .</span><span class="sxs-lookup"><span data-stu-id="5e3ff-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>

4. <span data-ttu-id="5e3ff-166">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="5e3ff-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5e3ff-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5e3ff-170">Nella sezione **Configurazione di StatusPage** fare clic su **Configura StatusPage** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5e3ff-171">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5e3ff-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="5e3ff-173">In un'altra finestra del browser accedere al sito aziendale di StatusPage come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-173">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="5e3ff-174">Nella barra degli strumenti principale scegliere **Manage Account**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-174">In the main toolbar, click **Manage Account**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="5e3ff-176">Fare clic sulla scheda **Single Sign-on** .</span><span class="sxs-lookup"><span data-stu-id="5e3ff-176">Click the **Single Sign-on** tab.</span></span> 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="5e3ff-178">Nella pagina di configurazione dell’accesso Single Sign-On, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5e3ff-178">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="5e3ff-181">a.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-181">a.</span></span> <span data-ttu-id="5e3ff-182">Nella casella di testo **SSO Target URL** (URL di destinazione SSO) incollare il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5e3ff-183">b.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-183">b.</span></span> <span data-ttu-id="5e3ff-184">Aprire il certificato scaricato nel Blocco note, copiarne il contenuto e incollarlo nella casella di testo **Certificato** .</span><span class="sxs-lookup"><span data-stu-id="5e3ff-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 

    <span data-ttu-id="5e3ff-185">c.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-185">c.</span></span> <span data-ttu-id="5e3ff-186">Fare clic su **SALVA CONFIGURAZIONE**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="5e3ff-187">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5e3ff-188">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5e3ff-189">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e3ff-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5e3ff-190">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e3ff-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="5e3ff-191">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5e3ff-193">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5e3ff-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5e3ff-194">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5e3ff-196">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5e3ff-198">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5e3ff-200">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5e3ff-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5e3ff-202">a.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-202">a.</span></span> <span data-ttu-id="5e3ff-203">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5e3ff-204">b.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-204">b.</span></span> <span data-ttu-id="5e3ff-205">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5e3ff-206">c.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-206">c.</span></span> <span data-ttu-id="5e3ff-207">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5e3ff-208">d.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-208">d.</span></span> <span data-ttu-id="5e3ff-209">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="5e3ff-210">Creazione di un utente test per StatusPage</span><span class="sxs-lookup"><span data-stu-id="5e3ff-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="5e3ff-211">Questa sezione descrive come creare un utente chiamato Britta Simon in StatusPage.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="5e3ff-212">StatusPage supporta il provisioning JIT (just-in-time),</span><span class="sxs-lookup"><span data-stu-id="5e3ff-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="5e3ff-213">È già stato abilitato in [Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="5e3ff-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="5e3ff-214">**Per creare un utente denominato Britta Simon in StatusPage, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5e3ff-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="5e3ff-215">Accedere al sito aziendale di StatusPage come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-215">Sign-on to your StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="5e3ff-216">Nel menu in alto fare clic su **Gestisci Account**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-216">In the menu on the top, click **Manage Account**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="5e3ff-218">Fare clic sulla scheda **Membri del team**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-218">Click the **Team Members** tab.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="5e3ff-220">Fare clic su **AGGIUNGI MEMBRO DEL TEAM**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="5e3ff-222">Digitare i valori **Indirizzo di posta elettronica**, **Nome** e **Cognome** di un utente valido di cui si vuole eseguire il provisioning nelle caselle di testo corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="5e3ff-224">Per **Ruolo** scegliere **Client Administrator** (Amministratore client).</span><span class="sxs-lookup"><span data-stu-id="5e3ff-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="5e3ff-225">Fare clic su **CREA ACCOUNT**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5e3ff-226">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e3ff-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5e3ff-227">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a StatusPage.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5e3ff-229">**Per assegnare Britta Simon a StatusPage, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5e3ff-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="5e3ff-230">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5e3ff-232">Nell'elenco di applicazioni selezionare **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-232">In the applications list, select **StatusPage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="5e3ff-234">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5e3ff-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-236">Click **Add** button.</span></span> <span data-ttu-id="5e3ff-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5e3ff-239">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5e3ff-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5e3ff-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5e3ff-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5e3ff-242">Testing single sign-on</span></span>

<span data-ttu-id="5e3ff-243">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5e3ff-244">Quando si fa clic sul riquadro StatusPage nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione StatusPage.</span><span class="sxs-lookup"><span data-stu-id="5e3ff-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5e3ff-245">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5e3ff-245">Additional resources</span></span>

* [<span data-ttu-id="5e3ff-246">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e3ff-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5e3ff-247">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e3ff-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

