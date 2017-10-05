---
title: 'Esercitazione: Integrazione di Azure Active Directory con Onit | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Onit.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 47c0055b89dbcf6a30a7f9ac5a33913e7bf463fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="426cf-103">Esercitazione: Integrazione di Azure Active Directory con Onit</span><span class="sxs-lookup"><span data-stu-id="426cf-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="426cf-104">Questa esercitazione descrive come integrare Onit con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="426cf-104">In this tutorial, you learn how to integrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="426cf-105">L'integrazione di Onit con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="426cf-105">Integrating Onit with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="426cf-106">È possibile controllare in Azure AD chi può accedere a Onit.</span><span class="sxs-lookup"><span data-stu-id="426cf-106">You can control in Azure AD who has access to Onit.</span></span>
- <span data-ttu-id="426cf-107">È possibile abilitare gli utenti per l'accesso automatico a Onit (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="426cf-107">You can enable your users to automatically get signed-on to Onit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="426cf-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="426cf-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="426cf-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="426cf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="426cf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="426cf-110">Prerequisites</span></span>

<span data-ttu-id="426cf-111">Per configurare l'integrazione di Azure AD con Onit, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="426cf-111">To configure Azure AD integration with Onit, you need the following items:</span></span>

- <span data-ttu-id="426cf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="426cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="426cf-113">Sottoscrizione di Onit abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="426cf-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="426cf-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="426cf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="426cf-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="426cf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="426cf-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="426cf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="426cf-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="426cf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="426cf-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="426cf-118">Scenario description</span></span>

