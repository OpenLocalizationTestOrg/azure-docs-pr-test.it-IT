---
title: 'Esercitazione: Integrazione di Azure Active Directory con Qlik Sense Enterprise | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Qlik Sense Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4964634cd5aaf0dbb98c766f5e12700c4d118750
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="fc4b7-103">Esercitazione: Integrazione di Azure Active Directory con Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="fc4b7-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="fc4b7-104">Questa esercitazione descrive come integrare Qlik Sense Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fc4b7-105">L'integrazione di Qlik Sense Enterprise con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fc4b7-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fc4b7-106">È possibile controllare in Azure AD chi può accedere a Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-106">You can control in Azure AD who has access to Qlik Sense Enterprise.</span></span>
- <span data-ttu-id="fc4b7-107">È possibile abilitare gli utenti per l'accesso automatico a Qlik Sense Enterprise (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fc4b7-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="fc4b7-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc4b7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fc4b7-110">Prerequisites</span></span>

<span data-ttu-id="fc4b7-111">Per configurare l'integrazione di Azure AD con Qlik Sense Enterprise, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fc4b7-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span></span>

- <span data-ttu-id="fc4b7-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fc4b7-113">Sottoscrizione di Qlik Sense Enterprise abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fc4b7-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fc4b7-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fc4b7-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fc4b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fc4b7-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fc4b7-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fc4b7-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="fc4b7-118">Scenario description</span></span>
<span data-ttu-id="fc4b7-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fc4b7-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fc4b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fc4b7-121">Aggiunta di Qlik Sense Enterprise dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="fc4b7-121">Adding Qlik Sense Enterprise from the gallery</span></span>
2. <span data-ttu-id="fc4b7-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc4b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-the-gallery"></a><span data-ttu-id="fc4b7-123">Aggiunta di Qlik Sense Enterprise dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="fc4b7-123">Adding Qlik Sense Enterprise from the gallery</span></span>
<span data-ttu-id="fc4b7-124">Per configurare l'integrazione di Qlik Sense Enterprise in Azure AD, è necessario aggiungere Qlik Sense Enterprise dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fc4b7-125">**Per aggiungere Qlik Sense Enterprise dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fc4b7-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fc4b7-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="fc4b7-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fc4b7-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="fc4b7-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="fc4b7-133">Nella casella di ricerca digitare **Qlik Sense Enterprise**, selezionare **Qlik Sense Enterprise** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-133">In the search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button to add the application.</span></span>

    ![Qlik Sense Enterprise nell'elenco risultati](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fc4b7-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc4b7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fc4b7-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Qlik Sense Enterprise con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fc4b7-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fc4b7-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Qlik Sense Enterprise che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="fc4b7-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-138">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span></span>

<span data-ttu-id="fc4b7-139">Per stabilire la relazione di collegamento, in Qlik Sense Enterprise assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-139">In Qlik Sense Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fc4b7-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Qlik Sense Enterprise, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fc4b7-140">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fc4b7-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fc4b7-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fc4b7-143">**[Creare un utente di test di Qlik Sense Enterprise](#create-a-qlik-sense-enterprise-test-user)**: per avere una controparte di Britta Simon in Qlik Sense Enterprise collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fc4b7-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fc4b7-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fc4b7-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc4b7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fc4b7-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="fc4b7-148">**Per configurare l'accesso Single Sign-On di Azure AD con Qlik Sense Enterprise, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fc4b7-148">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="fc4b7-149">Nella pagina di integrazione dell'applicazione **Qlik Sense Enterprise** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-149">In the Azure portal, on the **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="fc4b7-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="fc4b7-153">Nella sezione **URL e dominio Qlik Sense Enterprise** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="fc4b7-153">On the **Qlik Sense Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="fc4b7-155">a.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-155">a.</span></span> <span data-ttu-id="fc4b7-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="fc4b7-157">Si noti la barra finale nell'URI.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-157">Note the trailing slash at the end of this URI.</span></span> <span data-ttu-id="fc4b7-158">È obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-158">It is required.</span></span>
    
    <span data-ttu-id="fc4b7-159">b.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-159">b.</span></span> <span data-ttu-id="fc4b7-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="fc4b7-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="fc4b7-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="fc4b7-161">These values are not real.</span></span> <span data-ttu-id="fc4b7-162">Aggiornare questi valori con identificatore e URL di accesso effettivi, illustrati più avanti in questa esercitazione, oppure contattare il [team di supporto clienti di Qlik Sense Enterprise](https://www.qlik.com/us/services/support) per ottenere questi valori.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-162">Update these values with the actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values.</span></span> 

4. <span data-ttu-id="fc4b7-163">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="fc4b7-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fc4b7-165">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fc4b7-167">Preparare il file XML di metadati della federazione per il caricamento sul server Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-167">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="fc4b7-168">Prima di caricare i metadati IdP sul server Qlik Sense, è necessario modificare il file rimuovendo informazioni in modo da garantire il corretto funzionamento tra Azure AD e il server Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-168">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![Qlik Sense][qs24]
   
    <span data-ttu-id="fc4b7-170">a.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-170">a.</span></span> <span data-ttu-id="fc4b7-171">Aprire il file FederationMetaData.xml scaricato dal portale di Azure in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-171">Open the FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="fc4b7-172">b.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-172">b.</span></span> <span data-ttu-id="fc4b7-173">Cercare il valore **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-173">Search for the value **RoleDescriptor**.</span></span>  <span data-ttu-id="fc4b7-174">Ci sono quattro voci (due coppie di tag di elementi di apertura e di chiusura).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="fc4b7-175">c.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-175">c.</span></span> <span data-ttu-id="fc4b7-176">Eliminare dal file i tag RoleDescriptor e tutte le informazioni in essi racchiuse.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-176">Delete the RoleDescriptor tags and all information in between from the file.</span></span>
   
    <span data-ttu-id="fc4b7-177">d.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-177">d.</span></span> <span data-ttu-id="fc4b7-178">Salvare il file e tenerlo a disposizione per usarlo più avanti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-178">Save the file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="fc4b7-179">Passare a Qlik Sense Qlik Management Console (QMC) come utente autorizzato a creare configurazioni di proxy virtuali.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-179">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="fc4b7-180">In QMC fare clic sulla voce di menu **Virtual Proxies** (Proxy virtuali).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-180">In the QMC, click on the **Virtual Proxies** menu item.</span></span>
   
    ![Qlik Sense][qs6] 

9. <span data-ttu-id="fc4b7-182">Nella parte inferiore dello schermo fare clic sul pulsante **Create new** (Crea nuovo).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-182">At the bottom of the screen, click the **Create new** button.</span></span>
   
    ![Qlik Sense][qs7]

10. <span data-ttu-id="fc4b7-184">Viene visualizzata la schermata per la modifica del proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-184">The Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="fc4b7-185">Sul lato destro della schermata è disponibile un menu per la visualizzazione delle opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-185">On the right side of the screen is a menu for making configuration options visible.</span></span>
   
    ![Qlik Sense][qs9]

11. <span data-ttu-id="fc4b7-187">Dopo aver selezionato l'opzione di menu Identification (Identificazione), immettere le informazioni di identificazione per la configurazione del proxy virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-187">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span></span>
    
    ![Qlik Sense][qs8]  
    
    <span data-ttu-id="fc4b7-189">a.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-189">a.</span></span> <span data-ttu-id="fc4b7-190">Il campo **Description** (Descrizione) contiene un nome descrittivo per la configurazione del proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-190">The **Description** field is a friendly name for the virtual proxy configuration.</span></span>  <span data-ttu-id="fc4b7-191">Immettere un valore per la descrizione.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="fc4b7-192">b.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-192">b.</span></span> <span data-ttu-id="fc4b7-193">Il campo **Prefix** (Prefisso) identifica l'endpoint proxy virtuale per la connessione a Qlik Sense con l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-193">The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="fc4b7-194">Immettere un nome di prefisso univoco per il proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="fc4b7-195">c.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-195">c.</span></span> <span data-ttu-id="fc4b7-196">**Session inactivity timeout (minutes)** (Timeout di inattività sessione - minuti) indica il timeout per le connessioni tramite il proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-196">**Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="fc4b7-197">d.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-197">d.</span></span> <span data-ttu-id="fc4b7-198">**Session cookie header name** (Nome intestazione cookie sessione) è il nome del cookie in cui è archiviato l'identificatore della sessione di Qlik Sense ricevuto da un utente dopo il completamento dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-198">The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="fc4b7-199">Il nome deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-199">This name must be unique.</span></span>

12. <span data-ttu-id="fc4b7-200">Fare clic sull'opzione di menu Authentication (Autenticazione) per renderla visibile.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-200">Click on the Authentication menu option to make it visible.</span></span>  <span data-ttu-id="fc4b7-201">Verrà visualizzata la schermata Authentication (Autenticazione).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-201">The Authentication screen appears.</span></span>
    
    ![Qlik Sense][qs10]
    
    <span data-ttu-id="fc4b7-203">a.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-203">a.</span></span> <span data-ttu-id="fc4b7-204">L'elenco a discesa **Anonymous access mode** (Modalità accesso anonimo) determina se gli utenti anonimi potranno accedere a Qlik Sense tramite il proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-204">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span></span>  <span data-ttu-id="fc4b7-205">L'opzione predefinita è No anonymous user (Nessun utente anonimo).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-205">The default option is No anonymous user.</span></span>
    
    <span data-ttu-id="fc4b7-206">b.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-206">b.</span></span> <span data-ttu-id="fc4b7-207">L'elenco a discesa **Authentication method** (Metodo di autenticazione) determina lo schema di autenticazione che verrà usato dal proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-207">The **Authentication method** drop-down determines the authentication scheme the virtual proxy will use.</span></span>  <span data-ttu-id="fc4b7-208">Selezionare SAML nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-208">Select SAML from the drop-down list.</span></span>  <span data-ttu-id="fc4b7-209">Verranno di conseguenza visualizzate altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="fc4b7-210">c.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-210">c.</span></span> <span data-ttu-id="fc4b7-211">Nel campo **SAML host URI** (URI host SAML) specificare il nome host che verrà immesso dagli utenti per accedere a Qlik Sense tramite questo proxy virtuale SAML.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-211">In the **SAML host URI field**, input the hostname users enter to access Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="fc4b7-212">Il nome host è l'URI del server Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-212">The hostname is the uri of the Qlik Sense server.</span></span>
    
    <span data-ttu-id="fc4b7-213">d.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-213">d.</span></span> <span data-ttu-id="fc4b7-214">In **SAML entity ID**(ID entità SAML) immettere lo stesso valore inserito nel campo SAML host URI (URI host SAML).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-214">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span></span>
    
    <span data-ttu-id="fc4b7-215">e.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-215">e.</span></span> <span data-ttu-id="fc4b7-216">**SAML IdP metadata** (Metadati IdP SAML) è il campo modificato nella precedente sezione relativa alla **modifica dei metadati della federazione della configurazione di Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-216">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="fc4b7-217">**Prima di caricare i metadati IdP, è necessario modificare il file** rimuovendo informazioni in modo da garantire il corretto funzionamento tra Azure AD e il server Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-217">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="fc4b7-218">**Se il file non è ancora stato modificato, vedere le istruzioni riportate sopra.**</span><span class="sxs-lookup"><span data-stu-id="fc4b7-218">**Please refer to the instructions above if the file has yet to be edited.**</span></span>  <span data-ttu-id="fc4b7-219">Se il file è stato modificato, fare clic sul pulsante Browse (Sfoglia) e selezionare il file di metadati modificato per caricarlo nella configurazione del proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-219">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span></span>
    
    <span data-ttu-id="fc4b7-220">f.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-220">f.</span></span> <span data-ttu-id="fc4b7-221">Immettere il nome dell'attributo o il riferimento dello schema per l'attributo SAML che rappresenta l'**ID utente** inviato da Azure AD al server Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-221">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD sends to the Qlik Sense server.</span></span>  <span data-ttu-id="fc4b7-222">Le informazioni relative al riferimento dello schema sono disponibili nelle schermate dell'app in Azure in seguito alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-222">Schema reference information is available in the Azure app screens post configuration.</span></span>  <span data-ttu-id="fc4b7-223">Per usare il nome di attributo, immettere `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-223">To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="fc4b7-224">g.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-224">g.</span></span> <span data-ttu-id="fc4b7-225">Immettere il valore della **directory utente** che verrà associata agli utenti quando eseguiranno l'autenticazione al server Qlik Sense tramite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-225">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span></span>  <span data-ttu-id="fc4b7-226">I valori hardcoded devono essere racchiusi tra **parentesi quadre []**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="fc4b7-227">Per usare un attributo inviato nell'asserzione SAML di Azure AD, immettere il nome dell'attributo in questa casella di testo **senza** parentesi quadre.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-227">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="fc4b7-228">h.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-228">h.</span></span> <span data-ttu-id="fc4b7-229">**SAML signing algorithm** (Algoritmo di firma SAML) imposta la firma del certificato del provider di servizi (in questo caso, il server Qlik Sense) per la configurazione del proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-229">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span></span>  <span data-ttu-id="fc4b7-230">Se il server Qlik Sense usa un certificato attendibile generato con Microsoft Enhanced RSA and AES Cryptographic Provider, modificare l'algoritmo di firma SAML impostandolo su **SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span></span>
    
    <span data-ttu-id="fc4b7-231">i.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-231">i.</span></span> <span data-ttu-id="fc4b7-232">La sezione SAML attribute mapping (Mapping attributi SAML) consente di inviare a Qlik Sense attributi aggiuntivi, come i gruppi, da usare nelle regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-232">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="fc4b7-233">Fare clic sull'opzione di menu **LOAD BALANCING** (BILANCIAMENTO DEL CARICO) per renderla visibile.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-233">Click on the **LOAD BALANCING** menu option to make it visible.</span></span>  <span data-ttu-id="fc4b7-234">Verrà visualizzata la schermata Load balancing (Bilanciamento del carico).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-234">The Load Balancing screen appears.</span></span>
    
    ![Qlik Sense][qs11]

14. <span data-ttu-id="fc4b7-236">Fare clic sul pulsante **Add new server node** (Aggiungi nuovo nodo server), selezionare uno o più nodi motore a cui Qlik Sense invierà le sessioni ai fini del bilanciamento del carico e fare clic su **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-236">Click on the **Add new server node** button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the **Add** button.</span></span>
    
    ![Qlik Sense][qs12]

15. <span data-ttu-id="fc4b7-238">Fare clic sull'opzione di menu Advanced (Avanzate) per renderla visibile.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-238">Click on the Advanced menu option to make it visible.</span></span> <span data-ttu-id="fc4b7-239">Verrà visualizzata la schermata Advanced (Avanzate).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-239">The Advanced screen appears.</span></span>
    
    ![Qlik Sense][qs13]
    
    <span data-ttu-id="fc4b7-241">Host white list (Elenco host consentiti) identifica i nomi host accettati per la connessione al server Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-241">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span></span>  <span data-ttu-id="fc4b7-242">**Immettere il nome host che gli utenti specificheranno per la connessione al server Qlik Sense.**</span><span class="sxs-lookup"><span data-stu-id="fc4b7-242">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span></span> <span data-ttu-id="fc4b7-243">Il nome host è lo stesso valore specificato in SAML host URI (URI host SAML) senza https://.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-243">The hostname is the same value as the SAML host uri without the https://.</span></span>

16. <span data-ttu-id="fc4b7-244">Fare clic sul pulsante **Apply** (Applica).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-244">Click the **Apply** button.</span></span>
    
    ![Qlik Sense][qs14]

17. <span data-ttu-id="fc4b7-246">Fare clic su OK per accettare il messaggio di avviso che indica che i proxy collegati al proxy virtuale verranno riavviati.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-246">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span></span>
    
    ![Qlik Sense][qs15]

18. <span data-ttu-id="fc4b7-248">Sul lato destro della schermata verrà visualizzato il menu Associated items (Elementi associati).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-248">On the right side of the screen, the Associated items menu appears.</span></span>  <span data-ttu-id="fc4b7-249">Fare clic sull'opzione di menu **Proxies** (Proxy).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-249">Click on the **Proxies** menu option.</span></span>
    
    ![Qlik Sense][qs16]

19. <span data-ttu-id="fc4b7-251">Verrà visualizza la schermata relativa ai proxy.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-251">The proxy screen appears.</span></span>  <span data-ttu-id="fc4b7-252">Fare clic sul pulsante **Link** (Collega) in basso per collegare un proxy al proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-252">Click the **Link** button at the bottom to link a proxy to the virtual proxy.</span></span>
    
    ![Qlik Sense][qs17]

20. <span data-ttu-id="fc4b7-254">Selezionare il nodo proxy che supporterà la connessione proxy virtuale e fare clic sul pulsante **Link** (Collega).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-254">Select the proxy node that will support this virtual proxy connection and click the **Link** button.</span></span>  <span data-ttu-id="fc4b7-255">Al termine del collegamento, il proxy verrà incluso nell'elenco dei proxy associati.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-255">After linking, the proxy will be listed under associated proxies.</span></span>
    
    ![Qlik Sense][qs18]
  
    ![Qlik Sense][qs19]

21. <span data-ttu-id="fc4b7-258">Dopo circa 5-10 secondi verrà visualizzato il messaggio per l'aggiornamento di QMC.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-258">After about five to ten seconds, the Refresh QMC message will appear.</span></span>  <span data-ttu-id="fc4b7-259">Fare clic sul pulsante **Refresh QMC** (Aggiorna QMC).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-259">Click the **Refresh QMC** button.</span></span>
    
    ![Qlik Sense][qs20]

22. <span data-ttu-id="fc4b7-261">Dopo l'aggiornamento di QMC, fare clic sulla voce di menu **Virtual proxies** (Proxy virtuali).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-261">When the QMC refreshes, click on the **Virtual proxies** menu item.</span></span> <span data-ttu-id="fc4b7-262">La nuova voce del proxy virtuale SAML sarà elencata nella tabella visualizzata.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-262">The new SAML virtual proxy entry is listed in the table on the screen.</span></span>  <span data-ttu-id="fc4b7-263">Fare clic sulla voce del proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-263">Single click on the virtual proxy entry.</span></span>
    
    ![Qlik Sense][qs51]

23. <span data-ttu-id="fc4b7-265">Nella parte inferiore della schermata verrà attivato il pulsante Download SP metadata (Scarica metadati SP).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-265">At the bottom of the screen, the Download SP metadata button will activate.</span></span>  <span data-ttu-id="fc4b7-266">Fare clic sul pulsante **Download SP metadata** (Scarica metadati SP) per salvare i metadati in un file.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-266">Click the **Download SP metadata** button to save the metadata to a file.</span></span>
    
    ![Qlik Sense][qs52]

24. <span data-ttu-id="fc4b7-268">Aprire il file di metadati SP.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-268">Open the sp metadata file.</span></span>  <span data-ttu-id="fc4b7-269">Osservare le voci **entityID** e **AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-269">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="fc4b7-270">Questi valori sono uguali ai valori **Identificatore** e **URL di accesso** nella configurazione dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-270">These values are equivalent to the **Identifier** and the **Sign on URL** in the Azure AD application configuration.</span></span> <span data-ttu-id="fc4b7-271">Incollare questi valori nella sezione **URL e dominio Qlik Sense Enterprise** nella configurazione dell'applicazione di Azure AD se i valori non corrispondono. Sarà quindi necessario sostituire i valori nella configurazione guidata dell'app Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-271">Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Azure AD application configuration if they are not matching, then you should replace them in the Azure AD App configuration wizard.</span></span>
    
    ![Qlik Sense][qs53]

> [!TIP]
> <span data-ttu-id="fc4b7-273">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-273">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fc4b7-274">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-274">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fc4b7-275">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fc4b7-275">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fc4b7-276">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc4b7-276">Create an Azure AD test user</span></span>
<span data-ttu-id="fc4b7-277">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-277">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="fc4b7-279">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fc4b7-279">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fc4b7-280">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-280">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

   ![Pulsante Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fc4b7-282">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-282">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

   ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fc4b7-284">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-284">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

   ![Pulsante Aggiungi](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fc4b7-286">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="fc4b7-286">In the **User** dialog box, perform the following steps:</span></span>

   ![Finestra di dialogo Utente](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="fc4b7-288">a.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-288">a.</span></span> <span data-ttu-id="fc4b7-289">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-289">In the **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="fc4b7-290">b.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-290">b.</span></span> <span data-ttu-id="fc4b7-291">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-291">In the **User name** box, type the email address of user Britta Simon.</span></span>

   <span data-ttu-id="fc4b7-292">c.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-292">c.</span></span> <span data-ttu-id="fc4b7-293">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-293">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

   <span data-ttu-id="fc4b7-294">d.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-294">d.</span></span> <span data-ttu-id="fc4b7-295">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="fc4b7-296">Creare un utente di test di Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="fc4b7-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="fc4b7-297">In questa sezione viene creato un utente chiamato Britta Simon in Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="fc4b7-298">Collaborare con il [team di supporto clienti di Qlik Sense Enterprise](https://www.qlik.com/us/services/support) per aggiungere gli utenti nella piattaforma Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add the users in the Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="fc4b7-299">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fc4b7-300">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc4b7-300">Assign the Azure AD test user</span></span>

<span data-ttu-id="fc4b7-301">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-301">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qlik Sense Enterprise.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="fc4b7-303">**Per assegnare Britta Simon a Qlik Sense Enterprise, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fc4b7-303">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="fc4b7-304">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-304">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="fc4b7-306">Nell'elenco delle applicazioni selezionare **Qlik Sense Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-306">In the applications list, select **Qlik Sense Enterprise**.</span></span>

    ![Collegamento di Qlik Sense Enterprise nell'elenco delle applicazioni](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="fc4b7-308">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-308">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="fc4b7-310">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-310">Click **Add** button.</span></span> <span data-ttu-id="fc4b7-311">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="fc4b7-313">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-313">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fc4b7-314">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fc4b7-315">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fc4b7-316">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fc4b7-316">Test single sign-on</span></span>

<span data-ttu-id="fc4b7-317">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-317">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fc4b7-318">Quando si fa clic sul riquadro Qlik Sense Enterprise nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fc4b7-318">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fc4b7-319">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fc4b7-319">Additional resources</span></span>

* [<span data-ttu-id="fc4b7-320">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc4b7-320">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fc4b7-321">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc4b7-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

