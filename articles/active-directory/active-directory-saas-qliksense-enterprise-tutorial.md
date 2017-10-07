---
title: 'Esercitazione: Integrazione di Azure Active Directory con Qlik Sense Enterprise | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Qlik senso Enterprise.
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
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="fe1b0-103">Esercitazione: Integrazione di Azure Active Directory con Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="fe1b0-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="fe1b0-104">In questa esercitazione, è illustrato come toointegrate Qlik senso Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe1b0-104">In this tutorial, you learn how toointegrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fe1b0-105">Integrazione di Enterprise senso Qlik con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-105">Integrating Qlik Sense Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fe1b0-106">È possibile controllare in Azure AD che ha accesso tooQlik senso Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-106">You can control in Azure AD who has access tooQlik Sense Enterprise.</span></span>
- <span data-ttu-id="fe1b0-107">È possibile abilitare l'utenti tooautomatically get connesso tooQlik senso Enterprise (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-107">You can enable your users tooautomatically get signed-on tooQlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fe1b0-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fe1b0-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fe1b0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe1b0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fe1b0-110">Prerequisites</span></span>

<span data-ttu-id="fe1b0-111">integrazione di Azure AD con Enterprise senso Qlik tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-111">tooconfigure Azure AD integration with Qlik Sense Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="fe1b0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fe1b0-113">Sottoscrizione di Qlik Sense Enterprise abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fe1b0-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fe1b0-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fe1b0-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fe1b0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fe1b0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe1b0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fe1b0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="fe1b0-118">Scenario description</span></span>
<span data-ttu-id="fe1b0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fe1b0-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fe1b0-121">Aggiunta di Qlik senso Enterprise dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fe1b0-121">Adding Qlik Sense Enterprise from hello gallery</span></span>
2. <span data-ttu-id="fe1b0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe1b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a><span data-ttu-id="fe1b0-123">Aggiunta di Qlik senso Enterprise dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fe1b0-123">Adding Qlik Sense Enterprise from hello gallery</span></span>
<span data-ttu-id="fe1b0-124">integrazione hello tooconfigure di Qlik senso Enterprise in Azure AD, è necessario tooadd Qlik senso Enterprise dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-124">tooconfigure hello integration of Qlik Sense Enterprise into Azure AD, you need tooadd Qlik Sense Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fe1b0-125">**tooadd Qlik senso Enterprise dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-125">**tooadd Qlik Sense Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe1b0-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="fe1b0-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fe1b0-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="fe1b0-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="fe1b0-133">Nella casella di ricerca hello, digitare **Qlik senso Enterprise**selezionare **Qlik senso Enterprise** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-133">In hello search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Enterprise senso Qlik nell'elenco risultati hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fe1b0-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe1b0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fe1b0-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Qlik Sense Enterprise con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fe1b0-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fe1b0-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Qlik senso Enterprise è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Qlik Sense Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="fe1b0-138">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Qlik senso Enterprise richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-138">In other words, a link relationship between an Azure AD user and hello related user in Qlik Sense Enterprise needs toobe established.</span></span>

