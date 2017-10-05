---
title: Gestione e personalizzazione di Active Directory Federation Services con Azure AD Connect | Microsoft Docs
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
ms.openlocfilehash: 14f03542a6553c5bb697192828368ffe6b96441c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="3e305-104">Gestire e personalizzare Active Directory Federation Services con Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3e305-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="3e305-105">In questo articolo viene descritto come gestire e personalizzare Active Directory Federation Services (ADFS) tramite Azure Active Directory (Azure AD) Connect.</span><span class="sxs-lookup"><span data-stu-id="3e305-105">This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="3e305-106">Si includono inoltre altre attività comuni di AD FS che potrebbero essere necessarie per eseguire una configurazione completa di una farm di AD FS.</span><span class="sxs-lookup"><span data-stu-id="3e305-106">It also includes other common AD FS tasks that you might need to do for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="3e305-107">Argomento</span><span class="sxs-lookup"><span data-stu-id="3e305-107">Topic</span></span> | <span data-ttu-id="3e305-108">Contenuto</span><span class="sxs-lookup"><span data-stu-id="3e305-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="3e305-109">**Gestire AD FS**</span><span class="sxs-lookup"><span data-stu-id="3e305-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="3e305-110">Ripristinare il trust</span><span class="sxs-lookup"><span data-stu-id="3e305-110">Repair the trust</span></span>](#repairthetrust) |<span data-ttu-id="3e305-111">Come ripristinare il trust federativo con Office 365.</span><span class="sxs-lookup"><span data-stu-id="3e305-111">How to repair the federation trust with Office 365.</span></span> |
| [<span data-ttu-id="3e305-112">Attuare la federazione con Azure AD mediante l'ID di accesso alternativo </span><span class="sxs-lookup"><span data-stu-id="3e305-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="3e305-113">Configurazione della federazione usando l'ID di accesso alternativo</span><span class="sxs-lookup"><span data-stu-id="3e305-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="3e305-114">Aggiungere un server AD FS</span><span class="sxs-lookup"><span data-stu-id="3e305-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="3e305-115">Come espandere una farm AD FS con un server AD FS aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="3e305-115">How to expand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="3e305-116">Aggiungere un server proxy applicazione Web AD FS</span><span class="sxs-lookup"><span data-stu-id="3e305-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="3e305-117">Come espandere la farm AD FS con un server Proxy applicazione Web (WAP) aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="3e305-117">How to expand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="3e305-118">Aggiunta di un dominio federato</span><span class="sxs-lookup"><span data-stu-id="3e305-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="3e305-119">Come aggiungere un dominio federato.</span><span class="sxs-lookup"><span data-stu-id="3e305-119">How to add a federated domain.</span></span> |
| [<span data-ttu-id="3e305-120">Aggiornare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="3e305-120">Update the SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="3e305-121">Come aggiornare il certificato SSL per una farm AD FS.</span><span class="sxs-lookup"><span data-stu-id="3e305-121">How to update the SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="3e305-122">**Personalizzare AD FS**</span><span class="sxs-lookup"><span data-stu-id="3e305-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="3e305-123">Aggiungere un'illustrazione o il logo personalizzato della società</span><span class="sxs-lookup"><span data-stu-id="3e305-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="3e305-124">Come personalizzare la pagina di accesso ad AD FS con un'illustrazione e il logo della società.</span><span class="sxs-lookup"><span data-stu-id="3e305-124">How to customize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="3e305-125">Aggiungere una descrizione di accesso</span><span class="sxs-lookup"><span data-stu-id="3e305-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="3e305-126">Come aggiungere una descrizione della pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="3e305-126">How to add a sign-in page description.</span></span> |
| [<span data-ttu-id="3e305-127">Modificare le regole attestazioni per AD FS</span><span class="sxs-lookup"><span data-stu-id="3e305-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="3e305-128">Come modificare le attestazioni di AD FS per vari scenari di federazione.</span><span class="sxs-lookup"><span data-stu-id="3e305-128">How to modify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="3e305-129">Gestire AD FS</span><span class="sxs-lookup"><span data-stu-id="3e305-129">Manage AD FS</span></span>
<span data-ttu-id="3e305-130">È possibile eseguire diverse operazioni relative ad Azure AD Connect con la procedura guidata di Azure AD Connect con un intervento minimo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3e305-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using the Azure AD Connect wizard.</span></span> <span data-ttu-id="3e305-131">Al termine dell'installazione guidata di Azure AD Connect, è possibile eseguire nuovamente la procedura guidata per eseguire attività aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="3e305-131">After you've finished installing Azure AD Connect by running the wizard, you can run the wizard again to perform additional tasks.</span></span>

## <span data-ttu-id="3e305-132">Ripristinare il trust <a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="3e305-132">Repair the trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="3e305-133">È possibile usare Azure AD Connect per controllare lo stato corrente dell'integrità di trust di AD FS e Azure AD e intraprendere le azioni necessarie per ripristinare il trust.</span><span class="sxs-lookup"><span data-stu-id="3e305-133">You can use Azure AD Connect to check the current health of the AD FS and Azure AD trust and take appropriate actions to repair the trust.</span></span> <span data-ttu-id="3e305-134">Per ripristinare la relazione di trust tra Azure AD e AD FS, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="3e305-134">Follow these steps to repair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="3e305-135">Selezionare **Ripristino del trust di AAD e AD FS** nell'elenco delle attività aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="3e305-135">Select **Repair AAD and ADFS Trust** from the list of additional tasks.</span></span>
   <span data-ttu-id="3e305-136">![Ripristino del trust di AAD e AD FS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="3e305-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="3e305-137">Nella pagina **Connessione ad Azure AD** specificare le credenziali di amministratore globale per Azure AD e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3e305-137">On the **Connect to Azure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="3e305-138">![Connessione ad Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="3e305-138">![Connect to Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="3e305-139">Nella pagina **Credenziali di accesso remoto** specificare le credenziali dell'amministratore di dominio.</span><span class="sxs-lookup"><span data-stu-id="3e305-139">On the **Remote access credentials** page, enter the credentials for the domain administrator.</span></span>

   ![Credenziali di accesso remoto](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="3e305-141">Dopo aver fatto clic su **Avanti**, Azure AD Connect verifica l'integrità del certificato e visualizza gli eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="3e305-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Stato dei certificati](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="3e305-143">La pagina **Pronto per la configurazione** mostra l'elenco delle azioni che verranno eseguite per ripristinare il trust.</span><span class="sxs-lookup"><span data-stu-id="3e305-143">The **Ready to configure** page shows the list of actions that will be performed to repair the trust.</span></span>

    ![Pronto per la configurazione](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="3e305-145">Fare clic su **Installa** per ripristinare il trust.</span><span class="sxs-lookup"><span data-stu-id="3e305-145">Click **Install** to repair the trust.</span></span>

> [!NOTE]
> <span data-ttu-id="3e305-146">Azure AD Connect può solo ripristinare o eseguire azioni sui certificati autofirmati.</span><span class="sxs-lookup"><span data-stu-id="3e305-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="3e305-147">I certificati di terze parti non possono essere ripristinati da Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3e305-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="3e305-148">Attuare la federazione con Azure AD mediante AlternateID <a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="3e305-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="3e305-149">Il nome dell’entità utente locale e il nome dell'entità utente cloud devono essere preferibilmente uguali.</span><span class="sxs-lookup"><span data-stu-id="3e305-149">It is recommended that the on-premises User Principal Name(UPN) and the cloud User Principal Name are kept the same.</span></span> <span data-ttu-id="3e305-150">Se il nome dell’entità utente locale usa un dominio non instradabile (ad esempio</span><span class="sxs-lookup"><span data-stu-id="3e305-150">If the on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="3e305-151">Contoso.local) o non può essere modificato a causa di dipendenze dell'applicazione locale, è consigliabile configurare l'ID di accesso alternativo.</span><span class="sxs-lookup"><span data-stu-id="3e305-151">Contoso.local) or cannot be changed due to local application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="3e305-152">L’ID di accesso alternativo consente di configurare un'esperienza in cui gli utenti possono accedere con un attributo diverso dal relativo nome dell’entità locale, ad esempio mail.</span><span class="sxs-lookup"><span data-stu-id="3e305-152">Alternate login ID allows you to configure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="3e305-153">La scelta del nome dell’entità utente in Azure AD Connect ricade per impostazione predefinita sull’attributo userPrincipalName in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e305-153">The choice for User Principal Name in Azure AD Connect defaults to the userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="3e305-154">Se si sceglie qualsiasi altro attributo per il nome dell'entità utente e si sta eseguendo la federazione con AD FS, Azure AD Connect configurerà AD FS per l’ID di accesso alternativo.</span><span class="sxs-lookup"><span data-stu-id="3e305-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="3e305-155">Di seguito è riportato un esempio della scelta di un attributo diverso per il nome dell'entità utente:</span><span class="sxs-lookup"><span data-stu-id="3e305-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Selezione dell’attributo ID alternativo](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="3e305-157">La configurazione dell’ID di accesso alternativo per AD FS consiste in due passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="3e305-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="3e305-158">**Configurare il set corretto di attestazioni di rilascio**: le regole di attestazione di rilascio nel trust della relying party di Azure AD vengono modificate per usare l’attributo UserPrincipalName selezionato come ID alternativo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3e305-158">**Configure the right set of issuance claims**: The issuance claim rules in the Azure AD relying party trust are modified to use the selected UserPrincipalName attribute as the alternate ID of the user.</span></span>
2. <span data-ttu-id="3e305-159">**Abilitare l'ID di accesso alternativo nella configurazione di AD FS**: la configurazione di AD FS viene aggiornata in modo che AD FS possa cercare gli utenti delle foreste appropriate con un ID alternativo.</span><span class="sxs-lookup"><span data-stu-id="3e305-159">**Enable alternate login ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests using the alternate ID.</span></span> <span data-ttu-id="3e305-160">Questa configurazione è supportata per AD FS in Windows Server 2012 R2 (con KB2919355) o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3e305-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="3e305-161">Se i server AD FS sono 2012 R2, Azure AD Connect controlla la presenza della KB richiesta.</span><span class="sxs-lookup"><span data-stu-id="3e305-161">If the AD FS servers are 2012 R2, Azure AD Connect checks for the presence of the required KB.</span></span> <span data-ttu-id="3e305-162">Se la Knowledge Base non viene rilevata, un avviso verrà visualizzato al termine della configurazione, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3e305-162">If the KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Avviso per KB mancante su 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="3e305-164">Per risolvere la configurazione in caso di KB mancante, installare la [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) richiesta e quindi ripristinare il trust usando [Ripristino del trust AAD e AD FS](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="3e305-164">To rectify the configuration in case of missing KB, install the required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair the trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="3e305-165">Per altre informazioni su alternateID e i passaggi per eseguire la configurazione manuale, leggere [Configurazione di ID di accesso alternativo](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id).</span><span class="sxs-lookup"><span data-stu-id="3e305-165">For more information on alternateID and steps to manually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="3e305-166">Aggiungere un server AD FS <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="3e305-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="3e305-167">Per aggiungere un server AD FS, Azure AD Connect richiede il file PFX del certificato.</span><span class="sxs-lookup"><span data-stu-id="3e305-167">To add an AD FS server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="3e305-168">È quindi possibile eseguire questa operazione solo se la farm AD FS è stata configurata con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3e305-168">Therefore, you can perform this operation only if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="3e305-169">Selezionare **Distribuzione di un server federativo aggiuntivo** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3e305-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Server federativo aggiuntivo](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="3e305-171">Nella pagina **Connessione ad Azure AD** specificare le credenziali di amministratore globale per Azure AD e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3e305-171">On the **Connect to Azure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Connettersi ad Azure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="3e305-173">Specificare le credenziali di amministratore di dominio.</span><span class="sxs-lookup"><span data-stu-id="3e305-173">Provide the domain administrator credentials.</span></span>

   ![Credenziali dell'amministratore di dominio](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="3e305-175">Azure AD Connect chiederà la password del file PFX specificato durante la configurazione della nuova farm AD FS con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3e305-175">Azure AD Connect asks for the password of the PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="3e305-176">Fare clic su **Immettere la password** per specificare la password del file PFX.</span><span class="sxs-lookup"><span data-stu-id="3e305-176">Click **Enter Password** to provide the password for the PFX file.</span></span>

   ![Password certificato](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Specificare il certificato SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="3e305-179">Nella pagina **Server ADFS** immettere il nome del server o l'indirizzo IP da aggiungere alla farm ADFS.</span><span class="sxs-lookup"><span data-stu-id="3e305-179">On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.</span></span>

   ![Server AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="3e305-181">Fare clic su **Avanti** e procedere fino alla pagina **Configura** finale.</span><span class="sxs-lookup"><span data-stu-id="3e305-181">Click **Next**, and go through the final **Configure** page.</span></span> <span data-ttu-id="3e305-182">Quando Azure AD Connect avrà completato l'aggiunta dei server alla farm AD FS, si potrà verificare la connettività.</span><span class="sxs-lookup"><span data-stu-id="3e305-182">After Azure AD Connect has finished adding the servers to the AD FS farm, you will be given the option to verify the connectivity.</span></span>

   ![Pronto per la configurazione](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Installazione completata](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="3e305-185">Aggiungere un server WAP AD FS <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="3e305-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="3e305-186">Per aggiungere un server WAP, Azure AD Connect richiede il file PFX del certificato.</span><span class="sxs-lookup"><span data-stu-id="3e305-186">To add a WAP server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="3e305-187">È quindi possibile eseguire questa operazione solo se la farm AD FS è stata configurata con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3e305-187">Therefore, you can only perform this operation if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="3e305-188">Selezionare **Distribuisci il proxy applicazione Web (nessuno attualmente configurato)** nell'elenco delle attività disponibili.</span><span class="sxs-lookup"><span data-stu-id="3e305-188">Select **Deploy Web Application Proxy** from the list of available tasks.</span></span>

   ![Distribuire il Proxy applicazione Web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="3e305-190">Specificare le credenziali di amministratore globale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3e305-190">Provide the Azure global administrator credentials.</span></span>

   ![Connettersi ad Azure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="3e305-192">Nella pagina **Specificare il certificato SSL** indicare la password per il file PFX specificato durante la configurazione della farm AD FS con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3e305-192">On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="3e305-193">![Password certificato](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="3e305-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Specificare il certificato SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="3e305-195">Aggiungere il server da usare come server WAP.</span><span class="sxs-lookup"><span data-stu-id="3e305-195">Add the server to be added as a WAP server.</span></span> <span data-ttu-id="3e305-196">Dato che il server WAP potrebbe anche non essere aggiunto al dominio, la procedura guidata richiede le credenziali amministrative da aggiungere per il server.</span><span class="sxs-lookup"><span data-stu-id="3e305-196">Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.</span></span>

   ![Credenziali amministrative del server](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="3e305-198">Nella pagina **Credenziali attendibilità proxy** specificare le credenziali amministrative per configurare l'attendibilità del proxy e accedere al server primario nella farm AD FS.</span><span class="sxs-lookup"><span data-stu-id="3e305-198">On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.</span></span>

   ![Credenziali di attendibilità del proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="3e305-200">La pagina **Pronto per la configurazione** della procedura guidata mostra l'elenco delle azioni che verranno eseguite.</span><span class="sxs-lookup"><span data-stu-id="3e305-200">On the **Ready to configure** page, the wizard shows the list of actions that will be performed.</span></span>

   ![Pronto per la configurazione](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="3e305-202">Fare clic su **Installa** per completare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="3e305-202">Click **Install** to finish the configuration.</span></span> <span data-ttu-id="3e305-203">Al termine della configurazione, la procedura guidata offre la possibilità di verificare la connettività ai server.</span><span class="sxs-lookup"><span data-stu-id="3e305-203">After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers.</span></span> <span data-ttu-id="3e305-204">Fare clic su **Verifica** per controllare la connettività.</span><span class="sxs-lookup"><span data-stu-id="3e305-204">Click **Verify** to check connectivity.</span></span>

   ![Installazione completata](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="3e305-206">Aggiunta di un dominio federato <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="3e305-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="3e305-207">Con Azure AD Connect è facile aggiungere un dominio per la federazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e305-207">It's easy to add a domain to be federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="3e305-208">Azure AD Connect aggiunge il dominio per la federazione e modifica le regole attestazioni per riflettere correttamente l'autorità di certificazione quando sono presenti più domini federati con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e305-208">Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="3e305-209">Per aggiungere un dominio federato, selezionare l'attività **Aggiunta di un altro dominio di Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="3e305-209">To add a federated domain, select the task **Add an additional Azure AD domain**.</span></span>

   ![Dominio di Azure AD aggiuntivo](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="3e305-211">Nella pagina successiva della procedura guidata specificare le credenziali di amministratore globale per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e305-211">On the next page of the wizard, provide the global administrator credentials for Azure AD.</span></span>

   ![Connessione ad Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="3e305-213">Nella pagina **Credenziali di accesso remoto** specificare le credenziali di amministratore di dominio.</span><span class="sxs-lookup"><span data-stu-id="3e305-213">On the **Remote access credentials** page, provide the domain administrator credentials.</span></span>

   ![Credenziali di accesso remoto](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="3e305-215">Nella pagina successiva la procedura guidata mostra un elenco di domini di Azure AD con cui è possibile attuare la federazione della directory locale.</span><span class="sxs-lookup"><span data-stu-id="3e305-215">On the next page, the wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="3e305-216">Scegliere il dominio dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="3e305-216">Choose the domain from the list.</span></span>

   ![Dominio di Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="3e305-218">Dopo aver scelto il dominio, la procedura guidata offre informazioni appropriate sulle altre azioni che verranno eseguite e sull'impatto della configurazione.</span><span class="sxs-lookup"><span data-stu-id="3e305-218">After you choose the domain, the wizard provides you with appropriate information about further actions that the wizard will take and the impact of the configuration.</span></span> <span data-ttu-id="3e305-219">In alcuni casi, se si seleziona un dominio non ancora verificato in Azure AD, la procedura guidata offre informazioni che consentono di verificare il dominio.</span><span class="sxs-lookup"><span data-stu-id="3e305-219">In some cases, if you select a domain that isn't yet verified in Azure AD, the wizard provides you with information to help you verify the domain.</span></span> <span data-ttu-id="3e305-220">Per altre informazioni, vedere [Aggiungere un nome di dominio personalizzato ad Azure Active Directory](../active-directory-add-domain.md) .</span><span class="sxs-lookup"><span data-stu-id="3e305-220">See [Add your custom domain name to Azure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="3e305-221">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3e305-221">Click **Next**.</span></span> <span data-ttu-id="3e305-222">Nella pagina **Pronto per la configurazione** viene visualizzato l'elenco delle azioni che verranno eseguite da Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3e305-222">The **Ready to configure** page shows the list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="3e305-223">Fare clic su **Installa** per completare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="3e305-223">Click **Install** to finish the configuration.</span></span>

   ![Pronto per la configurazione](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="3e305-225">Prima che possano accedere ad Azure AD, gli utenti del dominio federato aggiunto devono essere sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="3e305-225">Users from the added federated domain must be synchronized before they will be able to login to Azure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="3e305-226">Personalizzazione di AD FS</span><span class="sxs-lookup"><span data-stu-id="3e305-226">AD FS customization</span></span>
<span data-ttu-id="3e305-227">Le sezioni seguenti offrono informazioni dettagliate su alcune attività comuni che potrebbe essere necessario eseguire durante la configurazione della pagina di accesso ad AD FS.</span><span class="sxs-lookup"><span data-stu-id="3e305-227">The following sections provide details about some of the common tasks that you might have to perform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="3e305-228">Aggiungere un'illustrazione o il logo personalizzato della società <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="3e305-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="3e305-229">Per modificare il logo della società visualizzato nella pagina **Accesso** , usare la sintassi e il cmdlet di Windows PowerShell seguenti.</span><span class="sxs-lookup"><span data-stu-id="3e305-229">To change the logo of the company that's displayed on the **Sign-in** page, use the following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="3e305-230">Le dimensioni consigliate per il logo sono 260 x 35 a 96 DPI, con dimensioni del file non maggiori di 10 KB.</span><span class="sxs-lookup"><span data-stu-id="3e305-230">The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="3e305-231">Il parametro *TargetName* è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="3e305-231">The *TargetName* parameter is required.</span></span> <span data-ttu-id="3e305-232">Il tema predefinito incluso in AD FS è denominato Predefinito.</span><span class="sxs-lookup"><span data-stu-id="3e305-232">The default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="3e305-233">Aggiungere una descrizione di accesso <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="3e305-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="3e305-234">Per aggiungere una descrizione alla **Pagina di accesso**stessa, usare la sintassi e il cmdlet di Windows PowerShell seguenti.</span><span class="sxs-lookup"><span data-stu-id="3e305-234">To add a sign-in page description to the **Sign-in page**, use the following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="3e305-235">Modificare le regole attestazioni per AD FS <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="3e305-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="3e305-236">AD FS supporta un linguaggio di attestazione avanzato che può essere usato per creare regole attestazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="3e305-236">AD FS supports a rich claim language that you can use to create custom claim rules.</span></span> <span data-ttu-id="3e305-237">Per altre informazioni, vedere [Ruolo del linguaggio delle regole attestazioni](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e305-237">For more information, see [The Role of the Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="3e305-238">Le sezioni seguenti descrivono come scrivere regole personalizzate per alcuni scenari relativi alla federazione di AD FS e Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e305-238">The following sections describe how you can write custom rules for some scenarios that relate to Azure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-the-attribute"></a><span data-ttu-id="3e305-239">ID non modificabile in base alla presenza di un valore nell'attributo</span><span class="sxs-lookup"><span data-stu-id="3e305-239">Immutable ID conditional on a value being present in the attribute</span></span>
<span data-ttu-id="3e305-240">Azure AD Connect consente di specificare un attributo da usare come ancoraggio di origine durante la sincronizzazione degli oggetti con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e305-240">Azure AD Connect lets you specify an attribute to be used as a source anchor when objects are synced to Azure AD.</span></span> <span data-ttu-id="3e305-241">Se il valore dell'attributo personalizzato non è vuoto, è consigliabile rilasciare un'attestazione con ID non modificabile.</span><span class="sxs-lookup"><span data-stu-id="3e305-241">If the value in the custom attribute is not empty, you might want to issue an immutable ID claim.</span></span>

<span data-ttu-id="3e305-242">Ad esempio, è possibile selezionare **ms-ds-consistencyguid** come attributo per l'ancoraggio di origine e rilasciare **ImmutableID** come **ms-ds-consistencyguid** nel caso in cui il valore dell'attributo non sia vuoto.</span><span class="sxs-lookup"><span data-stu-id="3e305-242">For example, you might select **ms-ds-consistencyguid** as the attribute for the source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case the attribute has a value against it.</span></span> <span data-ttu-id="3e305-243">Se non esiste un valore a fronte dell'attributo, rilasciare **objectGuid** come ID non modificabile.</span><span class="sxs-lookup"><span data-stu-id="3e305-243">If there's no value against the attribute, issue **objectGuid** as the immutable ID.</span></span> <span data-ttu-id="3e305-244">È possibile costruire il set di regole attestazioni personalizzate come descritto nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="3e305-244">You can construct the set of custom claim rules as described in the following section.</span></span>

<span data-ttu-id="3e305-245">**Regola 1: Attributi della query**</span><span class="sxs-lookup"><span data-stu-id="3e305-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="3e305-246">In questa regola si esegue una query da Active Directory sui valori di **ms-ds-consistencyguid** e **objectGuid** per l'utente.</span><span class="sxs-lookup"><span data-stu-id="3e305-246">In this rule, you're querying the values of **ms-ds-consistencyguid** and **objectGuid** for the user from Active Directory.</span></span> <span data-ttu-id="3e305-247">Modificare il nome dell'archivio con un nome di archivio appropriato nella distribuzione di AD FS.</span><span class="sxs-lookup"><span data-stu-id="3e305-247">Change the store name to an appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="3e305-248">Sostituire anche il tipo di attestazioni con il tipo appropriato per la federazione, come definito per **objectGuid** e **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="3e305-248">Also change the claims type to a proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="3e305-249">Inoltre, se si usa **add** invece di **issue**, si evita di aggiungere un rilascio in uscita per l'entità ed è possibile usare i valori come valori intermedi.</span><span class="sxs-lookup"><span data-stu-id="3e305-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values.</span></span> <span data-ttu-id="3e305-250">L'attestazione verrà rilasciata in una regola successiva, dopo aver stabilito il valore usare come ID non modificabile.</span><span class="sxs-lookup"><span data-stu-id="3e305-250">You will issue the claim in a later rule after you establish which value to use as the immutable ID.</span></span>

<span data-ttu-id="3e305-251">**Regola 2: Verificare la presenza di ms-ds-consistencyguid per l'utente**</span><span class="sxs-lookup"><span data-stu-id="3e305-251">**Rule 2: Check if ms-ds-consistencyguid exists for the user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="3e305-252">Questa regola definisce un flag temporaneo denominato **idflag**, che è impostato su **useguid** se non è presente un **ms-ds-concistencyguid** popolato per l'utente.</span><span class="sxs-lookup"><span data-stu-id="3e305-252">This rule defines a temporary flag called **idflag** that is set to **useguid** if there's no **ms-ds-consistencyguid** populated for the user.</span></span> <span data-ttu-id="3e305-253">Questo perché secondo la logica di AD FS non sono ammesse attestazioni vuote.</span><span class="sxs-lookup"><span data-stu-id="3e305-253">The logic behind this is the fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="3e305-254">Pertanto quando si aggiungono le attestazioni http://contoso.com/ws/2016/02/identity/claims/objectguid e http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid nella regola 1, si ottiene un'attestazione **msdsconsistencyguid** solo se il valore viene popolato per l'utente.</span><span class="sxs-lookup"><span data-stu-id="3e305-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if the value is populated for the user.</span></span> <span data-ttu-id="3e305-255">Se non è popolato, AD FS rileva che avrà un valore vuoto e lo rimuove immediatamente.</span><span class="sxs-lookup"><span data-stu-id="3e305-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="3e305-256">Tutti gli oggetti avranno **objectGuid**, quindi l'attestazione sarà sempre presente dopo l'esecuzione della regola 1.</span><span class="sxs-lookup"><span data-stu-id="3e305-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="3e305-257">**Regola 3: Rilasciare ms-ds-consistencyguid come ID non modificabile se presente**</span><span class="sxs-lookup"><span data-stu-id="3e305-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="3e305-258">Si tratta di un controllo **Exist** implicito.</span><span class="sxs-lookup"><span data-stu-id="3e305-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="3e305-259">Se il valore per l'attestazione esiste, viene emesso come ID non modificabile.</span><span class="sxs-lookup"><span data-stu-id="3e305-259">If the value for the claim exists, then issue that as the immutable ID.</span></span> <span data-ttu-id="3e305-260">Nell'esempio precedente si usa l'attestazione **nameidentifier** .</span><span class="sxs-lookup"><span data-stu-id="3e305-260">The previous example uses the **nameidentifier** claim.</span></span> <span data-ttu-id="3e305-261">Sarà necessario sostituirla con il tipo di attestazione appropriato per l'ID non modificabile nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="3e305-261">You'll have to change this to the appropriate claim type for the immutable ID in your environment.</span></span>

<span data-ttu-id="3e305-262">**Regola 4: Rilasciare objectGuid come ID non modificabile se ms-ds-consistencyGuid non è presente**</span><span class="sxs-lookup"><span data-stu-id="3e305-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="3e305-263">In questa regola si verifica semplicemente il flag temporaneo **idflag**.</span><span class="sxs-lookup"><span data-stu-id="3e305-263">In this rule, you're simply checking the temporary flag **idflag**.</span></span> <span data-ttu-id="3e305-264">Decidere se rilasciare l'attestazione in base al relativo valore.</span><span class="sxs-lookup"><span data-stu-id="3e305-264">You decide whether to issue the claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="3e305-265">La sequenza delle regole è importante.</span><span class="sxs-lookup"><span data-stu-id="3e305-265">The sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="3e305-266">SSO con un UPN di sottodominio</span><span class="sxs-lookup"><span data-stu-id="3e305-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="3e305-267">È possibile aggiungere più domini per la federazione usando Azure AD Connect, come descritto in [Aggiungere un nuovo dominio federato](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="3e305-267">You can add more than one domain to be federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="3e305-268">È necessario modificare l'attestazione basata sul nome dell'entità utente (UPN), in modo che l'ID autorità emittente corrisponda al dominio radice e non al sottodominio, perché il dominio radice federato include anche il dominio figlio.</span><span class="sxs-lookup"><span data-stu-id="3e305-268">You must modify the user principal name (UPN) claim so that the issuer ID corresponds to the root domain and not the subdomain, because the federated root domain also covers the child.</span></span>

<span data-ttu-id="3e305-269">Per impostazione predefinita, la regola attestazioni per l'ID autorità di certificazione è impostata come:</span><span class="sxs-lookup"><span data-stu-id="3e305-269">By default, the claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Attestazione predefinita per l'ID autorità di certificazione](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="3e305-271">La regola predefinita usa semplicemente il suffisso UPN nell'attestazione per l'ID autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="3e305-271">The default rule simply takes the UPN suffix and uses it in the issuer ID claim.</span></span> <span data-ttu-id="3e305-272">Ad esempio, John è un utente in sub.contoso.com e contoso.com è federato con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e305-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="3e305-273">John immette john@sub.contoso.com come nome utente per accedere ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e305-273">John enters john@sub.contoso.com as the username while signing in to Azure AD.</span></span> <span data-ttu-id="3e305-274">La regola di attestazione ID autorità emittente predefinita in AD FS gestisce nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="3e305-274">The default issuer ID claim rule in AD FS handles it in the following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="3e305-275">**Valore dell'attestazione:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="3e305-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="3e305-276">Perché il valore attestazione dell'autorità emittente contenga solo il dominio radice, modificare la regola attestazioni in modo che corrisponda a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="3e305-276">To have only the root domain in the issuer claim value, change the claim rule to match the following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="3e305-277">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e305-277">Next steps</span></span>
<span data-ttu-id="3e305-278">Altre informazioni sulle [opzioni di accesso utente](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="3e305-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
