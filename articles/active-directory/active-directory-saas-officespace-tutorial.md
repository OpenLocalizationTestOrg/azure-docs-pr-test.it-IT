---
title: 'Esercitazione: Integrazione di Azure Active Directory con OfficeSpace Software | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e OfficeSpace Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 43d2ecfe851d8f6c43cd4ce7fc4bd872818f4137
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="12c6c-103">Esercitazione: Integrazione di Azure Active Directory con OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="12c6c-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="12c6c-104">Questa esercitazione descrive come integrare OfficeSpace Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12c6c-104">In this tutorial, you learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="12c6c-105">L'integrazione di OfficeSpace Software con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="12c6c-105">Integrating OfficeSpace Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="12c6c-106">È possibile controllare in Azure AD chi può accedere a OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="12c6c-106">You can control in Azure AD who has access to OfficeSpace Software.</span></span>
- <span data-ttu-id="12c6c-107">È possibile abilitare gli utenti per l'accesso automatico a OfficeSpace Software (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="12c6c-107">You can enable your users to automatically get signed-on to OfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="12c6c-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="12c6c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="12c6c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="12c6c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12c6c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="12c6c-110">Prerequisites</span></span>

<span data-ttu-id="12c6c-111">Per configurare l'integrazione di Azure AD con OfficeSpace Software, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="12c6c-111">To configure Azure AD integration with OfficeSpace Software, you need the following items:</span></span>

