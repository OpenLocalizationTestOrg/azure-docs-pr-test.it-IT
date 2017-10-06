---
title: Directory Federation Services aaaActive gestione e la personalizzazione con Azure AD Connect | Documenti Microsoft
description: Gestione di AD FS con Azure AD Connect e personalizzazione dell'esperienza utente di accesso ad AD FS con Azure AD Connect e PowerShell.
keywords: AD FS, ADFS, gestione di AD FS, AAD Connect, Connect, accesso, personalizzazione di AD FS, ripristino trust, O365, federazione, relying party
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="94ad1-104">Gestire e personalizzare Active Directory Federation Services con Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="94ad1-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="94ad1-105">Questo articolo viene descritto come toomanage e personalizzare Active Directory Federation Services (ADFS) con Connect di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94ad1-105">This article describes how toomanage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="94ad1-106">Include inoltre altre attività comuni di ADFS che toodo potrebbe essere necessario per completare la configurazione di una farm di ADFS.</span><span class="sxs-lookup"><span data-stu-id="94ad1-106">It also includes other common AD FS tasks that you might need toodo for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="94ad1-107">Argomento</span><span class="sxs-lookup"><span data-stu-id="94ad1-107">Topic</span></span> | <span data-ttu-id="94ad1-108">Contenuto</span><span class="sxs-lookup"><span data-stu-id="94ad1-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="94ad1-109">**Gestire AD FS**</span><span class="sxs-lookup"><span data-stu-id="94ad1-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="94ad1-110">Ripristino hello trust</span><span class="sxs-lookup"><span data-stu-id="94ad1-110">Repair hello trust</span></span>](#repairthetrust) |<span data-ttu-id="94ad1-111">Federazione hello toorepair come attendibile con Office 365.</span><span class="sxs-lookup"><span data-stu-id="94ad1-111">How toorepair hello federation trust with Office 365.</span></span> |
| [<span data-ttu-id="94ad1-112">Attuare la federazione con Azure AD mediante l'ID di accesso alternativo </span><span class="sxs-lookup"><span data-stu-id="94ad1-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="94ad1-113">Configurazione della federazione usando l'ID di accesso alternativo</span><span class="sxs-lookup"><span data-stu-id="94ad1-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="94ad1-114">Aggiungere un server AD FS</span><span class="sxs-lookup"><span data-stu-id="94ad1-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="94ad1-115">Come tooexpand ADFS farm con un server AD FS aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="94ad1-115">How tooexpand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="94ad1-116">Aggiungere un server proxy applicazione Web AD FS</span><span class="sxs-lookup"><span data-stu-id="94ad1-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="94ad1-117">La modalità della farm con un server Proxy applicazione Web (WAP) aggiuntivo tooexpand AD FS.</span><span class="sxs-lookup"><span data-stu-id="94ad1-117">How tooexpand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="94ad1-118">Aggiunta di un dominio federato</span><span class="sxs-lookup"><span data-stu-id="94ad1-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="94ad1-119">Come tooadd un dominio federato.</span><span class="sxs-lookup"><span data-stu-id="94ad1-119">How tooadd a federated domain.</span></span> |
| [<span data-ttu-id="94ad1-120">Aggiorna il certificato SSL hello</span><span class="sxs-lookup"><span data-stu-id="94ad1-120">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="94ad1-121">Hello tooupdate SSL come certificato per una farm ADFS.</span><span class="sxs-lookup"><span data-stu-id="94ad1-121">How tooupdate hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="94ad1-122">**Personalizzare AD FS**</span><span class="sxs-lookup"><span data-stu-id="94ad1-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="94ad1-123">Aggiungere un'illustrazione o il logo personalizzato della società</span><span class="sxs-lookup"><span data-stu-id="94ad1-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="94ad1-124">Come toocustomize AD FS sign-in di pagina con un logo della società e l'illustrazione.</span><span class="sxs-lookup"><span data-stu-id="94ad1-124">How toocustomize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="94ad1-125">Aggiungere una descrizione di accesso</span><span class="sxs-lookup"><span data-stu-id="94ad1-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="94ad1-126">Tooadd un Accedi alla pagina come descrizione.</span><span class="sxs-lookup"><span data-stu-id="94ad1-126">How tooadd a sign-in page description.</span></span> |
| [<span data-ttu-id="94ad1-127">Modificare le regole attestazioni per AD FS</span><span class="sxs-lookup"><span data-stu-id="94ad1-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="94ad1-128">Toomodify AD FS come attestazioni per vari scenari di federazione.</span><span class="sxs-lookup"><span data-stu-id="94ad1-128">How toomodify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="94ad1-129">Gestire AD FS</span><span class="sxs-lookup"><span data-stu-id="94ad1-129">Manage AD FS</span></span>
<span data-ttu-id="94ad1-130">È possibile eseguire varie attività AD FS correlati in Azure AD Connect, con un intervento minimo dell'utente tramite la procedura guidata di hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="94ad1-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using hello Azure AD Connect wizard.</span></span> <span data-ttu-id="94ad1-131">Dopo aver completato l'installazione di Azure AD Connect dalla procedura guidata hello in esecuzione, è possibile eseguire la procedura guidata hello nuovamente tooperform altre attività.</span><span class="sxs-lookup"><span data-stu-id="94ad1-131">After you've finished installing Azure AD Connect by running hello wizard, you can run hello wizard again tooperform additional tasks.</span></span>

## <span data-ttu-id="94ad1-132">Ripristino hello trust<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="94ad1-132">Repair hello trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="94ad1-133">È possibile utilizzare Azure AD Connect toocheck hello stato di integrità corrente di AD FS hello e trust di Azure AD e intraprendere le azioni appropriate toorepair hello trust.</span><span class="sxs-lookup"><span data-stu-id="94ad1-133">You can use Azure AD Connect toocheck hello current health of hello AD FS and Azure AD trust and take appropriate actions toorepair hello trust.</span></span> <span data-ttu-id="94ad1-134">Seguire questi passaggi toorepair di Azure Active Directory e ADFS attendibile.</span><span class="sxs-lookup"><span data-stu-id="94ad1-134">Follow these steps toorepair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="94ad1-135">Selezionare **AAD di riparazione e considerare attendibile ADFS** dall'elenco di hello di attività aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="94ad1-135">Select **Repair AAD and ADFS Trust** from hello list of additional tasks.</span></span>
   <span data-ttu-id="94ad1-136">![Ripristino del trust di AAD e AD FS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="94ad1-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="94ad1-137">In hello **connettersi AD tooAzure** pagina, fornire le credenziali di amministratore globale per Azure AD e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="94ad1-137">On hello **Connect tooAzure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="94ad1-138">![Connettersi AD tooAzure](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="94ad1-138">![Connect tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="94ad1-139">In hello **credenziali di accesso remoto** pagina, immettere le credenziali di hello hello amministratore di dominio.</span><span class="sxs-lookup"><span data-stu-id="94ad1-139">On hello **Remote access credentials** page, enter hello credentials for hello domain administrator.</span></span>

   ![Credenziali di accesso remoto](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="94ad1-141">Dopo aver fatto clic su **Avanti**, Azure AD Connect verifica l'integrità del certificato e visualizza gli eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="94ad1-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Stato dei certificati](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="94ad1-143">Hello **tooconfigure pronto** pagina Mostra hello elenco di azioni che saranno eseguite trust hello toorepair.</span><span class="sxs-lookup"><span data-stu-id="94ad1-143">hello **Ready tooconfigure** page shows hello list of actions that will be performed toorepair hello trust.</span></span>

    ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="94ad1-145">Fare clic su **installare** trust hello toorepair.</span><span class="sxs-lookup"><span data-stu-id="94ad1-145">Click **Install** toorepair hello trust.</span></span>

> [!NOTE]
> <span data-ttu-id="94ad1-146">Azure AD Connect può solo ripristinare o eseguire azioni sui certificati autofirmati.</span><span class="sxs-lookup"><span data-stu-id="94ad1-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="94ad1-147">I certificati di terze parti non possono essere ripristinati da Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="94ad1-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="94ad1-148">Attuare la federazione con Azure AD mediante AlternateID <a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="94ad1-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="94ad1-149">È consigliabile che hello Name(UPN) dell'entità utente in locale e cloud hello Nome entità utente vengono mantenute hello stesso.</span><span class="sxs-lookup"><span data-stu-id="94ad1-149">It is recommended that hello on-premises User Principal Name(UPN) and hello cloud User Principal Name are kept hello same.</span></span> <span data-ttu-id="94ad1-150">Se hello locale UPN viene utilizzato un dominio non instradabile (ad esempio,</span><span class="sxs-lookup"><span data-stu-id="94ad1-150">If hello on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="94ad1-151">Contoso. Local) o non può essere modificato a causa di dipendenze dell'applicazione toolocal, è consigliabile impostare l'ID di accesso alternativo.</span><span class="sxs-lookup"><span data-stu-id="94ad1-151">Contoso.local) or cannot be changed due toolocal application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="94ad1-152">ID di accesso alternativo consente un'esperienza di accesso in cui gli utenti possono accedere con un attributo diverso dal relativo UPN, ad esempio mail tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="94ad1-152">Alternate login ID allows you tooconfigure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="94ad1-153">scelta di Hello per nome dell'entità utente in Azure AD Connect attributo userPrincipalName toohello di valori predefiniti in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94ad1-153">hello choice for User Principal Name in Azure AD Connect defaults toohello userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="94ad1-154">Se si sceglie qualsiasi altro attributo per il nome dell'entità utente e si sta eseguendo la federazione con AD FS, Azure AD Connect configurerà AD FS per l’ID di accesso alternativo.</span><span class="sxs-lookup"><span data-stu-id="94ad1-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="94ad1-155">Di seguito è riportato un esempio della scelta di un attributo diverso per il nome dell'entità utente:</span><span class="sxs-lookup"><span data-stu-id="94ad1-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Selezione dell’attributo ID alternativo](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="94ad1-157">La configurazione dell’ID di accesso alternativo per AD FS consiste in due passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="94ad1-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="94ad1-158">**Configurare il set corretto di hello di attestazioni di rilascio**: regole attestazione di rilascio hello nel componente hello Azure AD attendibilità attributo UserPrincipalName di hello selezionato toouse modificato come hello ID alternativo dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-158">**Configure hello right set of issuance claims**: hello issuance claim rules in hello Azure AD relying party trust are modified toouse hello selected UserPrincipalName attribute as hello alternate ID of hello user.</span></span>
2. <span data-ttu-id="94ad1-159">**Abilitare l'ID di accesso alternativo nella configurazione di ADFS hello**: la configurazione di ADFS hello Active Directory viene aggiornata in modo che ADFS è possibile cercare gli utenti nelle foreste di hello appropriata utilizzando ID alternativo di hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-159">**Enable alternate login ID in hello AD FS configuration**: hello AD FS configuration is updated so that AD FS can look up users in hello appropriate forests using hello alternate ID.</span></span> <span data-ttu-id="94ad1-160">Questa configurazione è supportata per AD FS in Windows Server 2012 R2 (con KB2919355) o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="94ad1-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="94ad1-161">Se hello AD FS Server 2012 R2, Azure AD Connect Verifica presenza di hello di hello necessario KB.</span><span class="sxs-lookup"><span data-stu-id="94ad1-161">If hello AD FS servers are 2012 R2, Azure AD Connect checks for hello presence of hello required KB.</span></span> <span data-ttu-id="94ad1-162">Se hello KB non viene rilevato, un messaggio di avviso verrà visualizzato al termine della configurazione, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="94ad1-162">If hello KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Avviso per KB mancante su 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="94ad1-164">configurazione di hello toorectify in caso di KB mancante, installare hello necessario [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) e quindi ripristinare hello trust utilizzando [ripristinare AAD e Trust di AD FS](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="94ad1-164">toorectify hello configuration in case of missing KB, install hello required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair hello trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="94ad1-165">Per ulteriori informazioni su toomanually alternateID e passaggi di configurazione, leggere [la configurazione di ID di accesso alternativo](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="94ad1-165">For more information on alternateID and steps toomanually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="94ad1-166">Aggiungere un server AD FS <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="94ad1-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="94ad1-167">server AD FS tooadd, Azure AD Connect richiede un certificato PFX hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-167">tooadd an AD FS server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="94ad1-168">Pertanto, è possibile eseguire questa operazione solo se è configurato farm ADFS hello Active Directory con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="94ad1-168">Therefore, you can perform this operation only if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="94ad1-169">Selezionare **Distribuzione di un server federativo aggiuntivo** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="94ad1-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Server federativo aggiuntivo](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="94ad1-171">In hello **connettersi AD tooAzure** pagina, immettere le credenziali di amministratore globale per Azure AD e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="94ad1-171">On hello **Connect tooAzure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Connettersi AD tooAzure](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="94ad1-173">Fornire le credenziali di amministratore di dominio hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-173">Provide hello domain administrator credentials.</span></span>

   ![Credenziali dell'amministratore di dominio](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="94ad1-175">Azure AD Connect richiede password hello del file PFX hello fornito dall'utente durante la configurazione della nuova farm ADFS con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="94ad1-175">Azure AD Connect asks for hello password of hello PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="94ad1-176">Fare clic su **immettere la Password** password hello tooprovide per il file PFX hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-176">Click **Enter Password** tooprovide hello password for hello PFX file.</span></span>

   ![Password certificato](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Specificare il certificato SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="94ad1-179">In hello **server ADFS** pagina, immettere il nome di server hello o toobe di indirizzo IP aggiunto farm ADFS toohello Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94ad1-179">On hello **AD FS Servers** page, enter hello server name or IP address toobe added toohello AD FS farm.</span></span>

   ![Server AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="94ad1-181">Fare clic su **Avanti**e passare a hello finale **configura** pagina.</span><span class="sxs-lookup"><span data-stu-id="94ad1-181">Click **Next**, and go through hello final **Configure** page.</span></span> <span data-ttu-id="94ad1-182">Al termine dell'aggiunta di farm di ADFS hello server toohello AD Azure AD Connect, si avrà la connettività di hello opzione tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-182">After Azure AD Connect has finished adding hello servers toohello AD FS farm, you will be given hello option tooverify hello connectivity.</span></span>

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Installazione completata](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="94ad1-185">Aggiungere un server WAP AD FS <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="94ad1-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="94ad1-186">tooadd un server WAP, Azure AD Connect richiede un certificato PFX hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-186">tooadd a WAP server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="94ad1-187">Pertanto, è possibile eseguire questa operazione solo se è configurato farm ADFS hello Active Directory con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="94ad1-187">Therefore, you can only perform this operation if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="94ad1-188">Selezionare **distribuire Proxy applicazione Web** dall'elenco di hello delle attività disponibili.</span><span class="sxs-lookup"><span data-stu-id="94ad1-188">Select **Deploy Web Application Proxy** from hello list of available tasks.</span></span>

   ![Distribuire il Proxy applicazione Web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="94ad1-190">Fornire le credenziali di amministratore globale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-190">Provide hello Azure global administrator credentials.</span></span>

   ![Connettersi AD tooAzure](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="94ad1-192">In hello **certificato SSL specificare** pagina, fornire la password di hello per il file PFX hello fornito con la farm di hello AD FS è stato configurato con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="94ad1-192">On hello **Specify SSL certificate** page, provide hello password for hello PFX file that you provided when you configured hello AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="94ad1-193">![Password certificato](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="94ad1-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Specificare il certificato SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="94ad1-195">Aggiungere hello server toobe aggiunto come server WAP.</span><span class="sxs-lookup"><span data-stu-id="94ad1-195">Add hello server toobe added as a WAP server.</span></span> <span data-ttu-id="94ad1-196">Poiché il server WAP hello potrebbe non essere toohello aggiunti a un dominio, la procedura guidata hello richiede server toohello credenziali amministrative da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="94ad1-196">Because hello WAP server might not be joined toohello domain, hello wizard asks for administrative credentials toohello server being added.</span></span>

   ![Credenziali amministrative del server](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="94ad1-198">In hello **credenziali trust Proxy** fornire proxy hello di credenziali amministrative tooconfigure trust e accesso hello server primario nella farm ADFS hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-198">On hello **Proxy trust credentials** page, provide administrative credentials tooconfigure hello proxy trust and access hello primary server in hello AD FS farm.</span></span>

   ![Credenziali di attendibilità del proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="94ad1-200">In hello **tooconfigure pronto** pagina, la procedura guidata hello Mostra elenco hello di azioni che verranno eseguite.</span><span class="sxs-lookup"><span data-stu-id="94ad1-200">On hello **Ready tooconfigure** page, hello wizard shows hello list of actions that will be performed.</span></span>

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="94ad1-202">Fare clic su **installare** configurazione hello toofinish.</span><span class="sxs-lookup"><span data-stu-id="94ad1-202">Click **Install** toofinish hello configuration.</span></span> <span data-ttu-id="94ad1-203">Al termine della configurazione di hello, hello guidata garantisce hello tooverify opzione hello server toohello di connettività.</span><span class="sxs-lookup"><span data-stu-id="94ad1-203">After hello configuration is complete, hello wizard gives you hello option tooverify hello connectivity toohello servers.</span></span> <span data-ttu-id="94ad1-204">Fare clic su **verificare** toocheck connettività.</span><span class="sxs-lookup"><span data-stu-id="94ad1-204">Click **Verify** toocheck connectivity.</span></span>

   ![Installazione completata](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="94ad1-206">Aggiunta di un dominio federato <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="94ad1-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="94ad1-207">È facile tooadd toobe un dominio federato con Azure AD mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="94ad1-207">It's easy tooadd a domain toobe federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="94ad1-208">Azure AD Connect aggiunge hello del dominio per la federazione e modifica attestazioni hello regole toocorrectly riflettere emittente hello quando si dispone di più domini federati con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94ad1-208">Azure AD Connect adds hello domain for federation and modifies hello claim rules toocorrectly reflect hello issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="94ad1-209">tooadd un dominio federato, attività hello selezionare **aggiungere un altro dominio di Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="94ad1-209">tooadd a federated domain, select hello task **Add an additional Azure AD domain**.</span></span>

   ![Dominio di Azure AD aggiuntivo](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="94ad1-211">Nella pagina successiva di hello della procedura guidata hello, fornire le credenziali di amministratore globale di hello per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94ad1-211">On hello next page of hello wizard, provide hello global administrator credentials for Azure AD.</span></span>

   ![Connettersi AD tooAzure](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="94ad1-213">In hello **credenziali di accesso remoto** pagina, fornire le credenziali di amministratore di dominio hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-213">On hello **Remote access credentials** page, provide hello domain administrator credentials.</span></span>

   ![Credenziali di accesso remoto](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="94ad1-215">Nella pagina successiva di hello, la procedura guidata hello fornisce un elenco di domini di Azure AD che si può creare la directory locale con una federazione.</span><span class="sxs-lookup"><span data-stu-id="94ad1-215">On hello next page, hello wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="94ad1-216">Scegliere il dominio hello dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-216">Choose hello domain from hello list.</span></span>

   ![Dominio di Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="94ad1-218">Dopo aver scelto il dominio di hello, guidata hello offre le informazioni corrette su altre azioni che hello guidata verrà richiedere e hello impatto della configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-218">After you choose hello domain, hello wizard provides you with appropriate information about further actions that hello wizard will take and hello impact of hello configuration.</span></span> <span data-ttu-id="94ad1-219">In alcuni casi, se si seleziona un dominio che non è ancora verificato in Azure AD, la procedura guidata hello vengono fornite informazioni toohelp è verificare il dominio hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-219">In some cases, if you select a domain that isn't yet verified in Azure AD, hello wizard provides you with information toohelp you verify hello domain.</span></span> <span data-ttu-id="94ad1-220">Vedere [aggiungere tooAzure di nome Active Directory del dominio personalizzato](../active-directory-add-domain.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="94ad1-220">See [Add your custom domain name tooAzure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="94ad1-221">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="94ad1-221">Click **Next**.</span></span> <span data-ttu-id="94ad1-222">Hello **tooconfigure pronto** pagina Mostra elenco hello di azioni che verranno eseguite di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="94ad1-222">hello **Ready tooconfigure** page shows hello list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="94ad1-223">Fare clic su **installare** configurazione hello toofinish.</span><span class="sxs-lookup"><span data-stu-id="94ad1-223">Click **Install** toofinish hello configuration.</span></span>

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="94ad1-225">Aggiungere utenti da hello dominio federato deve essere sincronizzato prima saranno in grado di toologin tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94ad1-225">Users from hello added federated domain must be synchronized before they will be able toologin tooAzure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="94ad1-226">Personalizzazione di AD FS</span><span class="sxs-lookup"><span data-stu-id="94ad1-226">AD FS customization</span></span>
<span data-ttu-id="94ad1-227">Hello sezioni seguenti forniscono informazioni dettagliate su alcune delle attività comuni di hello che potrebbe essere tooperform quando si personalizza la pagina di accesso di ADFS.</span><span class="sxs-lookup"><span data-stu-id="94ad1-227">hello following sections provide details about some of hello common tasks that you might have tooperform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="94ad1-228">Aggiungere un'illustrazione o il logo personalizzato della società <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="94ad1-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="94ad1-229">logo di hello toochange della società hello che viene visualizzato in hello **Accedi** pagina, utilizzare i seguenti cmdlet di Windows PowerShell e la sintassi hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-229">toochange hello logo of hello company that's displayed on hello **Sign-in** page, use hello following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="94ad1-230">Hello consigliata dimensioni per il logo hello sono 260 x 35 96 DPI con dimensioni non superiori a 10 KB.</span><span class="sxs-lookup"><span data-stu-id="94ad1-230">hello recommended dimensions for hello logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="94ad1-231">Hello *TargetName* parametro è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="94ad1-231">hello *TargetName* parameter is required.</span></span> <span data-ttu-id="94ad1-232">tema predefinito Hello che viene rilasciata con AD FS è denominato Default.</span><span class="sxs-lookup"><span data-stu-id="94ad1-232">hello default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="94ad1-233">Aggiungere una descrizione di accesso <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="94ad1-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="94ad1-234">tooadd un toohello descrizione nella pagina di accesso **nella pagina di accesso**, utilizzare hello segue sintassi e i cmdlet di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94ad1-234">tooadd a sign-in page description toohello **Sign-in page**, use hello following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="94ad1-235">Modificare le regole attestazioni per AD FS <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="94ad1-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="94ad1-236">ADFS supporta un linguaggio di attestazione completo che è possibile utilizzare regole attestazione toocreate personalizzato.</span><span class="sxs-lookup"><span data-stu-id="94ad1-236">AD FS supports a rich claim language that you can use toocreate custom claim rules.</span></span> <span data-ttu-id="94ad1-237">Per ulteriori informazioni, vedere [hello ruolo del linguaggio delle regole attestazioni hello](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="94ad1-237">For more information, see [hello Role of hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="94ad1-238">Hello nelle sezioni seguenti viene illustrato come scrivere regole personalizzate per alcuni scenari correlati tooAzure Active Directory e la federazione ADFS.</span><span class="sxs-lookup"><span data-stu-id="94ad1-238">hello following sections describe how you can write custom rules for some scenarios that relate tooAzure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a><span data-ttu-id="94ad1-239">ID non modificabile condizionale su un valore presente nell'attributo hello</span><span class="sxs-lookup"><span data-stu-id="94ad1-239">Immutable ID conditional on a value being present in hello attribute</span></span>
<span data-ttu-id="94ad1-240">Azure AD Connect consente di specificare toobe un attributo utilizzato come un ancoraggio di origine quando gli oggetti sono sincronizzati tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94ad1-240">Azure AD Connect lets you specify an attribute toobe used as a source anchor when objects are synced tooAzure AD.</span></span> <span data-ttu-id="94ad1-241">Se il valore di hello nell'attributo personalizzato di hello non è vuoto, è possibile tooissue un'attestazione ID non modificabile.</span><span class="sxs-lookup"><span data-stu-id="94ad1-241">If hello value in hello custom attribute is not empty, you might want tooissue an immutable ID claim.</span></span>

<span data-ttu-id="94ad1-242">Ad esempio, è possibile selezionare **ms-ds-consistencyguid** attributo hello di ancoraggio di origine hello e problema **ImmutableID** come **ms-ds-consistencyguid** in case hello attributo ha un valore su di essa.</span><span class="sxs-lookup"><span data-stu-id="94ad1-242">For example, you might select **ms-ds-consistencyguid** as hello attribute for hello source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case hello attribute has a value against it.</span></span> <span data-ttu-id="94ad1-243">Se è presente alcun valore rispetto a attributo hello, emettere **objectGuid** come hello ID non modificabile.</span><span class="sxs-lookup"><span data-stu-id="94ad1-243">If there's no value against hello attribute, issue **objectGuid** as hello immutable ID.</span></span> <span data-ttu-id="94ad1-244">È possibile costruire il set di hello di regole attestazioni personalizzate come descritto nella seguente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-244">You can construct hello set of custom claim rules as described in hello following section.</span></span>

<span data-ttu-id="94ad1-245">**Regola 1: Attributi della query**</span><span class="sxs-lookup"><span data-stu-id="94ad1-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="94ad1-246">In questa regola, si sta eseguendo la query valori hello di **ms-ds-consistencyguid** e **objectGuid** per utente hello da Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94ad1-246">In this rule, you're querying hello values of **ms-ds-consistencyguid** and **objectGuid** for hello user from Active Directory.</span></span> <span data-ttu-id="94ad1-247">Modificare il nome hello archivio nome tooan archivio appropriato nella distribuzione di ADFS.</span><span class="sxs-lookup"><span data-stu-id="94ad1-247">Change hello store name tooan appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="94ad1-248">Inoltre modificare il tipo hello attestazioni tipo tooa attestazioni appropriate per la federazione, come definito per **objectGuid** e **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="94ad1-248">Also change hello claims type tooa proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="94ad1-249">Inoltre, tramite **aggiungere** e non **problema**, evitare di aggiungere un problema in uscita per l'entità hello e può utilizzare valori hello come valori intermedi.</span><span class="sxs-lookup"><span data-stu-id="94ad1-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for hello entity, and can use hello values as intermediate values.</span></span> <span data-ttu-id="94ad1-250">Attestazione hello in una regola successiva vengono emessi dopo aver stabilito quali toouse valore come hello ID non modificabile.</span><span class="sxs-lookup"><span data-stu-id="94ad1-250">You will issue hello claim in a later rule after you establish which value toouse as hello immutable ID.</span></span>

<span data-ttu-id="94ad1-251">**Regola 2: Verificare che ms-ds-consistencyguid esista per l'utente hello**</span><span class="sxs-lookup"><span data-stu-id="94ad1-251">**Rule 2: Check if ms-ds-consistencyguid exists for hello user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="94ad1-252">Questa regola definisce un flag temporaneo denominato **idflag** impostato troppo**useguid** se è presente alcun **ms-ds-consistencyguid** popolata per utente hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-252">This rule defines a temporary flag called **idflag** that is set too**useguid** if there's no **ms-ds-consistencyguid** populated for hello user.</span></span> <span data-ttu-id="94ad1-253">logica di Hello protetti da questo è il fatto di hello che ADFS non consentono le attestazioni vuote.</span><span class="sxs-lookup"><span data-stu-id="94ad1-253">hello logic behind this is hello fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="94ad1-254">Pertanto quando si aggiungono attestazioni http://contoso.com/ws/2016/02/identity/claims/objectguid e http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid nella regola 1, si otterrà un **msdsconsistencyguid** attestazione solo se il valore di Hello viene popolato per utente hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if hello value is populated for hello user.</span></span> <span data-ttu-id="94ad1-255">Se non è popolato, AD FS rileva che avrà un valore vuoto e lo rimuove immediatamente.</span><span class="sxs-lookup"><span data-stu-id="94ad1-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="94ad1-256">Tutti gli oggetti avranno **objectGuid**, quindi l'attestazione sarà sempre presente dopo l'esecuzione della regola 1.</span><span class="sxs-lookup"><span data-stu-id="94ad1-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="94ad1-257">**Regola 3: Rilasciare ms-ds-consistencyguid come ID non modificabile se presente**</span><span class="sxs-lookup"><span data-stu-id="94ad1-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="94ad1-258">Si tratta di un controllo **Exist** implicito.</span><span class="sxs-lookup"><span data-stu-id="94ad1-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="94ad1-259">Se il valore di hello di attestazione hello esiste, quindi rilasciare che come non modificabile hello ID.</span><span class="sxs-lookup"><span data-stu-id="94ad1-259">If hello value for hello claim exists, then issue that as hello immutable ID.</span></span> <span data-ttu-id="94ad1-260">esempio precedente Hello utilizza hello **nameidentifier** attestazione.</span><span class="sxs-lookup"><span data-stu-id="94ad1-260">hello previous example uses hello **nameidentifier** claim.</span></span> <span data-ttu-id="94ad1-261">È necessario toochange questo tipo di attestazione appropriate toohello per l'ID non modificabile hello nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="94ad1-261">You'll have toochange this toohello appropriate claim type for hello immutable ID in your environment.</span></span>

<span data-ttu-id="94ad1-262">**Regola 4: Rilasciare objectGuid come ID non modificabile se ms-ds-consistencyGuid non è presente**</span><span class="sxs-lookup"><span data-stu-id="94ad1-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="94ad1-263">In questa regola, si stia controllando semplicemente flag temporaneo hello **idflag**.</span><span class="sxs-lookup"><span data-stu-id="94ad1-263">In this rule, you're simply checking hello temporary flag **idflag**.</span></span> <span data-ttu-id="94ad1-264">È possibile decidere se tooissue hello attestazione in base al relativo valore.</span><span class="sxs-lookup"><span data-stu-id="94ad1-264">You decide whether tooissue hello claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="94ad1-265">sequenza di Hello di queste regole è importante.</span><span class="sxs-lookup"><span data-stu-id="94ad1-265">hello sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="94ad1-266">SSO con un UPN di sottodominio</span><span class="sxs-lookup"><span data-stu-id="94ad1-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="94ad1-267">È possibile aggiungere più toobe dominio federato con Azure AD Connect, come descritto in [aggiungere un nuovo dominio federato](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="94ad1-267">You can add more than one domain toobe federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="94ad1-268">Attestazione del nome principale (UPN) utente hello è necessario modificare in modo che hello ID autorità di certificazione corrisponde dominio radice toohello e non a sottodominio hello, perché il dominio federato radice hello riguarda anche figlio hello.</span><span class="sxs-lookup"><span data-stu-id="94ad1-268">You must modify hello user principal name (UPN) claim so that hello issuer ID corresponds toohello root domain and not hello subdomain, because hello federated root domain also covers hello child.</span></span>

<span data-ttu-id="94ad1-269">Per impostazione predefinita, hello regola attestazione per l'ID viene impostato come autorità di certificazione:</span><span class="sxs-lookup"><span data-stu-id="94ad1-269">By default, hello claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Attestazione predefinita per l'ID autorità di certificazione](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="94ad1-271">regola predefinita Hello semplicemente accetta suffisso UPN hello e viene utilizzato in hello attestazione dell'ID dell'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="94ad1-271">hello default rule simply takes hello UPN suffix and uses it in hello issuer ID claim.</span></span> <span data-ttu-id="94ad1-272">Ad esempio, John è un utente in sub.contoso.com e contoso.com è federato con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94ad1-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="94ad1-273">Immette John john@sub.contoso.com come hello nome utente durante la firma in tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94ad1-273">John enters john@sub.contoso.com as hello username while signing in tooAzure AD.</span></span> <span data-ttu-id="94ad1-274">regola attestazione ID Hello predefinita dell'autorità di certificazione in ADFS viene gestito da hello seguente modo:</span><span class="sxs-lookup"><span data-stu-id="94ad1-274">hello default issuer ID claim rule in AD FS handles it in hello following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="94ad1-275">**Valore dell'attestazione:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="94ad1-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="94ad1-276">toohave solo hello dominio radice dell'autorità di certificazione hello il valore dell'attestazione, modificare hello attestazione regola toomatch hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="94ad1-276">toohave only hello root domain in hello issuer claim value, change hello claim rule toomatch hello following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="94ad1-277">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94ad1-277">Next steps</span></span>
<span data-ttu-id="94ad1-278">Altre informazioni sulle [opzioni di accesso utente](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="94ad1-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
