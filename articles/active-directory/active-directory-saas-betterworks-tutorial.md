---
title: 'Esercitazione: Integrazione di Azure Active Directory con BetterWorks | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e BetterWorks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d6a5b167c0befbd0fe2c65bdd16abc35ed0a659c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="c3d57-103">Esercitazione: Integrazione di Azure Active Directory con BetterWorks</span><span class="sxs-lookup"><span data-stu-id="c3d57-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="c3d57-104">Questa esercitazione descrive come integrare BetterWorks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3d57-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3d57-105">L'integrazione di BetterWorks con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3d57-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c3d57-106">È possibile controllare in Azure AD chi può accedere a BetterWorks</span><span class="sxs-lookup"><span data-stu-id="c3d57-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="c3d57-107">È possibile abilitare gli utenti per l'accesso automatico a BetterWorks (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3d57-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3d57-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3d57-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c3d57-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3d57-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3d57-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c3d57-110">Prerequisites</span></span>

<span data-ttu-id="c3d57-111">Per configurare l'integrazione di Azure AD con BetterWorks, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3d57-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="c3d57-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3d57-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3d57-113">Sottoscrizione di BetterWorks abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c3d57-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3d57-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c3d57-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3d57-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3d57-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3d57-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c3d57-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3d57-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3d57-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3d57-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c3d57-118">Scenario description</span></span>
<span data-ttu-id="c3d57-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c3d57-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3d57-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3d57-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3d57-121">Aggiunta di BetterWorks dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c3d57-121">Adding BetterWorks from the gallery</span></span>
2. <span data-ttu-id="c3d57-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3d57-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="c3d57-123">Aggiunta di BetterWorks dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c3d57-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="c3d57-124">Per configurare l'integrazione di BetterWorks in Azure AD, è necessario aggiungere BetterWorks dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c3d57-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c3d57-125">**Per aggiungere BetterWorks dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c3d57-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c3d57-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c3d57-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c3d57-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c3d57-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c3d57-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3d57-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c3d57-133">Nella casella di ricerca digitare **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-133">In the search box, type **BetterWorks**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="c3d57-135">Nel pannello dei risultati selezionare **BetterWorks** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3d57-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3d57-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3d57-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3d57-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BetterWorks usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c3d57-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c3d57-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di BetterWorks corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3d57-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="c3d57-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="c3d57-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="c3d57-141">Per stabilire la relazione di collegamento, in BetterWorks assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="c3d57-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c3d57-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con BetterWorks, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3d57-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c3d57-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c3d57-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c3d57-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3d57-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3d57-145">**[Creazione di un utente di test di BetterWorks](#creating-a-betterworks-test-user)**: per avere una controparte di Britta Simon in BetterWorks collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3d57-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3d57-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3d57-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3d57-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c3d57-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3d57-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3d57-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3d57-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="c3d57-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="c3d57-150">**Per configurare l'accesso Single Sign-On di Azure AD con BetterWorks, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c3d57-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="c3d57-151">Nella pagina di integrazione dell'applicazione **BetterWorks** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c3d57-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c3d57-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="c3d57-155">Per configurare l'applicazione in **modalità avviata da IDP**, nella sezione **URL e dominio BetterWorks** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c3d57-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="c3d57-157">a.</span><span class="sxs-lookup"><span data-stu-id="c3d57-157">a.</span></span> <span data-ttu-id="c3d57-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="c3d57-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="c3d57-159">b.</span><span class="sxs-lookup"><span data-stu-id="c3d57-159">b.</span></span> <span data-ttu-id="c3d57-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="c3d57-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="c3d57-161">Per configurare l'applicazione in **modalità avviata da SP**, nella sezione **URL e dominio BetterWorks** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c3d57-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="c3d57-163">a.</span><span class="sxs-lookup"><span data-stu-id="c3d57-163">a.</span></span> <span data-ttu-id="c3d57-164">Fare clic su **Mostra impostazioni URL avanzate**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="c3d57-165">b.</span><span class="sxs-lookup"><span data-stu-id="c3d57-165">b.</span></span> <span data-ttu-id="c3d57-166">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="c3d57-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c3d57-167">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c3d57-167">These are not real values.</span></span> <span data-ttu-id="c3d57-168">è necessario aggiornarli con l'URL di risposta, l'ID e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="c3d57-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="c3d57-169">Per ottenere questi valori, contattare il [team di supporto di BetterWorks](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="c3d57-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
4. <span data-ttu-id="c3d57-170">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="c3d57-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="c3d57-172">L'applicazione BetterWorks si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="c3d57-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c3d57-173">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3d57-173">Configure the following claims for this application.</span></span> <span data-ttu-id="c3d57-174">È possibile gestire i valori di questi attributi dalla scheda **Attribute** (Attributo) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3d57-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="c3d57-175">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="c3d57-175">The following screenshot shows an example for this.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="c3d57-177">Nella finestra di dialogo **Attributi token SAML** seguire questa procedura per ciascuna riga della tabella:</span><span class="sxs-lookup"><span data-stu-id="c3d57-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="c3d57-178">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="c3d57-178">Attribute Name</span></span> | <span data-ttu-id="c3d57-179">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="c3d57-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="c3d57-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="c3d57-180">saml_token</span></span>     | <span data-ttu-id="c3d57-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="c3d57-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="c3d57-182">a.</span><span class="sxs-lookup"><span data-stu-id="c3d57-182">a.</span></span> <span data-ttu-id="c3d57-183">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="c3d57-186">b.</span><span class="sxs-lookup"><span data-stu-id="c3d57-186">b.</span></span> <span data-ttu-id="c3d57-187">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="c3d57-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="c3d57-188">c.</span><span class="sxs-lookup"><span data-stu-id="c3d57-188">c.</span></span> <span data-ttu-id="c3d57-189">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="c3d57-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="c3d57-190">d.</span><span class="sxs-lookup"><span data-stu-id="c3d57-190">d.</span></span> <span data-ttu-id="c3d57-191">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-191">Click **Ok**.</span></span>

7. <span data-ttu-id="c3d57-192">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c3d57-192">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c3d57-194">Per configurare l'accesso Single Sign-On sul lato **BetterWorks**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di BetterWorks](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="c3d57-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="c3d57-195">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c3d57-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c3d57-196">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c3d57-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c3d57-197">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3d57-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3d57-198">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3d57-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3d57-199">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3d57-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c3d57-201">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c3d57-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c3d57-202">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c3d57-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c3d57-204">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="c3d57-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c3d57-206">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3d57-208">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c3d57-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c3d57-210">a.</span><span class="sxs-lookup"><span data-stu-id="c3d57-210">a.</span></span> <span data-ttu-id="c3d57-211">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3d57-212">b.</span><span class="sxs-lookup"><span data-stu-id="c3d57-212">b.</span></span> <span data-ttu-id="c3d57-213">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c3d57-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c3d57-214">c.</span><span class="sxs-lookup"><span data-stu-id="c3d57-214">c.</span></span> <span data-ttu-id="c3d57-215">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c3d57-216">d.</span><span class="sxs-lookup"><span data-stu-id="c3d57-216">d.</span></span> <span data-ttu-id="c3d57-217">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="c3d57-218">Creazione di un utente di test per BetterWorks</span><span class="sxs-lookup"><span data-stu-id="c3d57-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="c3d57-219">In questa sezione viene creato un utente di nome Britta Simon in BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="c3d57-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="c3d57-220">Collaborare con il [team di supporto di BetterWorks](mailto:support@betterworks.com) per aggiungere gli utenti alla piattaforma BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="c3d57-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c3d57-221">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3d57-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c3d57-222">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="c3d57-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c3d57-224">**Per assegnare Britta Simon a BetterWorks, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c3d57-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="c3d57-225">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c3d57-227">Nell'elenco delle applicazioni selezionare **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-227">In the applications list, select **BetterWorks**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="c3d57-229">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c3d57-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c3d57-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-231">Click **Add** button.</span></span> <span data-ttu-id="c3d57-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c3d57-234">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c3d57-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c3d57-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3d57-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c3d57-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c3d57-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c3d57-237">Testing single sign-on</span></span>

<span data-ttu-id="c3d57-238">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c3d57-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c3d57-239">Quando si fa clic sul riquadro BetterWorks nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="c3d57-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3d57-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c3d57-240">Additional resources</span></span>

* [<span data-ttu-id="c3d57-241">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3d57-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3d57-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3d57-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

