---
title: 'Esercitazione: integrazione di Azure Active Directory con iLMS | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e iLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 22c72020200138e78835ed7dd2661f18b824c785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="0a263-103">Esercitazione: Integrazione di Azure Active Directory con iLMS</span><span class="sxs-lookup"><span data-stu-id="0a263-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="0a263-104">Questa esercitazione descrive come integrare iLMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a263-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a263-105">L'integrazione di iLMS con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a263-105">Integrating iLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a263-106">È possibile controllare in Azure AD chi può accedere a iLMS</span><span class="sxs-lookup"><span data-stu-id="0a263-106">You can control in Azure AD who has access to iLMS</span></span>
- <span data-ttu-id="0a263-107">È possibile abilitare gli utenti per l'accesso automatico a iLMS (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a263-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a263-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0a263-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a263-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a263-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a263-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0a263-110">Prerequisites</span></span>

<span data-ttu-id="0a263-111">Per configurare l'integrazione di Azure AD con iLMS sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a263-111">To configure Azure AD integration with iLMS, you need the following items:</span></span>

- <span data-ttu-id="0a263-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a263-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a263-113">Sottoscrizione di iLMS abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0a263-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a263-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0a263-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a263-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a263-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a263-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0a263-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0a263-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a263-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a263-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0a263-118">Scenario description</span></span>
<span data-ttu-id="0a263-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0a263-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a263-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a263-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a263-121">Aggiunta di iLMS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0a263-121">Adding iLMS from the gallery</span></span>
2. <span data-ttu-id="0a263-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a263-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-the-gallery"></a><span data-ttu-id="0a263-123">Aggiunta di iLMS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0a263-123">Adding iLMS from the gallery</span></span>
<span data-ttu-id="0a263-124">Per configurare l'integrazione di iLMS in Azure AD, è necessario aggiungere iLMS dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0a263-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a263-125">**Per aggiungere iLMS dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0a263-125">**To add iLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a263-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0a263-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a263-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0a263-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a263-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0a263-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0a263-131">Per aggiungere una nuova applicazione, fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0a263-131">To add new application, click **New application** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0a263-133">Nella casella di ricerca digitare **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="0a263-133">In the search box, type **iLMS**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="0a263-135">Nel pannello dei risultati selezionare **iLMS** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a263-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a263-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a263-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a263-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con iLMS in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0a263-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a263-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di iLMS che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a263-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span></span> <span data-ttu-id="0a263-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in iLMS.</span><span class="sxs-lookup"><span data-stu-id="0a263-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span></span>

<span data-ttu-id="0a263-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in iLMS.</span><span class="sxs-lookup"><span data-stu-id="0a263-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span></span>