<span data-ttu-id="426cf-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="426cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="426cf-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="426cf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="426cf-121">Aggiunta di Onit dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="426cf-121">Adding Onit from the gallery</span></span>
2. <span data-ttu-id="426cf-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="426cf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-the-gallery"></a><span data-ttu-id="426cf-123">Aggiunta di Onit dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="426cf-123">Adding Onit from the gallery</span></span>
<span data-ttu-id="426cf-124">Per configurare l'integrazione di Onit in Azure AD, è necessario aggiungere Onit dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="426cf-124">To configure the integration of Onit into Azure AD, you need to add Onit from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="426cf-125">**Per aggiungere Onit dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="426cf-125">**To add Onit from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="426cf-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="426cf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="426cf-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="426cf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="426cf-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="426cf-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="426cf-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="426cf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="426cf-133">Nella casella di ricerca digitare **Onit**, selezionare **Onit** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="426cf-133">In the search box, type **Onit**, select **Onit** from result panel then click **Add** button to add the application.</span></span>

    ![Onit nell'elenco risultati](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="426cf-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="426cf-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="426cf-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Onit usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="426cf-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="426cf-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Onit corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="426cf-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Onit is to a user in Azure AD.</span></span> <span data-ttu-id="426cf-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Onit.</span><span class="sxs-lookup"><span data-stu-id="426cf-138">In other words, a link relationship between an Azure AD user and the related user in Onit needs to be established.</span></span>

<span data-ttu-id="426cf-139">Per stabilire la relazione di collegamento, in Onit assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="426cf-139">In Onit, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="426cf-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Onit, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="426cf-140">To configure and test Azure AD single sign-on with Onit, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="426cf-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="426cf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="426cf-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="426cf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="426cf-143">**[Creare un utente di test di Onit](#create-an-onit-test-user)**: per avere una controparte di Britta Simon in Onit collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="426cf-143">**[Create an Onit test user](#create-an-onit-test-user)** - to have a counterpart of Britta Simon in Onit that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="426cf-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="426cf-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="426cf-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="426cf-145">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="426cf-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="426cf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="426cf-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Onit.</span><span class="sxs-lookup"><span data-stu-id="426cf-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="426cf-148">**Per configurare l'accesso Single Sign-On di Azure AD con Onit, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="426cf-148">**To configure Azure AD single sign-on with Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="426cf-149">Nella pagina di integrazione dell'applicazione **Onit** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="426cf-149">In the Azure portal, on the **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="426cf-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="426cf-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="426cf-153">Nella sezione **URL e dominio Onit** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="426cf-153">On the **Onit Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="426cf-155">a.</span><span class="sxs-lookup"><span data-stu-id="426cf-155">a.</span></span> <span data-ttu-id="426cf-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<sub-domain>.onit.com`.</span><span class="sxs-lookup"><span data-stu-id="426cf-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="426cf-157">b.</span><span class="sxs-lookup"><span data-stu-id="426cf-157">b.</span></span> <span data-ttu-id="426cf-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="426cf-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="426cf-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="426cf-159">These values are not real.</span></span> <span data-ttu-id="426cf-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="426cf-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="426cf-161">Per ottenere questi valori, contattare il [team di supporto clienti di Onit](https://www.onit.com/support).</span><span class="sxs-lookup"><span data-stu-id="426cf-161">Contact [Onit Client support team](https://www.onit.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="426cf-162">Nella sezione **Certificato di firma SAML** copiare il valore **IDENTIFICAZIONE PERSONALE** del certificato.</span><span class="sxs-lookup"><span data-stu-id="426cf-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="426cf-164">L'applicazione Onit prevede un formato specifico per le asserzioni SAML.</span><span class="sxs-lookup"><span data-stu-id="426cf-164">Onit application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="426cf-165">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="426cf-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="426cf-166">È possibile gestire i valori di questi attributi dalla scheda **Attribute (Attributo)** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="426cf-166">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="426cf-167">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="426cf-167">The following screenshot shows an example for this.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="426cf-169">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come illustrato nell'immagine e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="426cf-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="426cf-170">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="426cf-170">Attribute Name</span></span> | <span data-ttu-id="426cf-171">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="426cf-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="426cf-172">email</span><span class="sxs-lookup"><span data-stu-id="426cf-172">email</span></span> | <span data-ttu-id="426cf-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="426cf-173">user.mail</span></span> |
    
    <span data-ttu-id="426cf-174">a.</span><span class="sxs-lookup"><span data-stu-id="426cf-174">a.</span></span> <span data-ttu-id="426cf-175">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="426cf-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="426cf-178">b.</span><span class="sxs-lookup"><span data-stu-id="426cf-178">b.</span></span> <span data-ttu-id="426cf-179">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="426cf-179">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="426cf-180">c.</span><span class="sxs-lookup"><span data-stu-id="426cf-180">c.</span></span> <span data-ttu-id="426cf-181">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="426cf-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="426cf-182">d.</span><span class="sxs-lookup"><span data-stu-id="426cf-182">d.</span></span> <span data-ttu-id="426cf-183">Lasciare vuota la casella **Spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="426cf-183">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="426cf-184">e.</span><span class="sxs-lookup"><span data-stu-id="426cf-184">e.</span></span> <span data-ttu-id="426cf-185">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="426cf-185">Click **Ok**.</span></span>

7. <span data-ttu-id="426cf-186">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="426cf-186">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="426cf-188">Nella sezione **Configurazione di Onit** fare clic su **Configura Onit** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="426cf-188">On the **Onit Configuration** section, click **Configure Onit** to open **Configure sign-on** window.</span></span> <span data-ttu-id="426cf-189">Copiare **URL di disconnessione e URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="426cf-189">Copy the **Sign-Out URL, SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="426cf-191">In un'altra finestra del Web browser accedere al sito aziendale di Onit come amministratore.</span><span class="sxs-lookup"><span data-stu-id="426cf-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="426cf-192">Scegliere **Amministrazione**dal menu disponibile nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="426cf-192">In the menu on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="426cf-193">![Amministrazione](./media/active-directory-saas-onit-tutorial/IC791174.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="426cf-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="426cf-194">Fare clic su **Edit Corporation**.</span><span class="sxs-lookup"><span data-stu-id="426cf-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="426cf-195">![Modificare l'azienda](./media/active-directory-saas-onit-tutorial/IC791175.png "Modificare l'azienda")</span><span class="sxs-lookup"><span data-stu-id="426cf-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="426cf-196">Fare clic sulla scheda **Security** .</span><span class="sxs-lookup"><span data-stu-id="426cf-196">Click the **Security** tab.</span></span>
    
    <span data-ttu-id="426cf-197">![Modificare le informazioni sulla società](./media/active-directory-saas-onit-tutorial/IC791176.png "Modificare le informazioni sulla società")</span><span class="sxs-lookup"><span data-stu-id="426cf-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="426cf-198">Nella scheda **Sicurezza** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="426cf-198">On the **Security** tab, perform the following steps:</span></span>

    <span data-ttu-id="426cf-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="426cf-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="426cf-200">a.</span><span class="sxs-lookup"><span data-stu-id="426cf-200">a.</span></span> <span data-ttu-id="426cf-201">Come **strategia di autenticazione** selezionare **Single Sign-On e password**.</span><span class="sxs-lookup"><span data-stu-id="426cf-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="426cf-202">b.</span><span class="sxs-lookup"><span data-stu-id="426cf-202">b.</span></span> <span data-ttu-id="426cf-203">Nella casella di testo **Idp Target URL** (URL di destinazione IdP) incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="426cf-203">In **Idp Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="426cf-204">c.</span><span class="sxs-lookup"><span data-stu-id="426cf-204">c.</span></span> <span data-ttu-id="426cf-205">Nella casella di testo **IDP Logout URL** (URL di disconnessione IDP) incollare l'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="426cf-205">In **Idp logout URL** textbox, paste the value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="426cf-206">d.</span><span class="sxs-lookup"><span data-stu-id="426cf-206">d.</span></span> <span data-ttu-id="426cf-207">Nella casella di testo **Idp Cert Fingerprint (SHA1)** (Impronta digitale certificato IdP - SHA1) incollare il valore **Identificazione personale** del certificato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="426cf-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste the  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="426cf-208">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="426cf-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="426cf-209">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="426cf-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="426cf-210">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="426cf-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="426cf-211">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="426cf-211">Create an Azure AD test user</span></span>

