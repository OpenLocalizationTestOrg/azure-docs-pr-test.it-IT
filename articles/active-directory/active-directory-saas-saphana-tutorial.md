---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP HANA | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAP HANA.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="0751c-103">Esercitazione: Integrazione di Azure Active Directory con SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0751c-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="0751c-104">In questa esercitazione, è illustrato come toointegrate SAP HANA con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0751c-104">In this tutorial, you learn how toointegrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0751c-105">Integrazione di SAP HANA con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0751c-105">Integrating SAP HANA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0751c-106">È possibile controllare in Azure AD che ha accesso tooSAP HANA</span><span class="sxs-lookup"><span data-stu-id="0751c-106">You can control in Azure AD who has access tooSAP HANA</span></span>
- <span data-ttu-id="0751c-107">È possibile abilitare l'utenti tooautomatically get connesso tooSAP HANA (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0751c-107">You can enable your users tooautomatically get signed-on tooSAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0751c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0751c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0751c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0751c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0751c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0751c-110">Prerequisites</span></span>

<span data-ttu-id="0751c-111">integrazione di Azure AD con SAP HANA tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0751c-111">tooconfigure Azure AD integration with SAP HANA, you need hello following items:</span></span>

- <span data-ttu-id="0751c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0751c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0751c-113">Sottoscrizione di SAP HANA abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0751c-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="0751c-114">Istanza di HANA in esecuzione in qualsiasi VM IaaS pubblica, locale o di Azure oppure in istanze di grandi dimensioni di SAP in Azure</span><span class="sxs-lookup"><span data-stu-id="0751c-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="0751c-115">Interfaccia Web di amministrazione XSA Hello nonché HANA Studio installato nell'istanza HANA hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-115">hello XSA Administration Web Interface as well as HANA Studio installed on hello HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="0751c-116">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0751c-116">tootest hello steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="0751c-117">Prima di tutto testare integrazione hello nello sviluppo e gestione temporanea di ambiente dell'applicazione hello e quindi utilizzare hello ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0751c-117">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="0751c-118">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="0751c-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0751c-119">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0751c-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0751c-120">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0751c-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0751c-121">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0751c-121">Scenario description</span></span>
<span data-ttu-id="0751c-122">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0751c-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0751c-123">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="0751c-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0751c-124">Aggiunta di SAP HANA dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0751c-124">Adding SAP HANA from hello gallery</span></span>
2. <span data-ttu-id="0751c-125">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0751c-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-hello-gallery"></a><span data-ttu-id="0751c-126">Aggiunta di SAP HANA dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0751c-126">Adding SAP HANA from hello gallery</span></span>
<span data-ttu-id="0751c-127">integrazione hello tooconfigure di SAP HANA in Azure AD, è necessario tooadd SAP HANA dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0751c-127">tooconfigure hello integration of SAP HANA into Azure AD, you need tooadd SAP HANA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0751c-128">**tooadd SAP HANA dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0751c-128">**tooadd SAP HANA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0751c-129">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0751c-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="0751c-131">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0751c-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0751c-132">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0751c-132">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="0751c-134">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0751c-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="0751c-136">Nella casella di ricerca hello, digitare **SAP HANA**selezionare **SAP HANA** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0751c-136">In hello search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button tooadd hello application.</span></span> 

    ![Nuova applicazione Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0751c-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0751c-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0751c-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP HANA usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0751c-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0751c-140">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SAP HANA è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0751c-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA is tooa user in Azure AD.</span></span> <span data-ttu-id="0751c-141">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SAP HANA deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="0751c-141">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA needs toobe established.</span></span>

<span data-ttu-id="0751c-142">In SAP HANA, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-142">In SAP HANA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0751c-143">tooconfigure e prova AD Azure single sign-on con SAP HANA, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="0751c-143">tooconfigure and test Azure AD single sign-on with SAP HANA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0751c-144">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0751c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0751c-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0751c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0751c-146">**[Creazione di un utente test SAP HANA](#creating-a-sap-hana-test-user)**  -toohave un equivalente di Britta Simon in SAP HANA che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0751c-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - toohave a counterpart of Britta Simon in SAP HANA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0751c-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0751c-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0751c-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="0751c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0751c-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0751c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0751c-150">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0751c-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="0751c-151">**Azure AD tooconfigure single sign-on con SAP HANA, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0751c-151">**tooconfigure Azure AD single sign-on with SAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="0751c-152">Nel portale di Azure su hello hello **SAP HANA** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0751c-152">In hello Azure portal, on hello **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0751c-154">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0751c-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="0751c-156">In hello **URL e SAP HANA dominio** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0751c-156">On hello **SAP HANA Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="0751c-158">a.</span><span class="sxs-lookup"><span data-stu-id="0751c-158">a.</span></span> <span data-ttu-id="0751c-159">In hello **identificatore** casella di testo, tipo:`HA100`</span><span class="sxs-lookup"><span data-stu-id="0751c-159">In hello **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="0751c-160">b.</span><span class="sxs-lookup"><span data-stu-id="0751c-160">b.</span></span> <span data-ttu-id="0751c-161">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="0751c-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0751c-162">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0751c-162">These values are not real.</span></span> <span data-ttu-id="0751c-163">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-163">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0751c-164">Contatto [team di supporto di SAP HANA Client](https://cloudplatform.sap.com/contact.html) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="0751c-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="0751c-165">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0751c-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="0751c-167">Se il certificato non è attivo renderlo attivo facendo hello "creare nuovo certificato active" casella di controllo in hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0751c-167">If certificate is not active then make it active by clicking hello “Make new certificate active” checkbox in hello Azure AD.</span></span> 

5. <span data-ttu-id="0751c-168">Applicazione SAP HANA prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="0751c-168">SAP HANA application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="0751c-169">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="0751c-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="0751c-170">Di seguito è stato eseguito il mapping hello **identificatore utente** con **ExtractMailPrefix()** funzione **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="0751c-170">Here we have mapped hello **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="0751c-171">In questo modo il valore di prefisso hello messaggi di posta elettronica dell'utente hello che è hello ID utente univoco.</span><span class="sxs-lookup"><span data-stu-id="0751c-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="0751c-172">Viene inviato toohello applicazione SAP HANA in ogni risposta con esito positivo.</span><span class="sxs-lookup"><span data-stu-id="0751c-172">This is sent toohello SAP HANA application in every successful response.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="0751c-174">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="0751c-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="0751c-175">a.</span><span class="sxs-lookup"><span data-stu-id="0751c-175">a.</span></span> <span data-ttu-id="0751c-176">In hello **identificatore utente** elenco a discesa, seleziona **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="0751c-176">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="0751c-177">b.</span><span class="sxs-lookup"><span data-stu-id="0751c-177">b.</span></span> <span data-ttu-id="0751c-178">In hello **posta** elenco a discesa, seleziona **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="0751c-178">In hello **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="0751c-179">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0751c-179">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="0751c-181">tooconfigure single sign-on sul **SAP HANA** lato, account di accesso tooyour **HANA XSA Web Console** esplorando toohello rispettivi endpoint HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0751c-181">tooconfigure single sign-on on **SAP HANA** side, login tooyour **HANA XSA Web Console**  by browsing toohello respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="0751c-182">Nella configurazione predefinita di hello, hello URL reindirizza hello richiesta tooa schermata di accesso, che richiede credenziali hello di un processo accesso autenticato di SAP HANA database utente toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-182">In hello default configuration, hello URL redirects hello request tooa logon screen, which requires hello credentials of an authenticated SAP HANA database user toocomplete hello logon process.</span></span> <span data-ttu-id="0751c-183">utente di Hello che effettua l'accesso deve disporre di attività di amministrazione di hello privilegi necessari tooperform SAML.</span><span class="sxs-lookup"><span data-stu-id="0751c-183">hello user who logs on must have hello privileges required tooperform SAML administration tasks.</span></span>

9. <span data-ttu-id="0751c-184">Nell'interfaccia Web XSA hello, passare troppo**Provider di identità SAML** e da lì, fare clic su hello **"+"** -pulsante nella parte inferiore di hello del riquadro di aggiungere informazioni sul Provider di identità di hello schermata toodisplay hello ed eseguire Hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0751c-184">In hello XSA Web Interface, navigate too**SAML Identity Provider** and from there, click hello **“+”** -button on hello bottom of hello screen toodisplay hello Add Identity Provider Info pane and perform hello following steps:</span></span>

    ![Aggiungi provider di identità](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="0751c-186">a.</span><span class="sxs-lookup"><span data-stu-id="0751c-186">a.</span></span> <span data-ttu-id="0751c-187">In hello **aggiungere informazioni sul Provider di identità** riquadro contenuto di hello Incolla di hello Metadata XML, che è stato scaricato dal portale di Azure in hello **metadati** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="0751c-187">In hello **Add Identity Provider Info** pane, paste hello contents of hello Metadata XML, which you have downloaded from Azure portal into hello **Metadata** textbox.</span></span>

    ![Impostazioni di aggiunta del provider di identità](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="0751c-189">b.</span><span class="sxs-lookup"><span data-stu-id="0751c-189">b.</span></span> <span data-ttu-id="0751c-190">Se il contenuto di hello del documento XML hello è valido, hello analisi del processo estrae tooinsert informazioni necessarie hello in hello **oggetto, ID entità e dell'autorità di certificazione** campi di dati generale hello area dello schermo e hello campi URL hello Schermata area di destinazione, ad esempio,  **URL di Base e l'URL di ADFS (*)**.</span><span class="sxs-lookup"><span data-stu-id="0751c-190">If hello contents of hello XML document are valid, hello parsing process extracts hello information required tooinsert into hello **Subject, Entity ID, and Issuer** fields in hello General Data screen area, and hello URL fields in hello Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Impostazioni di aggiunta del provider di identità](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="0751c-192">c.</span><span class="sxs-lookup"><span data-stu-id="0751c-192">c.</span></span> <span data-ttu-id="0751c-193">Nella casella Nome hello di hello dati generale area dello schermo, immettere un nome per il nuovo provider di identità SAML SSO di hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-193">In hello Name box of hello General Data screen area, enter a name for hello new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="0751c-194">nome Hello del provider di identità SAML hello è obbligatoria e deve essere univoco. viene visualizzato nell'elenco hello di IDPs SAML disponibili che è visibile, se si seleziona SAML come metodo di autenticazione hello per toouse applicazioni SAP HANA XS, ad esempio, nell'area dello schermo di autenticazione hello hello XS artefatto dello strumento di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="0751c-194">hello name of hello SAML IDP is mandatory and must be unique; it appears in hello list of available SAML IDPs that is displayed, if you select SAML as hello authentication method for SAP HANA XS applications toouse, for example, in hello Authentication screen area of hello XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="0751c-195">Salvare i dettagli di hello del nuovo provider di identità SAML hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-195">Save hello details of hello new SAML identity provider.</span></span> <span data-ttu-id="0751c-196">Scegliere **salvare** toosave hello dettagli del provider di identità SAML hello e hello nuovo provider di identità SAML toohello elenco di noti IDPs SAML.</span><span class="sxs-lookup"><span data-stu-id="0751c-196">Choose **Save** toosave hello details of hello SAML identity provider and add hello new SAML IDP toohello list of known SAML IDPs.</span></span>

    ![Pulsante per il salvataggio](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="0751c-198">In Studio HANA all'interno delle proprietà di sistema hello di hello **configurazione** scheda, filtrare solo le impostazioni da **saml** e regolare hello **assertion_timeout** da **10 sec** troppo**120 secondi**.</span><span class="sxs-lookup"><span data-stu-id="0751c-198">In HANA Studio within hello system properties of hello **Configuration** tab, just filter settings by **saml** and adjust hello **assertion_timeout** from **10 sec** too**120 sec**.</span></span>

    ![Impostazione assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="0751c-200">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="0751c-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0751c-201">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0751c-202">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0751c-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0751c-203">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0751c-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="0751c-204">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0751c-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0751c-206">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0751c-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0751c-207">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0751c-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0751c-209">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0751c-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0751c-211">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0751c-213">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0751c-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0751c-215">a.</span><span class="sxs-lookup"><span data-stu-id="0751c-215">a.</span></span> <span data-ttu-id="0751c-216">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0751c-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0751c-217">b.</span><span class="sxs-lookup"><span data-stu-id="0751c-217">b.</span></span> <span data-ttu-id="0751c-218">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0751c-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0751c-219">c.</span><span class="sxs-lookup"><span data-stu-id="0751c-219">c.</span></span> <span data-ttu-id="0751c-220">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="0751c-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0751c-221">d.</span><span class="sxs-lookup"><span data-stu-id="0751c-221">d.</span></span> <span data-ttu-id="0751c-222">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0751c-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="0751c-223">Creazione di un utente di test di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0751c-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="0751c-224">toolog agli utenti di Azure AD tooenable in tooSAP HANA, è necessario eseguirne il provisioning in SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0751c-224">tooenable Azure AD users toolog in tooSAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="0751c-225">SAP HANA supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0751c-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="0751c-226">Se è necessario un utente toocreate manualmente, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0751c-226">If you need toocreate a user manually, perform hello following steps:</span></span>

>[!Note]
><span data-ttu-id="0751c-227">È possibile modificare l'autenticazione di hello esterno utilizzato dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-227">You can change hello external authentication used by hello user.</span></span>
<span data-ttu-id="0751c-228">Gli utenti esterni vengono autenticati mediante un sistema esterno, ad esempio un sistema Kerberos.</span><span class="sxs-lookup"><span data-stu-id="0751c-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="0751c-229">Per informazioni dettagliate sulle identità esterne, contattare l'[amministratore di dominio](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="0751c-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="0751c-230">Aprire hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) come amministratore e abilitare hello database utente per SSO SAML.</span><span class="sxs-lookup"><span data-stu-id="0751c-230">Open hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable hello DB-User for SAML SSO.</span></span>

    ![crea utente](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="0751c-232">Segni di graduazione hello casella di controllo invisibile toohello a sinistra della **SAML** e seguire il collegamento di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-232">Tick hello invisible checkbox toohello left of **SAML** and follow hello Configure link.</span></span>

3. <span data-ttu-id="0751c-233">Fare clic su **Aggiungi** tooadd hello provider di identità SAML e fare clic su **OK** selezionando hello provider di identità SAML appropriato.</span><span class="sxs-lookup"><span data-stu-id="0751c-233">Click **Add** tooadd hello SAML IDP and click **OK** selecting hello appropriate SAML IDP.</span></span>

4. <span data-ttu-id="0751c-234">Aggiungere hello **identità esterna** (es.</span><span class="sxs-lookup"><span data-stu-id="0751c-234">Add hello **External Identity** (ex.</span></span> <span data-ttu-id="0751c-235">BrittaSimon) oppure scegliere **"Any"** (Qualsiasi) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0751c-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="0751c-236">Se "ANY" casella di controllo è deselezionata, il nome utente hello in HANA deve tooexactly corrispondenza hello nome utente hello in hello UPN prima il suffisso di dominio hello (vale a dire BrittaSimon@contoso.com diventerebbe BrittaSimon in HANA).</span><span class="sxs-lookup"><span data-stu-id="0751c-236">If "ANY" check-box is not checked, then hello user name in HANA needs tooexactly match hello name of hello user in hello UPN before hello domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="0751c-237">A scopo di test, assegnare tutte **"XS"** utente toohello ruoli.</span><span class="sxs-lookup"><span data-stu-id="0751c-237">For testing purposes, assign all **"XS"** roles toohello user.</span></span>

    ![assegnazione di ruoli](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="0751c-239">È consigliabile assegnare solo le autorizzazioni appropriate per il caso d'uso.</span><span class="sxs-lookup"><span data-stu-id="0751c-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="0751c-240">Salvare utente hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-240">Save hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0751c-241">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0751c-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0751c-242">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0751c-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP HANA.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="0751c-244">**tooassign Britta Simon tooSAP HANA, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0751c-244">**tooassign Britta Simon tooSAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="0751c-245">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0751c-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0751c-247">Nell'elenco di applicazioni hello, selezionare **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="0751c-247">In hello applications list, select **SAP HANA**.</span></span>

    ![Assegna utente](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="0751c-249">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0751c-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. <span data-ttu-id="0751c-251">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0751c-251">Click **Add** button.</span></span> <span data-ttu-id="0751c-252">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0751c-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="0751c-254">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="0751c-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0751c-255">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0751c-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0751c-256">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0751c-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0751c-257">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0751c-257">Testing single sign-on</span></span>

<span data-ttu-id="0751c-258">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0751c-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0751c-259">Quando si fa clic su riquadro SAP HANA hello in hello Pannello di accesso, è necessario ottenere l'applicazione SAP HANA tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="0751c-259">When you click hello SAP HANA tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA application.</span></span>
<span data-ttu-id="0751c-260">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0751c-260">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0751c-261">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0751c-261">Additional resources</span></span>

* [<span data-ttu-id="0751c-262">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0751c-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0751c-263">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0751c-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

