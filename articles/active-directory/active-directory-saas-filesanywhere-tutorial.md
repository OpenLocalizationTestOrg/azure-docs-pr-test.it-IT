---
title: 'Esercitazione: Integrazione di Azure Active Directory con FilesAnywhere | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e FilesAnywhere.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 4153056bd21006061c6ad8ff9cf3c17de9248628
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="2dba3-103">Esercitazione: Integrazione di Azure Active Directory con FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="2dba3-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="2dba3-104">Questa esercitazione descrive come integrare FilesAnywhere con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2dba3-104">In this tutorial, you learn how to integrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2dba3-105">L'integrazione di FilesAnywhere con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dba3-105">Integrating FilesAnywhere with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2dba3-106">È possibile controllare in Azure AD chi può accedere a FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="2dba3-106">You can control in Azure AD who has access to FilesAnywhere</span></span>
- <span data-ttu-id="2dba3-107">È possibile abilitare gli utenti per l'accesso automatico a FilesAnywhere (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dba3-107">You can enable your users to automatically get signed-on to FilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2dba3-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="2dba3-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2dba3-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2dba3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2dba3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2dba3-110">Prerequisites</span></span>

<span data-ttu-id="2dba3-111">Per configurare l'integrazione di Azure AD con FilesAnywhere, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dba3-111">To configure Azure AD integration with FilesAnywhere, you need the following items:</span></span>

- <span data-ttu-id="2dba3-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2dba3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2dba3-113">Sottoscrizione di FilesAnywhere abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2dba3-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="2dba3-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2dba3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="2dba3-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dba3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2dba3-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2dba3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2dba3-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2dba3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2dba3-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2dba3-118">Scenario description</span></span>
<span data-ttu-id="2dba3-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2dba3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2dba3-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dba3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2dba3-121">Aggiunta di FilesAnywhere dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2dba3-121">Adding FilesAnywhere from the gallery</span></span>
2. <span data-ttu-id="2dba3-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dba3-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-the-gallery"></a><span data-ttu-id="2dba3-123">Aggiungere FilesAnywhere dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2dba3-123">Adding FilesAnywhere from the gallery</span></span>
<span data-ttu-id="2dba3-124">Per configurare l'integrazione di FilesAnywhere in Azure AD, è necessario aggiungere FilesAnywhere dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2dba3-124">To configure the integration of FilesAnywhere into Azure AD, you need to add FilesAnywhere from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2dba3-125">**Per aggiungere FilesAnywhere dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2dba3-125">**To add FilesAnywhere from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2dba3-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2dba3-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2dba3-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2dba3-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2dba3-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2dba3-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2dba3-133">Nella casella di ricerca digitare **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-133">In the search box, type **FilesAnywhere**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="2dba3-135">Nel pannello dei risultati selezionare **FilesAnywhere** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2dba3-135">In the results panel, select **FilesAnywhere**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2dba3-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dba3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2dba3-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FilesAnywhere in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2dba3-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2dba3-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di FilesAnywhere che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2dba3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FilesAnywhere is to a user in Azure AD.</span></span> <span data-ttu-id="2dba3-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="2dba3-140">In other words, a link relationship between an Azure AD user and the related user in FilesAnywhere needs to be established.</span></span>