- <span data-ttu-id="12c6c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12c6c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="12c6c-113">Sottoscrizione di OfficeSpace Software abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="12c6c-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="12c6c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="12c6c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="12c6c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="12c6c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="12c6c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="12c6c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="12c6c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12c6c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="12c6c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="12c6c-118">Scenario description</span></span>
<span data-ttu-id="12c6c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="12c6c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="12c6c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="12c6c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12c6c-121">Aggiunta di OfficeSpace Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="12c6c-121">Adding OfficeSpace Software from the gallery</span></span>
2. <span data-ttu-id="12c6c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c6c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-the-gallery"></a><span data-ttu-id="12c6c-123">Aggiunta di OfficeSpace Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="12c6c-123">Adding OfficeSpace Software from the gallery</span></span>
<span data-ttu-id="12c6c-124">Per configurare l'integrazione di OfficeSpace Software in Azure AD, è necessario aggiungere OfficeSpace Software dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="12c6c-124">To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="12c6c-125">**Per aggiungere OfficeSpace Software dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="12c6c-125">**To add OfficeSpace Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="12c6c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="12c6c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="12c6c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="12c6c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="12c6c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="12c6c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="12c6c-133">Nella casella di ricerca digitare **OfficeSpace Software**, selezionare **OfficeSpace Software** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="12c6c-133">In the search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button to add the application.</span></span>

    ![OfficeSpace Software nell'elenco risultati](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="12c6c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c6c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="12c6c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con OfficeSpace Software usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="12c6c-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="12c6c-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di OfficeSpace Software che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12c6c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OfficeSpace Software is to a user in Azure AD.</span></span> <span data-ttu-id="12c6c-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="12c6c-138">In other words, a link relationship between an Azure AD user and the related user in OfficeSpace Software needs to be established.</span></span>

<span data-ttu-id="12c6c-139">Per stabilire la relazione di collegamento, in OfficeSpace Software assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="12c6c-139">In OfficeSpace Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="12c6c-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con OfficeSpace Software, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="12c6c-140">To configure and test Azure AD single sign-on with OfficeSpace Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="12c6c-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="12c6c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="12c6c-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12c6c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="12c6c-143">**[Creare un utente di test di OfficeSpace Software](#create-a-officespace-software-test-user)**: per avere una controparte di Britta Simon in OfficeSpace Software collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12c6c-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - to have a counterpart of Britta Simon in OfficeSpace Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="12c6c-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12c6c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="12c6c-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="12c6c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="12c6c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c6c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="12c6c-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="12c6c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="12c6c-148">**Per configurare l'accesso Single Sign-On di Azure AD con OfficeSpace Software, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="12c6c-148">**To configure Azure AD single sign-on with OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="12c6c-149">Nella pagina di integrazione dell'applicazione **OfficeSpace Software** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-149">In the Azure portal, on the **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="12c6c-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="12c6c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="12c6c-153">Nella sezione **URL e dominio OfficeSpace Software** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="12c6c-153">On the **OfficeSpace Software Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="12c6c-155">a.</span><span class="sxs-lookup"><span data-stu-id="12c6c-155">a.</span></span> <span data-ttu-id="12c6c-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company name>.officespacesoftware.com/users/sign_in/saml`.</span><span class="sxs-lookup"><span data-stu-id="12c6c-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="12c6c-157">b.</span><span class="sxs-lookup"><span data-stu-id="12c6c-157">b.</span></span> <span data-ttu-id="12c6c-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="12c6c-158">In the **Identifier** textbox, type a URL using the following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="12c6c-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="12c6c-159">These values are not real.</span></span> <span data-ttu-id="12c6c-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="12c6c-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="12c6c-161">Per ottenere questi valori, contattare il [team di supporto clienti di OfficeSpace Software](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="12c6c-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) to get these values.</span></span> 

4. <span data-ttu-id="12c6c-162">L'applicazione OfficeSpace Software si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="12c6c-162">OfficeSpace Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="12c6c-163">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="12c6c-163">Please configure the following claims for this application.</span></span> <span data-ttu-id="12c6c-164">È possibile gestire i valori di questi attributi dalla sezione "**Attributi utente**" nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="12c6c-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="12c6c-165">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="12c6c-165">The following screenshot shows an example for this.</span></span>
    
    ![Configurazione dell'attributo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="12c6c-167">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** selezionare **user.mail** come **Identificatore utente**. Per ogni riga illustrata nella tabella seguente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="12c6c-167">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="12c6c-168">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="12c6c-168">Attribute Name</span></span> | <span data-ttu-id="12c6c-169">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="12c6c-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="12c6c-170">email</span><span class="sxs-lookup"><span data-stu-id="12c6c-170">email</span></span> | <span data-ttu-id="12c6c-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="12c6c-171">user.mail</span></span> |
    | <span data-ttu-id="12c6c-172">name</span><span class="sxs-lookup"><span data-stu-id="12c6c-172">name</span></span> | <span data-ttu-id="12c6c-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="12c6c-173">user.displayname</span></span> |
    | <span data-ttu-id="12c6c-174">first_name</span><span class="sxs-lookup"><span data-stu-id="12c6c-174">first_name</span></span> | <span data-ttu-id="12c6c-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="12c6c-175">user.givenname</span></span> |
    | <span data-ttu-id="12c6c-176">last_name</span><span class="sxs-lookup"><span data-stu-id="12c6c-176">last_name</span></span> | <span data-ttu-id="12c6c-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="12c6c-177">user.surname</span></span> |

    <span data-ttu-id="12c6c-178">a.</span><span class="sxs-lookup"><span data-stu-id="12c6c-178">a.</span></span> <span data-ttu-id="12c6c-179">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="12c6c-180">Configurazione, aggiunta</span><span class="sxs-lookup"><span data-stu-id="12c6c-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Configurazione dell'attributo](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="12c6c-182">b.</span><span class="sxs-lookup"><span data-stu-id="12c6c-182">b.</span></span> <span data-ttu-id="12c6c-183">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="12c6c-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="12c6c-184">c.</span><span class="sxs-lookup"><span data-stu-id="12c6c-184">c.</span></span> <span data-ttu-id="12c6c-185">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="12c6c-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="12c6c-186">d.</span><span class="sxs-lookup"><span data-stu-id="12c6c-186">d.</span></span> <span data-ttu-id="12c6c-187">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="12c6c-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="12c6c-188">Nella sezione **Certificato di firma SAML** copiare il valore **IDENTIFICAZIONE PERSONALE** del certificato.</span><span class="sxs-lookup"><span data-stu-id="12c6c-188">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of the certificate.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="12c6c-190">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="12c6c-190">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="12c6c-192">Nella sezione **Configurazione di OfficeSpace Software** fare clic su **Configura OfficeSpace Software** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-192">On the **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="12c6c-193">Copiare i valori **Sign-Out URL (URL di disconnessione) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="12c6c-193">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="12c6c-195">In un'altra finestra del browser Web accedere al tenant di OfficeSpace Software come amministratore.</span><span class="sxs-lookup"><span data-stu-id="12c6c-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="12c6c-196">Passare a **Impostazioni** e fare clic su **Connettori**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-196">Go to **Settings** and click **Connectors**.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="12c6c-198">Fare clic su **Autenticazione SAML**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-198">Click **SAML Authentication**.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="12c6c-200">Nella sezione **SAML Authentication** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="12c6c-200">In the **SAML Authentication** section, perform the following steps:</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="12c6c-202">a.</span><span class="sxs-lookup"><span data-stu-id="12c6c-202">a.</span></span> <span data-ttu-id="12c6c-203">Nella casella di testo **Logout provider url** (URL provider di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="12c6c-203">In the **Logout provider url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="12c6c-204">b.</span><span class="sxs-lookup"><span data-stu-id="12c6c-204">b.</span></span> <span data-ttu-id="12c6c-205">Nella casella di testo **Client idp target url** (URL di destinazione IdP client) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="12c6c-205">In the **Client idp target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="12c6c-206">c.</span><span class="sxs-lookup"><span data-stu-id="12c6c-206">c.</span></span> <span data-ttu-id="12c6c-207">Nella casella di testo **Client IDP certificate fingerprint** (Impronta digitale certificato IDP client) incollare il valore **Identificazione personale** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="12c6c-207">Paste the **Thumbprint** value which you have copied from Azure portal, into the **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="12c6c-208">d.</span><span class="sxs-lookup"><span data-stu-id="12c6c-208">d.</span></span> <span data-ttu-id="12c6c-209">Fare clic su **Salva impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="12c6c-210">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="12c6c-210">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="12c6c-211">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="12c6c-211">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="12c6c-212">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12c6c-212">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="12c6c-213">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c6c-213">Create an Azure AD test user</span></span>

<span data-ttu-id="12c6c-214">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="12c6c-214">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="12c6c-216">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="12c6c-216">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="12c6c-217">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="12c6c-217">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="12c6c-219">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-219">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="12c6c-221">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-221">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="12c6c-223">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="12c6c-223">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="12c6c-225">a.</span><span class="sxs-lookup"><span data-stu-id="12c6c-225">a.</span></span> <span data-ttu-id="12c6c-226">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-226">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="12c6c-227">b.</span><span class="sxs-lookup"><span data-stu-id="12c6c-227">b.</span></span> <span data-ttu-id="12c6c-228">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12c6c-228">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="12c6c-229">c.</span><span class="sxs-lookup"><span data-stu-id="12c6c-229">c.</span></span> <span data-ttu-id="12c6c-230">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-230">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="12c6c-231">d.</span><span class="sxs-lookup"><span data-stu-id="12c6c-231">d.</span></span> <span data-ttu-id="12c6c-232">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="12c6c-233">Creare un utente di test di OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="12c6c-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="12c6c-234">Questa sezione descrive come creare un utente di nome Britta Simon in OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="12c6c-234">The objective of this section is to create a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="12c6c-235">OfficeSpace Software supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="12c6c-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="12c6c-236">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="12c6c-236">There is no action item for you in this section.</span></span> <span data-ttu-id="12c6c-237">Durante un tentativo di accesso a OfficeSpace Software verrà creato un nuovo utente, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="12c6c-237">A new user will be created during an attempt to access OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="12c6c-238">Per creare un utente manualmente, è necessario contattare il [team di supporto di OfficeSpace Software](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="12c6c-238">If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="12c6c-239">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c6c-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="12c6c-240">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="12c6c-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OfficeSpace Software.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="12c6c-242">**Per assegnare Britta Simon a OfficeSpace Software, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="12c6c-242">**To assign Britta Simon to OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="12c6c-243">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="12c6c-245">Nell'elenco di applicazioni selezionare **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-245">In the applications list, select **OfficeSpace Software**.</span></span>

    ![Collegamento di OfficeSpace Software nell'elenco delle applicazioni](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="12c6c-247">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="12c6c-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="12c6c-249">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-249">Click **Add** button.</span></span> <span data-ttu-id="12c6c-250">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="12c6c-252">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="12c6c-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="12c6c-253">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="12c6c-254">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="12c6c-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="12c6c-255">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="12c6c-255">Test single sign-on</span></span>

<span data-ttu-id="12c6c-256">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="12c6c-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="12c6c-257">Quando si fa clic sul riquadro OfficeSpace Software nel pannello di accesso, si accederà automaticamente all'applicazione OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="12c6c-257">When you click the OfficeSpace Software tile in the Access Panel, you should get automatically signed-on to your OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12c6c-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="12c6c-258">Additional resources</span></span>

* [<span data-ttu-id="12c6c-259">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12c6c-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12c6c-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12c6c-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