<span data-ttu-id="fe1b0-139">In Enterprise senso Qlik, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-139">In Qlik Sense Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fe1b0-140">tooconfigure e prova AD Azure single sign-on con Qlik senso Enterprise, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-140">tooconfigure and test Azure AD single sign-on with Qlik Sense Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fe1b0-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fe1b0-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fe1b0-143">**[Creare un utente test Qlik senso Enterprise](#create-a-qlik-sense-enterprise-test-user)**  -toohave un equivalente di Britta Simon Qlik senso organizzazione che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - toohave a counterpart of Britta Simon in Qlik Sense Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fe1b0-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fe1b0-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fe1b0-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe1b0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fe1b0-147">In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Qlik senso Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="fe1b0-148">**tooconfigure AD Azure single sign-on con Qlik senso Enterprise, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-148">**tooconfigure Azure AD single sign-on with Qlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe1b0-149">Nel portale di Azure su hello hello **Qlik senso Enterprise** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-149">In hello Azure portal, on hello **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="fe1b0-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="fe1b0-153">In hello **Qlik senso Enterprise dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-153">On hello **Qlik Sense Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="fe1b0-155">a.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-155">a.</span></span> <span data-ttu-id="fe1b0-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="fe1b0-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="fe1b0-157">Si noti hello barra alla fine di hello dell'URI finale.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-157">Note hello trailing slash at hello end of this URI.</span></span> <span data-ttu-id="fe1b0-158">È obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-158">It is required.</span></span>
    
    <span data-ttu-id="fe1b0-159">b.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-159">b.</span></span> <span data-ttu-id="fe1b0-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="fe1b0-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="fe1b0-161">These values are not real.</span></span> <span data-ttu-id="fe1b0-162">Aggiornamento di questi valori con hello effettivo URL Sign-On e l'identificatore, che vengono descritte più avanti in questa esercitazione o contatto [team di supporto Client di Enterprise senso Qlik](https://www.qlik.com/us/services/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-162">Update these values with hello actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="fe1b0-163">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="fe1b0-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fe1b0-165">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fe1b0-167">Preparare il file di codice XML dei metadati di federazione hello in modo che è possibile caricare tale server senso tooQlik.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-167">Prepare hello Federation Metadata XML file so that you can upload that tooQlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="fe1b0-168">Prima di caricare hello IdP metadati toohello server Qlik senso, il file hello deve toobe modificato tooremove informazioni tooensure il corretto funzionamento tra Azure AD e ha senso Qlik server.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-168">Before uploading hello IdP metadata toohello Qlik Sense server, hello file needs toobe edited tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![Qlik Sense][qs24]
   
    <span data-ttu-id="fe1b0-170">a.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-170">a.</span></span> <span data-ttu-id="fe1b0-171">Aprire il file FederationMetadata hello, che è stato scaricato dal portale di Azure in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-171">Open hello FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="fe1b0-172">b.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-172">b.</span></span> <span data-ttu-id="fe1b0-173">Cercare il valore di hello **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-173">Search for hello value **RoleDescriptor**.</span></span>  <span data-ttu-id="fe1b0-174">Ci sono quattro voci (due coppie di tag di elementi di apertura e di chiusura).</span><span class="sxs-lookup"><span data-stu-id="fe1b0-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="fe1b0-175">c.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-175">c.</span></span> <span data-ttu-id="fe1b0-176">Eliminare tra i tag di elemento RoleDescriptor hello e tutte le informazioni dal file hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-176">Delete hello RoleDescriptor tags and all information in between from hello file.</span></span>
   
    <span data-ttu-id="fe1b0-177">d.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-177">d.</span></span> <span data-ttu-id="fe1b0-178">Salvare il file hello e mantenerlo nelle vicinanze per usare più avanti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-178">Save hello file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="fe1b0-179">Passare toohello Qlik senso Qlik Management Console (QMC) come un utente può creare configurazioni virtuale proxy.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-179">Navigate toohello Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="fe1b0-180">In hello QMC, fare clic su hello **virtuale proxy** voce di menu.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-180">In hello QMC, click on hello **Virtual Proxies** menu item.</span></span>
   
    ![Qlik Sense][qs6] 

9. <span data-ttu-id="fe1b0-182">In basso hello hello, fare clic su hello **Crea nuovo** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-182">At hello bottom of hello screen, click hello **Create new** button.</span></span>
   
    ![Qlik Sense][qs7]

10. <span data-ttu-id="fe1b0-184">verrà visualizzata la schermata di modifica di Hello virtuale proxy.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-184">hello Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="fe1b0-185">In hello lato destro dello schermo hello è un menu di rendere visibili le opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-185">On hello right side of hello screen is a menu for making configuration options visible.</span></span>
   
    ![Qlik Sense][qs9]

11. <span data-ttu-id="fe1b0-187">Con l'opzione di menu identificazione hello selezionata, immettere informazioni di identificazione per la configurazione del proxy virtuale Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-187">With hello Identification menu option checked, enter hello identifying information for hello Azure virtual proxy configuration.</span></span>
    
    ![Qlik Sense][qs8]  
    
    <span data-ttu-id="fe1b0-189">a.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-189">a.</span></span> <span data-ttu-id="fe1b0-190">Hello **descrizione** campo è un nome descrittivo per la configurazione del proxy virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-190">hello **Description** field is a friendly name for hello virtual proxy configuration.</span></span>  <span data-ttu-id="fe1b0-191">Immettere un valore per la descrizione.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="fe1b0-192">b.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-192">b.</span></span> <span data-ttu-id="fe1b0-193">Hello **prefisso** campo identifica l'endpoint proxy virtuale hello per la connessione tooQlik senso con Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-193">hello **Prefix** field identifies hello virtual proxy endpoint for connecting tooQlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="fe1b0-194">Immettere un nome di prefisso univoco per il proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="fe1b0-195">c.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-195">c.</span></span> <span data-ttu-id="fe1b0-196">**Timeout di inattività della sessione (minuti)** timeout hello per le connessioni tramite proxy virtuale.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-196">**Session inactivity timeout (minutes)** is hello timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="fe1b0-197">d.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-197">d.</span></span> <span data-ttu-id="fe1b0-198">Hello **nome intestazione cookie della sessione** è l'archiviazione di hello cookie nome hello identificatore di sessione per hello sessione senso Qlik un utente riceve dopo l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-198">hello **Session cookie header name** is hello cookie name storing hello session identifier for hello Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="fe1b0-199">Il nome deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-199">This name must be unique.</span></span>

12. <span data-ttu-id="fe1b0-200">Fare clic su hello autenticazione menu opzione toomake è visibile.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-200">Click on hello Authentication menu option toomake it visible.</span></span>  <span data-ttu-id="fe1b0-201">verrà visualizzata la schermata di autenticazione Hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-201">hello Authentication screen appears.</span></span>
    
    ![Qlik Sense][qs10]
    
    <span data-ttu-id="fe1b0-203">a.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-203">a.</span></span> <span data-ttu-id="fe1b0-204">Hello **modalità di accesso anonimo** elenco a discesa determina se gli utenti anonimi possono accedere senso Qlik tramite proxy virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-204">hello **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through hello virtual proxy.</span></span>  <span data-ttu-id="fe1b0-205">opzione predefinita di Hello non è l'utente anonimo.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-205">hello default option is No anonymous user.</span></span>
    
    <span data-ttu-id="fe1b0-206">b.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-206">b.</span></span> <span data-ttu-id="fe1b0-207">Hello **metodo di autenticazione** elenco a discesa determina l'utilizzo di proxy virtuale hello hello autenticazione schema.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-207">hello **Authentication method** drop-down determines hello authentication scheme hello virtual proxy will use.</span></span>  <span data-ttu-id="fe1b0-208">Selezionare SAML dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-208">Select SAML from hello drop-down list.</span></span>  <span data-ttu-id="fe1b0-209">Verranno di conseguenza visualizzate altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="fe1b0-210">c.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-210">c.</span></span> <span data-ttu-id="fe1b0-211">In hello **il campo URI host SAML**, gli utenti di nome host di input hello immettere tooaccess Qlik senso attraverso questo proxy virtuale SAML.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-211">In hello **SAML host URI field**, input hello hostname users enter tooaccess Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="fe1b0-212">il nome host Hello è uri hello del server ha senso Qlik hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-212">hello hostname is hello uri of hello Qlik Sense server.</span></span>
    
    <span data-ttu-id="fe1b0-213">d.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-213">d.</span></span> <span data-ttu-id="fe1b0-214">In hello **ID entità SAML**, immettere hello stesso valore immesso per il campo hello SAML host URI.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-214">In hello **SAML entity ID**, enter hello same value entered for hello SAML host URI field.</span></span>
    
    <span data-ttu-id="fe1b0-215">e.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-215">e.</span></span> <span data-ttu-id="fe1b0-216">Hello **SAML IdP metadata** file hello modificato in precedenza in hello **modificare i metadati di federazione dalla configurazione di Azure AD** sezione.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-216">hello **SAML IdP metadata** is hello file edited earlier in hello **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="fe1b0-217">**Prima di caricare hello IdP metadata, file hello deve modificare toobe** tooremove informazioni tooensure il corretto funzionamento tra Azure AD e ha senso Qlik server.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-217">**Before uploading hello IdP metadata, hello file needs toobe edited** tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="fe1b0-218">**Se il file hello è ancora toobe modificato, fare riferimento toohello istruzioni sopra riportate.**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-218">**Please refer toohello instructions above if hello file has yet toobe edited.**</span></span>  <span data-ttu-id="fe1b0-219">Se file hello è stato modificato fare clic su pulsante hello e tooupload file di metadati modificati hello selezionare la configurazione del proxy virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-219">If hello file has been edited click on hello Browse button and select hello edited metadata file tooupload it toohello virtual proxy configuration.</span></span>
    
    <span data-ttu-id="fe1b0-220">f.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-220">f.</span></span> <span data-ttu-id="fe1b0-221">Immettere hello di attributo nome o lo schema di riferimento per attributo SAML hello che rappresenta hello **UserID** Azure AD invia toohello server Qlik senso.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-221">Enter hello attribute name or schema reference for hello SAML attribute representing hello **UserID** Azure AD sends toohello Qlik Sense server.</span></span>  <span data-ttu-id="fe1b0-222">Informazioni di riferimento dello schema sono disponibile in hello Azure app schermate post-configurazione.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-222">Schema reference information is available in hello Azure app screens post configuration.</span></span>  <span data-ttu-id="fe1b0-223">attributo del nome hello toouse immettere `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-223">toouse hello name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="fe1b0-224">g.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-224">g.</span></span> <span data-ttu-id="fe1b0-225">Immettere il valore di hello per hello **directory utente** che verranno collegati toousers durante l'autenticazione server senso tooQlik tramite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-225">Enter hello value for hello **user directory** that will be attached toousers when they authenticate tooQlik Sense server through Azure AD.</span></span>  <span data-ttu-id="fe1b0-226">I valori hardcoded devono essere racchiusi tra **parentesi quadre []**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="fe1b0-227">un attributo inviato nell'asserzione SAML per Azure AD, hello toouse immettere il nome di hello dell'attributo hello in questa casella di testo **senza** le parentesi quadre.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-227">toouse an attribute sent in hello Azure AD SAML assertion, enter hello name of hello attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="fe1b0-228">h.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-228">h.</span></span> <span data-ttu-id="fe1b0-229">Hello **algoritmo di firma SAML** hello di set di configurazione del proxy virtuale hello di firma del certificato del servizio provider (in questo server ha senso Qlik case).</span><span class="sxs-lookup"><span data-stu-id="fe1b0-229">hello **SAML signing algorithm** sets hello service provider (in this case Qlik Sense server) certificate signing for hello virtual proxy configuration.</span></span>  <span data-ttu-id="fe1b0-230">Se il server ha senso Qlik utilizza un certificato attendibile generato utilizzando Microsoft Enhanced RSA e AES Cryptographic Provider, modificare algoritmo di firma SAML hello troppo**SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change hello SAML signing algorithm too**SHA-256**.</span></span>
    
    <span data-ttu-id="fe1b0-231">i.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-231">i.</span></span> <span data-ttu-id="fe1b0-232">sezione di mapping di attributi SAML Hello consente di attributi aggiuntivi quali gruppi toobe inviati tooQlik senso per l'utilizzo nelle regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-232">hello SAML attribute mapping section allows for additional attributes like groups toobe sent tooQlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="fe1b0-233">Fare clic su hello **il bilanciamento del carico** toomake opzione di menu è visibile.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-233">Click on hello **LOAD BALANCING** menu option toomake it visible.</span></span>  <span data-ttu-id="fe1b0-234">verrà visualizzata la schermata di bilanciamento del carico Hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-234">hello Load Balancing screen appears.</span></span>
    
    ![Qlik Sense][qs11]

14. <span data-ttu-id="fe1b0-236">Fare clic su hello **Aggiungi nuovo nodo server** pulsante, selezionare motore o nodi Qlik senso verranno inviato a scopo di bilanciamento del carico di toofor di sessioni e fare clic su hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-236">Click on hello **Add new server node** button, select engine node or nodes Qlik Sense will send sessions toofor load balancing purposes, and click hello **Add** button.</span></span>
    
    ![Qlik Sense][qs12]

15. <span data-ttu-id="fe1b0-238">Fare clic su toomake opzione di menu Avanzate hello è visibile.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-238">Click on hello Advanced menu option toomake it visible.</span></span> <span data-ttu-id="fe1b0-239">verrà visualizzata la schermata di Hello avanzate.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-239">hello Advanced screen appears.</span></span>
    
    ![Qlik Sense][qs13]
    
    <span data-ttu-id="fe1b0-241">elenco vuoto di Hello Host identifica i nomi host che vengono accettati quando ci si connette il server ha senso Qlik toohello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-241">hello Host white list identifies hostnames that are accepted when connecting toohello Qlik Sense server.</span></span>  <span data-ttu-id="fe1b0-242">**Immettere il nome host hello gli utenti specificheranno durante la connessione server senso tooQlik.**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-242">**Enter hello hostname users will specify when connecting tooQlik Sense server.**</span></span> <span data-ttu-id="fe1b0-243">nome host Hello è hello stesso valore di hello SAML host uri senza hello https://.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-243">hello hostname is hello same value as hello SAML host uri without hello https://.</span></span>

16. <span data-ttu-id="fe1b0-244">Fare clic su hello **applica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-244">Click hello **Apply** button.</span></span>
    
    ![Qlik Sense][qs14]

17. <span data-ttu-id="fe1b0-246">Fare clic su OK tooaccept messaggio di avviso hello indicante proxy proxy virtuale toohello collegato verrà riavviato.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-246">Click OK tooaccept hello warning message that states proxies linked toohello virtual proxy will be restarted.</span></span>
    
    ![Qlik Sense][qs15]

18. <span data-ttu-id="fe1b0-248">Sul lato destro di hello della schermata ciao, viene visualizzato dal menu di elementi associati hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-248">On hello right side of hello screen, hello Associated items menu appears.</span></span>  <span data-ttu-id="fe1b0-249">Fare clic su hello **proxy** opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-249">Click on hello **Proxies** menu option.</span></span>
    
    ![Qlik Sense][qs16]

19. <span data-ttu-id="fe1b0-251">verrà visualizzata la schermata di Hello proxy.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-251">hello proxy screen appears.</span></span>  <span data-ttu-id="fe1b0-252">Fare clic su hello **collegamento** pulsante hello inferiore toolink proxy virtuale toohello proxy.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-252">Click hello **Link** button at hello bottom toolink a proxy toohello virtual proxy.</span></span>
    
    ![Qlik Sense][qs17]

20. <span data-ttu-id="fe1b0-254">Nodo proxy selezionare hello che supporterà questa connessione proxy virtuale e fare clic su hello **collegamento** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-254">Select hello proxy node that will support this virtual proxy connection and click hello **Link** button.</span></span>  <span data-ttu-id="fe1b0-255">Dopo aver collegato, proxy hello sarà elencata sotto proxy associati.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-255">After linking, hello proxy will be listed under associated proxies.</span></span>
    
    ![Qlik Sense][qs18]
  
    ![Qlik Sense][qs19]

21. <span data-ttu-id="fe1b0-258">Dopo circa cinque secondi tooten, hello messaggio QMC aggiornamento verranno visualizzati.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-258">After about five tooten seconds, hello Refresh QMC message will appear.</span></span>  <span data-ttu-id="fe1b0-259">Fare clic su hello **QMC aggiornamento** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-259">Click hello **Refresh QMC** button.</span></span>
    
    ![Qlik Sense][qs20]

22. <span data-ttu-id="fe1b0-261">Quando viene aggiornato hello QMC, fare clic su hello **virtuale proxy** voce di menu.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-261">When hello QMC refreshes, click on hello **Virtual proxies** menu item.</span></span> <span data-ttu-id="fe1b0-262">nuova voce di proxy virtuale SAML Hello è elencato nella tabella hello nella schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-262">hello new SAML virtual proxy entry is listed in hello table on hello screen.</span></span>  <span data-ttu-id="fe1b0-263">Singolo clic sulla voce proxy virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-263">Single click on hello virtual proxy entry.</span></span>
    
    ![Qlik Sense][qs51]

23. <span data-ttu-id="fe1b0-265">In basso hello hello, pulsante di hello SP scaricare i metadati verrà attivati.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-265">At hello bottom of hello screen, hello Download SP metadata button will activate.</span></span>  <span data-ttu-id="fe1b0-266">Fare clic su hello **scaricare SP metadata** file tooa di pulsante toosave hello metadati.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-266">Click hello **Download SP metadata** button toosave hello metadata tooa file.</span></span>
    
    ![Qlik Sense][qs52]

24. <span data-ttu-id="fe1b0-268">File di metadati sp hello aperto.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-268">Open hello sp metadata file.</span></span>  <span data-ttu-id="fe1b0-269">Osservare hello **entityID** voce e hello **AssertionConsumerService** voce.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-269">Observe hello **entityID** entry and hello **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="fe1b0-270">Questi valori sono equivalente toohello **identificatore** hello e **URL di accesso** nella configurazione dell'applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-270">These values are equivalent toohello **Identifier** and hello **Sign on URL** in hello Azure AD application configuration.</span></span> <span data-ttu-id="fe1b0-271">Incollare questi valori in hello **Qlik senso Enterprise dominio e gli URL** sezione di configurazione dell'applicazione hello Azure AD se essi non corrispondono, quindi è necessario sostituirli nella configurazione guidata di Azure AD App hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-271">Paste these values in hello **Qlik Sense Enterprise Domain and URLs** section in hello Azure AD application configuration if they are not matching, then you should replace them in hello Azure AD App configuration wizard.</span></span>
    
    ![Qlik Sense][qs53]

> [!TIP]
> <span data-ttu-id="fe1b0-273">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="fe1b0-273">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fe1b0-274">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-274">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fe1b0-275">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fe1b0-275">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fe1b0-276">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe1b0-276">Create an Azure AD test user</span></span>
<span data-ttu-id="fe1b0-277">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-277">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="fe1b0-279">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-279">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe1b0-280">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-280">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

   ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fe1b0-282">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-282">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

   ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fe1b0-284">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-284">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

   ![pulsante Aggiungi Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fe1b0-286">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-286">In hello **User** dialog box, perform hello following steps:</span></span>

   ![finestra di dialogo utente Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="fe1b0-288">a.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-288">a.</span></span> <span data-ttu-id="fe1b0-289">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-289">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="fe1b0-290">b.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-290">b.</span></span> <span data-ttu-id="fe1b0-291">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-291">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="fe1b0-292">c.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-292">c.</span></span> <span data-ttu-id="fe1b0-293">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-293">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="fe1b0-294">d.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-294">d.</span></span> <span data-ttu-id="fe1b0-295">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="fe1b0-296">Creare un utente di test di Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="fe1b0-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="fe1b0-297">In questa sezione viene creato un utente chiamato Britta Simon in Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="fe1b0-298">Lavorare con [team di supporto Client di Enterprise senso Qlik](https://www.qlik.com/us/services/support) per aggiungere gli utenti di hello nella piattaforma Qlik senso Enterprise hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add hello users in hello Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="fe1b0-299">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fe1b0-300">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe1b0-300">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fe1b0-301">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooQlik senso Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-301">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQlik Sense Enterprise.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="fe1b0-303">**tooassign Britta Simon tooQlik senso Enterprise, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-303">**tooassign Britta Simon tooQlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe1b0-304">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-304">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="fe1b0-306">Nell'elenco di applicazioni hello, selezionare **Qlik senso Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-306">In hello applications list, select **Qlik Sense Enterprise**.</span></span>

    ![collegamento Qlik senso Enterprise Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="fe1b0-308">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-308">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="fe1b0-310">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-310">Click **Add** button.</span></span> <span data-ttu-id="fe1b0-311">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="fe1b0-313">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-313">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fe1b0-314">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fe1b0-315">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fe1b0-316">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fe1b0-316">Test single sign-on</span></span>

<span data-ttu-id="fe1b0-317">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-317">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fe1b0-318">Quando si fa clic su riquadro Qlik senso Enterprise hello in hello Pannello di accesso, è necessario ottenere applicazione Enterprise senso Qlik tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-318">When you click hello Qlik Sense Enterprise tile in hello Access Panel, you should get automatically signed-on tooyour Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fe1b0-319">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fe1b0-319">Additional resources</span></span>

* [<span data-ttu-id="fe1b0-320">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe1b0-320">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fe1b0-321">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe1b0-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