<span data-ttu-id="0a263-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con iLMS, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a263-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a263-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0a263-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0a263-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a263-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a263-145">**[Creazione di un utente di test di iLMS](#creating-an-ilms-test-user)** : per avere una controparte di Britta Simon in iLMS collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a263-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="0a263-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a263-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a263-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="0a263-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a263-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a263-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a263-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione iLMS.</span><span class="sxs-lookup"><span data-stu-id="0a263-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="0a263-150">**Per configurare Single Sign-On di Azure AD con iLMS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0a263-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="0a263-151">Nella pagina di integrazione dell'applicazione **iLMS** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0a263-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0a263-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0a263-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="0a263-155">Nella sezione **URL e dominio iLMS** se si vuole configurare l'applicazione in modalità avviata da **IDP**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0a263-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="0a263-157">a.</span><span class="sxs-lookup"><span data-stu-id="0a263-157">a.</span></span> <span data-ttu-id="0a263-158">Nella casella di testo **Identificatore** incollare il valore **Identificatore** copiato dalla sezione **Provider di servizi** delle impostazioni SAML nel portale di amministrazione iLMS.</span><span class="sxs-lookup"><span data-stu-id="0a263-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="0a263-159">b.</span><span class="sxs-lookup"><span data-stu-id="0a263-159">b.</span></span> <span data-ttu-id="0a263-160">Nella casella di testo **URL di risposta** incollare il valore **Endpoint (URL)** copiato dalla sezione **Provider di servizi** delle impostazioni SAML nel portale di amministrazione iLMS con il modello seguente `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="0a263-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="0a263-161">Questo '123456' è un valore di esempio dell'identificatore.</span><span class="sxs-lookup"><span data-stu-id="0a263-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="0a263-162">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="0a263-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="0a263-164">Nella casella di testo **URL di accesso** incollare il valore **Endpoint (URL)** copiato dalla sezione **Provider di servizi** delle impostazioni SAML nel portale di amministrazione come `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="0a263-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="0a263-165">Per abilitare il provisioning JIT, l'applicazione iLMS si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="0a263-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0a263-166">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a263-166">Configure the following claims for this application.</span></span> <span data-ttu-id="0a263-167">È possibile gestire i valori di questi attributi dalla sezione **Attributi utente** nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a263-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="0a263-168">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="0a263-168">The following screenshot shows an example for this.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="0a263-170">Creare gli attributi **Department (Reparto), Region (Area)** e **Division** (Divisione) e aggiungere il nome di questi attributi in iLMS.</span><span class="sxs-lookup"><span data-stu-id="0a263-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span></span> <span data-ttu-id="0a263-171">Tutti gli attributi indicati sopra sono obbligatori.</span><span class="sxs-lookup"><span data-stu-id="0a263-171">All these attributes shown above are required.</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="0a263-172">È necessario abilitare **Create Un-recognized User Account** (Crea account utente non riconosciuto) in iLMS per eseguire il mapping di questi attributi.</span><span class="sxs-lookup"><span data-stu-id="0a263-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span></span> <span data-ttu-id="0a263-173">Seguire le istruzioni [qui](http://support.inspiredelearning.com/customer/portal/articles/2204526) per avere un'idea della configurazione degli attributi.</span><span class="sxs-lookup"><span data-stu-id="0a263-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span></span>

6. <span data-ttu-id="0a263-174">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come indicato nell'immagine precedente e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0a263-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="0a263-175">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="0a263-175">Attribute Name</span></span> | <span data-ttu-id="0a263-176">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="0a263-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="0a263-177">divisione</span><span class="sxs-lookup"><span data-stu-id="0a263-177">division</span></span> | <span data-ttu-id="0a263-178">user.department</span><span class="sxs-lookup"><span data-stu-id="0a263-178">user.department</span></span> |
    | <span data-ttu-id="0a263-179">region</span><span class="sxs-lookup"><span data-stu-id="0a263-179">region</span></span> | <span data-ttu-id="0a263-180">user.state</span><span class="sxs-lookup"><span data-stu-id="0a263-180">user.state</span></span> |
    | <span data-ttu-id="0a263-181">department</span><span class="sxs-lookup"><span data-stu-id="0a263-181">department</span></span> | <span data-ttu-id="0a263-182">user. jobtitle</span><span class="sxs-lookup"><span data-stu-id="0a263-182">user.jobtitle</span></span> |

    <span data-ttu-id="0a263-183">a.</span><span class="sxs-lookup"><span data-stu-id="0a263-183">a.</span></span> <span data-ttu-id="0a263-184">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="0a263-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="0a263-187">b.</span><span class="sxs-lookup"><span data-stu-id="0a263-187">b.</span></span> <span data-ttu-id="0a263-188">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="0a263-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="0a263-189">c.</span><span class="sxs-lookup"><span data-stu-id="0a263-189">c.</span></span> <span data-ttu-id="0a263-190">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="0a263-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0a263-191">d.</span><span class="sxs-lookup"><span data-stu-id="0a263-191">d.</span></span> <span data-ttu-id="0a263-192">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="0a263-192">Click **Ok**</span></span>

7. <span data-ttu-id="0a263-193">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="0a263-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="0a263-195">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0a263-195">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="0a263-197">In un'altra finestra del Web browser accedere al **portale di amministrazione di iLMS** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0a263-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="0a263-198">Fare clic su **SSO:SAML** nella scheda **Impostazioni** per aprire le impostazioni di SAML ed eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0a263-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="0a263-200">a.</span><span class="sxs-lookup"><span data-stu-id="0a263-200">a.</span></span> <span data-ttu-id="0a263-201">Espandere la sezione **Provider di servizi** e copiare l'**Identificatore** e il valore **Endpoint (URL)**.</span><span class="sxs-lookup"><span data-stu-id="0a263-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="0a263-203">b.</span><span class="sxs-lookup"><span data-stu-id="0a263-203">b.</span></span> <span data-ttu-id="0a263-204">Nella sezione **Provider di identità** fare clic su **Import metadata** (Importa metadati).</span><span class="sxs-lookup"><span data-stu-id="0a263-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="0a263-205">c.</span><span class="sxs-lookup"><span data-stu-id="0a263-205">c.</span></span> <span data-ttu-id="0a263-206">Selezionare il file **Metadati** scaricato dal portale di Azure dalla sezione **Certificato di firma SAML**.</span><span class="sxs-lookup"><span data-stu-id="0a263-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="0a263-208">d.</span><span class="sxs-lookup"><span data-stu-id="0a263-208">d.</span></span> <span data-ttu-id="0a263-209">Se si desidera abilitare il provisioning JIT per creare gli account iLMS per utenti non riconosciuti, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0a263-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="0a263-210">Selezionare **Create Un-recognized User Account** (Crea account utente non riconosciuto).</span><span class="sxs-lookup"><span data-stu-id="0a263-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="0a263-212">Eseguire il mapping degli attributi in Azure AD con gli attributi in iLMS.</span><span class="sxs-lookup"><span data-stu-id="0a263-212">Map the attributes in Azure AD with the attributes in iLMS.</span></span> <span data-ttu-id="0a263-213">Nella colonna dell'attributo specificare il nome degli attributi o il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="0a263-213">In the attribute column, specify the attributes name or the default value.</span></span>

    <span data-ttu-id="0a263-214">e.</span><span class="sxs-lookup"><span data-stu-id="0a263-214">e.</span></span> <span data-ttu-id="0a263-215">Passare alla scheda **Business Rules** (Regole Business) ed eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0a263-215">Go to **Business Rules** tab and perform the following steps:</span></span> 
        
       ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="0a263-217">Selezionare **Create Un-recognized Regions, Divisions and Departments** (Crea aree, divisioni e reparti non riconosciuti) per creare aree, divisioni e reparti che non esistono già al momento del Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="0a263-217">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="0a263-218">Selezionare **Update User Profile During Sign-in** (Aggiorna il profilo utente durante l'accesso) per specificare se il profilo dell'utente viene aggiornato ad ogni Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="0a263-218">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="0a263-219">Se l'opzione **"Update Blank Values for Non Mandatory Fields in User Profile"** (Aggiorna i valori vuoti per i campi non obbligatori nel profilo utente) è selezionata, i campi facoltativi del profilo vuoti al momento dell'accesso faranno sì che il profilo iLMS dell'utente contenga valori vuoti per quei campi.</span><span class="sxs-lookup"><span data-stu-id="0a263-219">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span></span>
        
       - <span data-ttu-id="0a263-220">Selezionare **Send Error Notification Email** (Invia una notifica di errore via posta elettronica) e immettere l'indirizzo di posta elettronica dell'utente a cui si desidera ricevere la notifica di errore.</span><span class="sxs-lookup"><span data-stu-id="0a263-220">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span></span>

11. <span data-ttu-id="0a263-221">Fare clic sul pulsante **Save** (Salva) per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="0a263-221">Click **Save** button to save the settings.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="0a263-223">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0a263-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a263-224">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="0a263-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a263-225">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a263-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a263-226">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a263-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a263-227">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a263-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0a263-229">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0a263-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a263-230">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0a263-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a263-232">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="0a263-232">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a263-234">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="0a263-234">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a263-236">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0a263-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a263-238">a.</span><span class="sxs-lookup"><span data-stu-id="0a263-238">a.</span></span> <span data-ttu-id="0a263-239">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a263-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a263-240">b.</span><span class="sxs-lookup"><span data-stu-id="0a263-240">b.</span></span> <span data-ttu-id="0a263-241">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a263-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a263-242">c.</span><span class="sxs-lookup"><span data-stu-id="0a263-242">c.</span></span> <span data-ttu-id="0a263-243">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="0a263-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a263-244">d.</span><span class="sxs-lookup"><span data-stu-id="0a263-244">d.</span></span> <span data-ttu-id="0a263-245">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0a263-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="0a263-246">Creazione di un utente test di iLMS</span><span class="sxs-lookup"><span data-stu-id="0a263-246">Creating an iLMS test user</span></span>

<span data-ttu-id="0a263-247">L'applicazione supporta il provisioning dell'utente just-in-time e dopo l'autenticazione gli utenti vengono automaticamente creati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a263-247">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="0a263-248">JIT funzionerà se si è fatto clic sulla casella di controllo **Create Un-recognized User Account** (Crea account utente non riconosciuto) durante l'impostazione di configurazione SAML presso il portale di amministrazione di iLMS.</span><span class="sxs-lookup"><span data-stu-id="0a263-248">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="0a263-249">Se è necessario creare manualmente un utente, seguire la seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="0a263-249">If you need to create an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="0a263-250">Accedere al sito aziendale di iLMS come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0a263-250">Log in to your iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="0a263-251">Fare clic su **"Register User"** (Registra utente) nella scheda **Users** (Utenti) per aprire la pagina **Register User** (Registra utente).</span><span class="sxs-lookup"><span data-stu-id="0a263-251">Click **“Register User”** under **Users** tab to open **Register User** page.</span></span> 
   
   ![Aggiungere un dipendente](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="0a263-253">Nella pagina **"Register User"** (Registra utente) eseguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="0a263-253">On the **“Register User”** page, perform the following steps.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="0a263-255">a.</span><span class="sxs-lookup"><span data-stu-id="0a263-255">a.</span></span> <span data-ttu-id="0a263-256">Nella casella di testo **First Name** (Nome) digitare Britta.</span><span class="sxs-lookup"><span data-stu-id="0a263-256">In the **First Name** textbox, type the first name Britta.</span></span>
   
    <span data-ttu-id="0a263-257">b.</span><span class="sxs-lookup"><span data-stu-id="0a263-257">b.</span></span> <span data-ttu-id="0a263-258">Nella casella di testo **Last name** (Cognome) digitare Simon.</span><span class="sxs-lookup"><span data-stu-id="0a263-258">In the **Last Name** textbox, type the last name Simon.</span></span>

    <span data-ttu-id="0a263-259">c.</span><span class="sxs-lookup"><span data-stu-id="0a263-259">c.</span></span> <span data-ttu-id="0a263-260">Nella casella di testo **ID email** (ID Posta elettronica) digitare l'indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a263-260">In the **Email ID** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="0a263-261">d.</span><span class="sxs-lookup"><span data-stu-id="0a263-261">d.</span></span> <span data-ttu-id="0a263-262">Dall'elenco a discesa **Region** (Area), selezionare il valore per l'area.</span><span class="sxs-lookup"><span data-stu-id="0a263-262">In the **Region** dropdown, select the value for region.</span></span>

    <span data-ttu-id="0a263-263">e.</span><span class="sxs-lookup"><span data-stu-id="0a263-263">e.</span></span> <span data-ttu-id="0a263-264">Dall'elenco a discesa **Division** (Divisione), selezionare il valore per la divisione.</span><span class="sxs-lookup"><span data-stu-id="0a263-264">In the **Division** dropdown, select the value for division.</span></span>

    <span data-ttu-id="0a263-265">f.</span><span class="sxs-lookup"><span data-stu-id="0a263-265">f.</span></span> <span data-ttu-id="0a263-266">Dall'elenco a discesa **Department** (Reparto), selezionare il valore per il reparto.</span><span class="sxs-lookup"><span data-stu-id="0a263-266">In the **Department** dropdown, select the value for department.</span></span>

    <span data-ttu-id="0a263-267">g.</span><span class="sxs-lookup"><span data-stu-id="0a263-267">g.</span></span> <span data-ttu-id="0a263-268">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0a263-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a263-269">È possibile inviare all'utente un messaggio di registrazione selezionando la casella di controllo **Send Registration Mail** (Invia email di registrazione).</span><span class="sxs-lookup"><span data-stu-id="0a263-269">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0a263-270">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a263-270">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0a263-271">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a iLMS.</span><span class="sxs-lookup"><span data-stu-id="0a263-271">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0a263-273">**Per assegnare Britta Simon a iLMS seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0a263-273">**To assign Britta Simon to iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="0a263-274">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0a263-274">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0a263-276">Nell'elenco delle applicazioni selezionare **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="0a263-276">In the applications list, select **iLMS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="0a263-278">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0a263-278">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0a263-280">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0a263-280">Click **Add** button.</span></span> <span data-ttu-id="0a263-281">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0a263-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0a263-283">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="0a263-283">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0a263-284">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0a263-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a263-285">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0a263-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a263-286">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0a263-286">Testing single sign-on</span></span>

<span data-ttu-id="0a263-287">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0a263-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0a263-288">Quando si fa clic sul riquadro iLMS nel pannello di accesso, si accederà automaticamente all'applicazione iLMS.</span><span class="sxs-lookup"><span data-stu-id="0a263-288">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a263-289">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0a263-289">Additional resources</span></span>

* [<span data-ttu-id="0a263-290">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a263-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a263-291">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a263-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