<span data-ttu-id="2dba3-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** di Azure AD come valore di **Username** (Nome utente) in FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="2dba3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="2dba3-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con FilesAnywhere, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dba3-142">To configure and test Azure AD single sign-on with FilesAnywhere, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2dba3-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2dba3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2dba3-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2dba3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2dba3-145">**[Creazione di un utente test di FilesAnywhere](#creating-a-filesanywhere-test-user)** : per avere una controparte di Britta Simon in FilesAnywhere collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2dba3-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - to have a counterpart of Britta Simon in FilesAnywhere that is linked to the Azure AD representation of her.</span></span>
3. <span data-ttu-id="2dba3-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2dba3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="2dba3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="2dba3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2dba3-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dba3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2dba3-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="2dba3-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="2dba3-150">**Per configurare l'accesso Single Sign-On di Azure AD con FilesAnywhere, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2dba3-150">**To configure Azure AD single sign-on with FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="2dba3-151">Nella pagina di integrazione dell'applicazione **FilesAnywhere** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-151">In the Azure Management portal, on the **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2dba3-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2dba3-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="2dba3-155">Nella sezione **URL e dominio FilesAnywhere**, se si vuole configurare l'applicazione in **modalità avviata da IDP**:</span><span class="sxs-lookup"><span data-stu-id="2dba3-155">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="2dba3-157">a.</span><span class="sxs-lookup"><span data-stu-id="2dba3-157">a.</span></span> <span data-ttu-id="2dba3-158">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="2dba3-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="2dba3-159">Si noti che il valore **215** di **clientid** è solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="2dba3-159">Please note that the value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="2dba3-160">È necessario sostituirlo con il valore clientid effettivo.</span><span class="sxs-lookup"><span data-stu-id="2dba3-160">You need to replace it with the actual clientid value.</span></span>

4. <span data-ttu-id="2dba3-161">Nella sezione **URL e dominio FilesAnywhere**, se si vuole configurare l'applicazione in **modalità avviata da SP**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2dba3-161">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="2dba3-163">a.</span><span class="sxs-lookup"><span data-stu-id="2dba3-163">a.</span></span> <span data-ttu-id="2dba3-164">Fare clic sull'opzione **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="2dba3-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="2dba3-165">b.</span><span class="sxs-lookup"><span data-stu-id="2dba3-165">b.</span></span> <span data-ttu-id="2dba3-166">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="2dba3-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2dba3-167">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="2dba3-167">Please note that these are not the real values.</span></span> <span data-ttu-id="2dba3-168">È necessario aggiornare questi valori con l'URL di accesso, l'ID e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="2dba3-168">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="2dba3-169">Per ottenere questi valori, contattare il [team di supporto di FilesAnywhere](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="2dba3-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) to get these values.</span></span> 