<span data-ttu-id="426cf-212">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="426cf-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="426cf-214">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="426cf-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="426cf-215">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="426cf-215">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="426cf-217">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="426cf-217">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="426cf-219">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="426cf-219">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="426cf-221">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="426cf-221">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="426cf-223">a.</span><span class="sxs-lookup"><span data-stu-id="426cf-223">a.</span></span> <span data-ttu-id="426cf-224">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="426cf-224">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="426cf-225">b.</span><span class="sxs-lookup"><span data-stu-id="426cf-225">b.</span></span> <span data-ttu-id="426cf-226">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="426cf-226">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="426cf-227">c.</span><span class="sxs-lookup"><span data-stu-id="426cf-227">c.</span></span> <span data-ttu-id="426cf-228">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="426cf-228">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="426cf-229">d.</span><span class="sxs-lookup"><span data-stu-id="426cf-229">d.</span></span> <span data-ttu-id="426cf-230">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="426cf-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="426cf-231">Creare un utente di test di Onit</span><span class="sxs-lookup"><span data-stu-id="426cf-231">Create an Onit test user</span></span>

<span data-ttu-id="426cf-232">Per consentire agli utenti di Azure AD di accedere a Onit, è necessario eseguirne il provisioning in Onit.</span><span class="sxs-lookup"><span data-stu-id="426cf-232">In order to enable Azure AD users to log into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="426cf-233">Nel caso di Onit, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="426cf-233">In the case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="426cf-234">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="426cf-234">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="426cf-235">Accedere al sito aziendale di **Onit** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="426cf-235">Sign on to your **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="426cf-236">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="426cf-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="426cf-237">![Amministrazione](./media/active-directory-saas-onit-tutorial/IC791180.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="426cf-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="426cf-238">Nella pagina della finestra di dialogo **Aggiungi utente** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="426cf-238">On the **Add User** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="426cf-239">![Aggiungere un utente](./media/active-directory-saas-onit-tutorial/IC791181.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="426cf-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="426cf-240">Digitare il **nome** e l'**indirizzo e-mail** di un account Azure AD valido di cui si vuole effettuare il provisioning nelle caselle di testo correlate.</span><span class="sxs-lookup"><span data-stu-id="426cf-240">Type the **Name** and the **Email Address** of a valid Azure AD account you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="426cf-241">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="426cf-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="426cf-242">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="426cf-242">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="426cf-243">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="426cf-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="426cf-244">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Onit.</span><span class="sxs-lookup"><span data-stu-id="426cf-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Onit.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="426cf-246">**Per assegnare Britta Simon a Onit, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="426cf-246">**To assign Britta Simon to Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="426cf-247">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="426cf-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="426cf-249">Nell'elenco delle applicazioni selezionare **Onit**.</span><span class="sxs-lookup"><span data-stu-id="426cf-249">In the applications list, select **Onit**.</span></span>

    ![Collegamento di Onit nell'elenco delle applicazioni](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="426cf-251">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="426cf-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="426cf-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="426cf-253">Click **Add** button.</span></span> <span data-ttu-id="426cf-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="426cf-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="426cf-256">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="426cf-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="426cf-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="426cf-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="426cf-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="426cf-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="426cf-259">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="426cf-259">Test single sign-on</span></span>

<span data-ttu-id="426cf-260">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="426cf-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="426cf-261">Quando si fa clic sul riquadro Onit nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Onit.</span><span class="sxs-lookup"><span data-stu-id="426cf-261">When you click the Onit tile in the Access Panel, you should get automatically signed-on to your Onit application.</span></span>
<span data-ttu-id="426cf-262">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="426cf-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="426cf-263">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="426cf-263">Additional resources</span></span>

* [<span data-ttu-id="426cf-264">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="426cf-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="426cf-265">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="426cf-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