5. <span data-ttu-id="2dba3-170">L'applicazione FilesAnywhere si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="2dba3-170">FilesAnywhere Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="2dba3-171">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="2dba3-171">Please configure the following claims for this application.</span></span> <span data-ttu-id="2dba3-172">È possibile gestire i valori di questi attributi dalla sezione "**Attributi utente**" nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2dba3-172">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="2dba3-173">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="2dba3-173">The following screenshot shows an example for this.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="2dba3-175">Quando gli utenti si iscrivono a FilesAnywhere ricevono il valore dell'attributo **clientid** dal [team di FilesAnywhere](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="2dba3-175">When the users signs up with FilesAnywhere they get the value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="2dba3-176">È necessario aggiungere l'attributo "Client Id" con il valore univoco ricevuto da FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="2dba3-176">You have to add the "Client Id" attribute with the unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="2dba3-177">Tutti gli attributi indicati sopra sono obbligatori.</span><span class="sxs-lookup"><span data-stu-id="2dba3-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="2dba3-178">Si noti che il valore **2331** di **clientid** è solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="2dba3-178">Please note that the value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="2dba3-179">È necessario specificare il valore reale.</span><span class="sxs-lookup"><span data-stu-id="2dba3-179">You need to provide the actual value.</span></span>


6. <span data-ttu-id="2dba3-180">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come indicato nell'immagine precedente e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2dba3-180">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="2dba3-181">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="2dba3-181">Attribute Name</span></span> | <span data-ttu-id="2dba3-182">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="2dba3-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="2dba3-183">clientid</span><span class="sxs-lookup"><span data-stu-id="2dba3-183">clientid</span></span> | <span data-ttu-id="2dba3-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="2dba3-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="2dba3-185">a.</span><span class="sxs-lookup"><span data-stu-id="2dba3-185">a.</span></span> <span data-ttu-id="2dba3-186">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="2dba3-189">b.</span><span class="sxs-lookup"><span data-stu-id="2dba3-189">b.</span></span> <span data-ttu-id="2dba3-190">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="2dba3-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="2dba3-191">c.</span><span class="sxs-lookup"><span data-stu-id="2dba3-191">c.</span></span> <span data-ttu-id="2dba3-192">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="2dba3-192">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="2dba3-193">d.</span><span class="sxs-lookup"><span data-stu-id="2dba3-193">d.</span></span> <span data-ttu-id="2dba3-194">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="2dba3-194">Click **Ok**</span></span>

7. <span data-ttu-id="2dba3-195">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2dba3-195">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2dba3-197">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="2dba3-197">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="2dba3-199">Nella sezione **Configurazione di FilesAnywhere** fare clic su **Configura FilesAnywhere** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-199">On the **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** to open **Configure sign-on** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="2dba3-202">Per completare la configurazione dell'accesso Single Sign-On per l'applicazione sul lato FilesAnywhere, indicare al [team di supporto di FilesAnywhere](mailto:support@FilesAnywhere.com) il certificato di firma del token SAML scaricato e l'URL di Single Sign-On (SSO).</span><span class="sxs-lookup"><span data-stu-id="2dba3-202">To get SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them the downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2dba3-203">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dba3-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="2dba3-204">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dba3-204">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2dba3-206">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2dba3-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2dba3-207">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2dba3-207">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2dba3-209">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="2dba3-209">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2dba3-211">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-211">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2dba3-213">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2dba3-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2dba3-215">a.</span><span class="sxs-lookup"><span data-stu-id="2dba3-215">a.</span></span> <span data-ttu-id="2dba3-216">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2dba3-217">b.</span><span class="sxs-lookup"><span data-stu-id="2dba3-217">b.</span></span> <span data-ttu-id="2dba3-218">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2dba3-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2dba3-219">c.</span><span class="sxs-lookup"><span data-stu-id="2dba3-219">c.</span></span> <span data-ttu-id="2dba3-220">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2dba3-221">d.</span><span class="sxs-lookup"><span data-stu-id="2dba3-221">d.</span></span> <span data-ttu-id="2dba3-222">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="2dba3-223">Creare un utente test di FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="2dba3-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="2dba3-224">L'applicazione supporta il provisioning dell'utente just-in-time e dopo l'autenticazione gli utenti verranno automaticamente creati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2dba3-224">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2dba3-225">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2dba3-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2dba3-226">In questa sezione viene concesso a Britta Simon l'accesso a FilesAnywhere per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dba3-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FilesAnywhere.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2dba3-228">**Per assegnare Britta Simon a FilesAnywhere, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2dba3-228">**To assign Britta Simon to FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="2dba3-229">Nel portale di gestione di Azure aprire la visualizzazione con le applicazioni e quindi passare alla visualizzazione con le directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2dba3-231">Selezionare **FilesAnywhere** nell'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2dba3-231">In the applications list, select **FilesAnywhere**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="2dba3-233">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="2dba3-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2dba3-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-235">Click **Add** button.</span></span> <span data-ttu-id="2dba3-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2dba3-238">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="2dba3-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2dba3-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2dba3-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2dba3-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="2dba3-241">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2dba3-241">Testing single sign-on</span></span>

<span data-ttu-id="2dba3-242">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2dba3-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2dba3-243">Quando si fa clic sul riquadro FilesAnywhere nel Pannello di accesso, si dovrebbe accedere automaticamente all'applicazione FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="2dba3-243">When you click the FilesAnywhere tile in the Access Panel, you should get automatically signed-on to your FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2dba3-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2dba3-244">Additional resources</span></span>

* [<span data-ttu-id="2dba3-245">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2dba3-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2dba3-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2dba3-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
