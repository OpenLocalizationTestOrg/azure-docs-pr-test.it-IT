---
title: dispositivi aggiunti a un aaaHow tooconfigure ibrida Azure Active Directory | Documenti Microsoft
description: "Informazioni su modalità ibrida tooconfigure Azure Active Directory unite in join i dispositivi."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: f97ea436eca2833d8a9843acd19e5c633bc0fc07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-hybrid-azure-active-directory-joined-devices"></a><span data-ttu-id="3dbed-103">Modalità ibrida tooconfigure Azure Active Directory unite in join i dispositivi</span><span class="sxs-lookup"><span data-stu-id="3dbed-103">How tooconfigure hybrid Azure Active Directory joined devices</span></span>

<span data-ttu-id="3dbed-104">Tramite la gestione dei dispositivi in Azure Active Directory (Azure AD) è possibile garantire che gli utenti accedano alle risorse da dispositivi che soddisfano gli standard di sicurezza e conformità.</span><span class="sxs-lookup"><span data-stu-id="3dbed-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> <span data-ttu-id="3dbed-105">Per ulteriori informazioni, vedere [gestione toodevice introduzione in Azure Active Directory](device-management-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3dbed-105">For more details, see [Introduction toodevice management in Azure Active Directory](device-management-introduction.md).</span></span>

<span data-ttu-id="3dbed-106">Se si dispone di un ambiente Active Directory locale e si desidera toojoin il tooAzure dispositivi appartenenti a un dominio Active Directory, è possibile eseguire tramite la configurazione di dispositivi AD Azure unita in join ibrido.</span><span class="sxs-lookup"><span data-stu-id="3dbed-106">If you have an on-premises Active Directory environment and you want toojoin your domain-joined devices tooAzure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span></span> <span data-ttu-id="3dbed-107">Hello argomento vengono fornite hello relativi passaggi.</span><span class="sxs-lookup"><span data-stu-id="3dbed-107">hello topic provides you with hello related steps.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="3dbed-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3dbed-108">Before you begin</span></span>

<span data-ttu-id="3dbed-109">Prima di iniziare la configurazione ibrida di Azure AD i dispositivi appartenenti nell'ambiente in uso, è consigliabile acquisire familiarità con i vincoli di hello e scenari di hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="3dbed-109">Before you start configuring hybrid Azure AD joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="3dbed-110">migliorare la leggibilità hello tooimprove delle descrizioni di hello, in questo argomento utilizza hello seguenti termini:</span><span class="sxs-lookup"><span data-stu-id="3dbed-110">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="3dbed-111">**Dispositivi di Windows correnti** -questo termine si riferisce unita toodomain dispositivi che eseguono Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="3dbed-111">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="3dbed-112">**Dispositivi di livello inferiore Windows** -questo termine si riferisce tooall **supportati** dispositivi Windows aggiunti a un dominio che non sono in esecuzione Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="3dbed-112">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="3dbed-113">Dispositivi Windows correnti</span><span class="sxs-lookup"><span data-stu-id="3dbed-113">Windows current devices</span></span>

- <span data-ttu-id="3dbed-114">Per i dispositivi che eseguono il sistema operativo desktop di hello Windows, è consigliabile utilizzare aggiornamento Aniversary di Windows 10 (versione 1607) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="3dbed-114">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="3dbed-115">registrazione di dispositivi corrente di Windows Hello **è** supportato in ambienti non federati, ad esempio configurazioni di sincronizzazione di hash di password.</span><span class="sxs-lookup"><span data-stu-id="3dbed-115">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="3dbed-116">Dispositivi Windows di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="3dbed-116">Windows down-level devices</span></span>

- <span data-ttu-id="3dbed-117">è supportato i seguenti dispositivi di livello inferiore di Windows Hello:</span><span class="sxs-lookup"><span data-stu-id="3dbed-117">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="3dbed-118">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="3dbed-118">Windows 8.1</span></span>
    - <span data-ttu-id="3dbed-119">Windows 7</span><span class="sxs-lookup"><span data-stu-id="3dbed-119">Windows 7</span></span>
    - <span data-ttu-id="3dbed-120">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3dbed-120">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="3dbed-121">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3dbed-121">Windows Server 2012</span></span>
    - <span data-ttu-id="3dbed-122">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="3dbed-122">Windows Server 2008 R2</span></span>
- <span data-ttu-id="3dbed-123">registrazione dei dispositivi legacy di Windows Hello **è** supportato in ambienti non federato tramite l'accesso Single Sign On [Azure Active Directory trasparente Single Sign-On](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="3dbed-123">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="3dbed-124">registrazione dei dispositivi legacy di Windows Hello **non** supportati per i dispositivi con i profili.</span><span class="sxs-lookup"><span data-stu-id="3dbed-124">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="3dbed-125">In caso di roaming delle impostazioni o dei profili, usare Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3dbed-125">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="3dbed-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3dbed-126">Prerequisites</span></span>

<span data-ttu-id="3dbed-127">Prima di iniziare l'attivazione ibrida Azure AD aggiunti nei dispositivi dell'organizzazione, è necessario assicurarsi che si esegue una versione aggiornata di Azure AD toomake connettersi.</span><span class="sxs-lookup"><span data-stu-id="3dbed-127">Before you start enabling hybrid Azure AD joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="3dbed-128">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="3dbed-128">Azure AD Connect:</span></span>

- <span data-ttu-id="3dbed-129">Consente di mantenere associazione hello tra account di computer hello in locale di Active Directory (AD) e oggetto dispositivo hello in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dbed-129">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="3dbed-130">Abilita altre funzionalità correlate al dispositivo come Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="3dbed-130">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="3dbed-131">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="3dbed-131">Configuration steps</span></span>

<span data-ttu-id="3dbed-132">È possibile configurare dispositivi aggiunti all'identità ibrida di Azure AD per diversi tipi di piattaforme di dispositivi Windows.</span><span class="sxs-lookup"><span data-stu-id="3dbed-132">You can configure hybrid Azure AD joined devices for various types of Windows device platforms.</span></span> <span data-ttu-id="3dbed-133">In questo argomento include i passaggi di hello necessarie per tutti gli scenari di configurazione tipica.</span><span class="sxs-lookup"><span data-stu-id="3dbed-133">This topic includes hello required steps for all typical configuration scenarios.</span></span>  

<span data-ttu-id="3dbed-134">Utilizzare hello tabella tooget una panoramica dei passaggi di hello necessari per lo scenario seguente:</span><span class="sxs-lookup"><span data-stu-id="3dbed-134">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="3dbed-135">Passi</span><span class="sxs-lookup"><span data-stu-id="3dbed-135">Steps</span></span>                                      | <span data-ttu-id="3dbed-136">Dispositivi Windows correnti e sincronizzazione dell'hash delle password</span><span class="sxs-lookup"><span data-stu-id="3dbed-136">Windows current and password hash sync</span></span> | <span data-ttu-id="3dbed-137">Dispositivi Windows correnti e federazione</span><span class="sxs-lookup"><span data-stu-id="3dbed-137">Windows current and federation</span></span> | <span data-ttu-id="3dbed-138">Dispositivi Windows di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="3dbed-138">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="3dbed-139">Passaggio 1: Configurare il punto di connessione del servizio</span><span class="sxs-lookup"><span data-stu-id="3dbed-139">Step 1: Configure service connection point</span></span> | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |
| <span data-ttu-id="3dbed-143">Passaggio 2: Configurare il rilascio delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="3dbed-143">Step 2: Setup issuance of claims</span></span>           |                                        | ![Controllo][1]                    | ![Controllo][1]        |
| <span data-ttu-id="3dbed-146">Passaggio 3: Abilitare dispositivi non Windows 10</span><span class="sxs-lookup"><span data-stu-id="3dbed-146">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Controllo][1]        |
| <span data-ttu-id="3dbed-148">Passaggio 4: Controllare la distribuzione e l'implementazione</span><span class="sxs-lookup"><span data-stu-id="3dbed-148">Step 4: Control deployment and rollout</span></span>     | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |
| <span data-ttu-id="3dbed-152">Passaggio 5: Verificare i dispositivi aggiunti</span><span class="sxs-lookup"><span data-stu-id="3dbed-152">Step 5: Verify joined devices</span></span>          | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="3dbed-156">Passaggio 1: Configurare il punto di connessione del servizio</span><span class="sxs-lookup"><span data-stu-id="3dbed-156">Step 1: Configure service connection point</span></span>

<span data-ttu-id="3dbed-157">oggetto di Hello service connection point (SCP) viene utilizzato dai dispositivi durante la registrazione di hello toodiscover informazioni sul tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dbed-157">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="3dbed-158">In locale Active Directory (AD), l'oggetto di hello SCP per i dispositivi di Azure AD unita in join ibrido hello deve esistere nella partizione denominazione contesto hello configurazione di foresta hello del computer.</span><span class="sxs-lookup"><span data-stu-id="3dbed-158">In your on-premises Active Directory (AD), hello SCP object for hello hybrid Azure AD joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="3dbed-159">Esiste un solo contesto dei nomi di configurazione per foresta.</span><span class="sxs-lookup"><span data-stu-id="3dbed-159">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="3dbed-160">In una configurazione di Active Directory a più foreste, punto di connessione del servizio hello deve esistere in tutte le foreste contenente i computer appartenenti a un dominio.</span><span class="sxs-lookup"><span data-stu-id="3dbed-160">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="3dbed-161">È possibile utilizzare hello [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello contesto dei nomi configurazione della foresta.</span><span class="sxs-lookup"><span data-stu-id="3dbed-161">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="3dbed-162">Per una foresta con nome di dominio Active Directory hello *fabrikam.com*, contesto dei nomi di configurazione hello è:</span><span class="sxs-lookup"><span data-stu-id="3dbed-162">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="3dbed-163">In una foresta, l'oggetto hello SCP per hello la registrazione automatica dei dispositivi appartenenti a un dominio si trova in:</span><span class="sxs-lookup"><span data-stu-id="3dbed-163">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="3dbed-164">A seconda di come è stato distribuito Azure AD Connect, oggetto SCP hello potrebbe sono già stata configurata.</span><span class="sxs-lookup"><span data-stu-id="3dbed-164">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="3dbed-165">È possibile verificare l'esistenza di hello dell'oggetto hello e recuperare i valori di individuazione di hello mediante hello lo script di Windows PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="3dbed-165">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="3dbed-166">Hello **$scp. Parole chiave** output mostra le informazioni sul tenant hello Azure AD, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3dbed-166">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="3dbed-167">Se il punto di connessione servizio hello non esiste, è possibile creare eseguendo hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet nel server di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3dbed-167">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="3dbed-168">Credenziali di amministratore dell'organizzazione è necessario toorun questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3dbed-168">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="3dbed-169">cmdlet di Hello:</span><span class="sxs-lookup"><span data-stu-id="3dbed-169">hello cmdlet:</span></span>

- <span data-ttu-id="3dbed-170">Crea punto di connessione del servizio hello in Azure AD Connect è connesso alla foresta di Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="3dbed-170">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="3dbed-171">È necessario hello toospecify `AdConnectorAccount` parametro.</span><span class="sxs-lookup"><span data-stu-id="3dbed-171">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="3dbed-172">Si tratta di account hello è configurato come account connettore di Azure AD connect di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3dbed-172">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="3dbed-173">Hello script riportato di seguito viene illustrato un esempio per l'utilizzo di cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="3dbed-173">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="3dbed-174">In questo script `$aadAdminCred = Get-Credential` richiede tootype un nome utente.</span><span class="sxs-lookup"><span data-stu-id="3dbed-174">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="3dbed-175">È necessario tooprovide hello utente nome nel formato di hello user principal name (UPN) (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="3dbed-175">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="3dbed-176">Hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3dbed-176">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="3dbed-177">Usa il modulo Active Directory PowerShell hello, che si basa su servizi Web Active Directory in esecuzione in un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="3dbed-177">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="3dbed-178">Il servizio Servizi Web Active Directory è supportato nei controller di dominio che eseguono Windows Server 2008 R2 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3dbed-178">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="3dbed-179">È supportato solo da hello **MSOnline PowerShell versione del modulo 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-179">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="3dbed-180">toodownload questo modulo, utilizzare questo [collegamento](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="3dbed-180">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="3dbed-181">Per i controller di dominio che eseguono Windows Server 2008 o versioni precedenti, utilizzare script hello seguente punto di connessione del servizio toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3dbed-181">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="3dbed-182">In una configurazione a più foreste, è consigliabile utilizzare hello script toocreate hello servizio punto di connessione in ogni foresta in cui sono presenti computer seguenti:</span><span class="sxs-lookup"><span data-stu-id="3dbed-182">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="3dbed-183">Passaggio 2: Configurare il rilascio delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="3dbed-183">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="3dbed-184">Di Azure federato configurazione di Active Directory, i dispositivi si basano su Active Directory Federation Services (ADFS) o un'entità 3 federation service tooauthenticate tooAzure AD in locale.</span><span class="sxs-lookup"><span data-stu-id="3dbed-184">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="3dbed-185">I dispositivi si autenticano tooget un tooregister del token di accesso su hello Azure Active Directory Device Registration Service (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="3dbed-185">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="3dbed-186">Dispositivi correnti l'autenticazione tramite autenticazione integrata di Windows tooan active endpoint WS-Trust (versione 1.3 o 2005) ospitato nel servizio federativo di hello locale di Windows.</span><span class="sxs-lookup"><span data-stu-id="3dbed-186">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="3dbed-187">Quando si usa AD FS, è necessario abilitare **adfs/services/trust/13/windowstransport** o **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-187">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="3dbed-188">Se si utilizza il Proxy di autenticazione Web hello, assicurarsi anche che questo endpoint verrà pubblicato tramite proxy hello.</span><span class="sxs-lookup"><span data-stu-id="3dbed-188">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="3dbed-189">È possibile vedere quali gli endpoint sono abilitati tramite la console di gestione AD FS hello in **servizio > endpoint**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-189">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="3dbed-190">Se non si dispone di AD FS come il servizio federativo locale, istruzioni hello di toomake del fornitore che supportano WS-Trust 1.3 o gli endpoint 2005 e che questi sono pubblicati tramite hello file di scambio di metadati (MEX).</span><span class="sxs-lookup"><span data-stu-id="3dbed-190">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="3dbed-191">Hello attestazioni riportate di seguito devono essere presente nel token hello ricevuti dal servizio di Azure DRS per toocomplete registrazione dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3dbed-191">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="3dbed-192">Azure DRS creerà un oggetto dispositivo in Azure AD con alcune di queste informazioni che viene quindi utilizzate dall'oggetto dispositivo di Azure AD Connect tooassociate hello appena creato con hello computer account locale.</span><span class="sxs-lookup"><span data-stu-id="3dbed-192">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="3dbed-193">Se si dispone di più di un nome di dominio verificato, è necessario hello tooprovide attestazioni per i computer seguenti:</span><span class="sxs-lookup"><span data-stu-id="3dbed-193">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="3dbed-194">Se già si emette un'attestazione ImmutableID (ad esempio, un ID di accesso alternativo) è necessario tooprovide un'attestazione corrispondente per i computer:</span><span class="sxs-lookup"><span data-stu-id="3dbed-194">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="3dbed-195">In hello le sezioni seguenti, reperire informazioni relative a:</span><span class="sxs-lookup"><span data-stu-id="3dbed-195">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="3dbed-196">i valori Hello deve avere ogni attestazione</span><span class="sxs-lookup"><span data-stu-id="3dbed-196">hello values each claim should have</span></span>
- <span data-ttu-id="3dbed-197">Come si presenta una definizione in AD FS</span><span class="sxs-lookup"><span data-stu-id="3dbed-197">How a definition would look like in AD FS</span></span>

<span data-ttu-id="3dbed-198">definizione di Hello consente tooverify se sono presenti valori hello o se è necessario toocreate li.</span><span class="sxs-lookup"><span data-stu-id="3dbed-198">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="3dbed-199">Se non si utilizza ADFS per il server federativo locale, seguire queste attestazioni tooissue del fornitore istruzioni toocreate hello configurazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="3dbed-199">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="3dbed-200">Rilasciare l'attestazione del tipo di account</span><span class="sxs-lookup"><span data-stu-id="3dbed-200">Issue account type claim</span></span>

<span data-ttu-id="3dbed-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Questa attestazione deve contenere un valore di **dispositivo**, che identifica il dispositivo hello come un computer aggiunto al dominio.</span><span class="sxs-lookup"><span data-stu-id="3dbed-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="3dbed-202">In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="3dbed-202">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="3dbed-203">Problema objectGUID di hello computer account locale</span><span class="sxs-lookup"><span data-stu-id="3dbed-203">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="3dbed-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Questa attestazione deve contenere hello **objectGUID** valore hello locale account computer.</span><span class="sxs-lookup"><span data-stu-id="3dbed-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="3dbed-205">In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="3dbed-205">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="3dbed-206">Problema objectSID hello computer account locale</span><span class="sxs-lookup"><span data-stu-id="3dbed-206">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="3dbed-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Questa attestazione deve contenere hello hello **objectSid** valore hello locale account computer.</span><span class="sxs-lookup"><span data-stu-id="3dbed-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="3dbed-208">In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="3dbed-208">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="3dbed-209">Rilasciare l'attestazione issuerID per il computer in presenza di più nomi di dominio verificati in Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dbed-209">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="3dbed-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Questa attestazione deve contenere hello identificatore URI (Uniform Resource) di uno qualsiasi dei hello verificare i nomi di dominio che si connettono hello locale federation service (AD FS o parte 3) il rilascio hello del token.</span><span class="sxs-lookup"><span data-stu-id="3dbed-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="3dbed-211">In ADFS, è possibile aggiungere regole di trasformazione rilascio come quelli hello seguente in un ordine specifico dopo hello quelli precedenti.</span><span class="sxs-lookup"><span data-stu-id="3dbed-211">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="3dbed-212">Si noti che una regola tooexplicitly problema hello regola per gli utenti è necessario.</span><span class="sxs-lookup"><span data-stu-id="3dbed-212">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="3dbed-213">In regole hello indicate di seguito, viene aggiunto una prima regola che identifica l'utente e l'autenticazione del computer.</span><span class="sxs-lookup"><span data-stu-id="3dbed-213">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="3dbed-214">Nell'attestazione hello precedente,</span><span class="sxs-lookup"><span data-stu-id="3dbed-214">In hello claim above,</span></span>

- <span data-ttu-id="3dbed-215">`$<domain>`URL del servizio hello AD FS</span><span class="sxs-lookup"><span data-stu-id="3dbed-215">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="3dbed-216">`<verified-domain-name>`è un segnaposto, è necessario tooreplace con uno dei nomi di dominio verificato in Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dbed-216">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="3dbed-217">Per ulteriori informazioni sui nomi di dominio verificato, vedere [aggiungere tooAzure di nome Active Directory un dominio personalizzato](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="3dbed-217">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="3dbed-218">tooget un elenco dei domini aziendali verificati, è possibile utilizzare hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3dbed-218">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="3dbed-220">Rilasciare l'attestazione ImmutableID per il computer quando ne esiste una per gli utenti (ad esempio, è impostato un ID di accesso alternativo)</span><span class="sxs-lookup"><span data-stu-id="3dbed-220">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="3dbed-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**: questa attestazione deve contenere un valore valido per i computer.</span><span class="sxs-lookup"><span data-stu-id="3dbed-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="3dbed-222">In AD FS, è possibile creare una regola di trasformazione rilascio come segue:</span><span class="sxs-lookup"><span data-stu-id="3dbed-222">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="3dbed-223">Regole di trasformazione di helper script toocreate hello AD FS rilascio</span><span class="sxs-lookup"><span data-stu-id="3dbed-223">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="3dbed-224">Hello lo script seguente consente di creazione hello dell'emissione hello trasformare le regole descritte sopra.</span><span class="sxs-lookup"><span data-stu-id="3dbed-224">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="3dbed-225">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="3dbed-225">Remarks</span></span> 

- <span data-ttu-id="3dbed-226">Questo script aggiunge hello toohello esistente regole.</span><span class="sxs-lookup"><span data-stu-id="3dbed-226">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="3dbed-227">Script hello non vengono eseguite due volte perché hello set di regole è necessario aggiungere due volte.</span><span class="sxs-lookup"><span data-stu-id="3dbed-227">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="3dbed-228">Verificare che nessuna regola corrispondente esistenza per queste attestazioni (condizioni hello corrispondente) prima di eseguire script hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="3dbed-228">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="3dbed-229">Se si dispongono di più nomi di dominio verificato (come mostrato nel portale di Azure AD hello o tramite il cmdlet Get-MsolDomains hello), impostare il valore di hello di **$multipleVerifiedDomainNames** in hello di script troppo**$true**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-229">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="3dbed-230">Assicurarsi anche di rimuovere qualsiasi attestazione issuerid esistente che potrebbe essere stata creata da Azure AD Connect o con altri mezzi.</span><span class="sxs-lookup"><span data-stu-id="3dbed-230">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="3dbed-231">Di seguito è riportato un esempio di questa regola:</span><span class="sxs-lookup"><span data-stu-id="3dbed-231">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="3dbed-232">Se è già stata eseguita un' **ImmutableID** attestazioni per gli account utente, impostare il valore di hello di **$immutableIDAlreadyIssuedforUsers** in hello di script troppo**$true**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-232">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="3dbed-233">Passaggio 3: Abilitare dispositivi Windows di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="3dbed-233">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="3dbed-234">Se alcuni dei dispositivi aggiunti a un dominio sono dispositivi Windows di livello inferiore, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="3dbed-234">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="3dbed-235">Impostare un criterio in Azure AD tooenable dispositivi tooregister utenti.</span><span class="sxs-lookup"><span data-stu-id="3dbed-235">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="3dbed-236">Configurare il toosupport di attestazioni locale federation service tooissue **l'autenticazione integrata di Windows (IWA)** per la registrazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3dbed-236">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="3dbed-237">Aggiungere hello Azure AD dispositivo autenticazione endpoint toohello locale nelle zone Intranet tooavoid certificato richiesto per l'autenticazione dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="3dbed-237">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="3dbed-238">Impostare i criteri in Azure AD tooenable dispositivi tooregister utenti</span><span class="sxs-lookup"><span data-stu-id="3dbed-238">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="3dbed-239">tooregister dispositivi di livello inferiore di Windows, è necessario che tale hello impostazione utenti tooallow tooregister dispositivi in Azure AD sia impostato toomake.</span><span class="sxs-lookup"><span data-stu-id="3dbed-239">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="3dbed-240">Nel portale di Azure hello, è possibile trovare questa impostazione in:</span><span class="sxs-lookup"><span data-stu-id="3dbed-240">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="3dbed-241">Hello criterio seguente deve essere impostato troppo**tutti**: **gli utenti possono registrare i propri dispositivi con Azure AD**</span><span class="sxs-lookup"><span data-stu-id="3dbed-241">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Registrare i dispositivi](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="3dbed-243">Configurare il servizio federativo locale</span><span class="sxs-lookup"><span data-stu-id="3dbed-243">Configure on-premises federation service</span></span> 

<span data-ttu-id="3dbed-244">Il servizio federativo locale deve supportare hello emittente **authenticationmehod** e **wiaormultiauthn** attestazioni durante la ricezione di un tipo di autenticazione richiesta componente toohello Azure Active Directory che contiene un resouce_params parametri con un valore codificato come illustrato qui di seguito:</span><span class="sxs-lookup"><span data-stu-id="3dbed-244">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="3dbed-245">Quando arriva una richiesta di questo tipo, servizio federativo locale di hello deve autenticare l'utente di hello utilizzando l'autenticazione integrata di Windows e al completamento dell'operazione, è necessario emettere hello due attestazioni di seguito:</span><span class="sxs-lookup"><span data-stu-id="3dbed-245">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="3dbed-246">In ADFS, è necessario aggiungere una regola di trasformazione rilascio tale metodo di autenticazione hello passate-through.</span><span class="sxs-lookup"><span data-stu-id="3dbed-246">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="3dbed-247">**tooadd questa regola:**</span><span class="sxs-lookup"><span data-stu-id="3dbed-247">**tooadd this rule:**</span></span>

1. <span data-ttu-id="3dbed-248">Nella console di gestione ADFS hello AD andare troppo`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="3dbed-248">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="3dbed-249">Oggetto di relazione di trust relying party di hello piattaforma delle identità di Microsoft Office 365 e quindi scegliere **Modifica regole attestazione**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-249">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="3dbed-250">In hello **regole di trasformazione rilascio** , selezionare **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-250">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="3dbed-251">In hello **regola attestazione** elenco modello, selezionare **inviare attestazioni mediante una regola personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-251">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="3dbed-252">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-252">Select **Next**.</span></span>
6. <span data-ttu-id="3dbed-253">In hello **nome regola attestazione** digitare **Auth Method Claim Rule**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-253">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="3dbed-254">In hello **regola attestazione** casella, hello tipo seguente regola:</span><span class="sxs-lookup"><span data-stu-id="3dbed-254">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="3dbed-255">Nel server federativo, digitare il comando PowerShell hello seguente dopo la sostituzione  **\<RPObjectName\>**  hello relying party nome di oggetto per l'oggetto di relazione di trust AD Azure relying party.</span><span class="sxs-lookup"><span data-stu-id="3dbed-255">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="3dbed-256">Tale oggetto è solitamente denominato **Piattaforma delle identità di Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-256">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="3dbed-257">Aggiungere zone Intranet locale di hello Azure AD dispositivo autenticazione endpoint toohello</span><span class="sxs-lookup"><span data-stu-id="3dbed-257">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="3dbed-258">certificato tooavoid richiede quando gli utenti di registrare dispositivi autenticano tooAzure AD è possibile distribuire un hello tooadd di criteri tooyour dispositivi appartenenti a un dominio seguente URL toohello Intranet locale in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="3dbed-258">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="3dbed-259">Passaggio 4: Controllare la distribuzione e l'implementazione</span><span class="sxs-lookup"><span data-stu-id="3dbed-259">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="3dbed-260">Quando sono stati completati i passaggi di hello necessario, i dispositivi appartenenti a un dominio sono join tooautomatically pronto AD Azure:</span><span class="sxs-lookup"><span data-stu-id="3dbed-260">When you have completed hello required steps, domain-joined devices are ready tooautomatically join Azure AD:</span></span>

- <span data-ttu-id="3dbed-261">Tutti i dispositivi aggiunti a un dominio che eseguono la versione Aggiornamento dell'anniversario di Windows 10 e Windows Server 2016 vengono registrati automaticamente in Azure AD al riavvio del dispositivo o all'accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3dbed-261">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> 

- <span data-ttu-id="3dbed-262">I nuovi dispositivi registrare con Azure AD al dispositivo hello riavvio al termine dell'operazione di aggiunta dominio hello.</span><span class="sxs-lookup"><span data-stu-id="3dbed-262">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

- <span data-ttu-id="3dbed-263">I dispositivi che erano in precedenza Azure AD registrati (ad esempio, per Intune) transizione troppo "*aggiunti a un dominio, AAD registrato*"; tuttavia comporta un tempo per toocomplete questo processo per tutti i dispositivi a causa di toohello normale flusso di attività utente e dominio.</span><span class="sxs-lookup"><span data-stu-id="3dbed-263">Devices that were previously Azure AD registered (for example, for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="3dbed-264">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="3dbed-264">Remarks</span></span>

- <span data-ttu-id="3dbed-265">È possibile utilizzare un'implementazione di hello toocontrol oggetto Criteri di gruppo registrazione automatica di Windows 10 e i computer appartenenti a un dominio di Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="3dbed-265">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="3dbed-266">Windows 10 novembre 2015 aggiornamento aggiunge automaticamente con Azure AD **solo** se è impostato l'oggetto Criteri di gruppo di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="3dbed-266">Windows 10 November 2015 Update automatically joins with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="3dbed-267">toorollout dei computer di livello inferiore di Windows, è possibile distribuire un [pacchetto Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers selezionato.</span><span class="sxs-lookup"><span data-stu-id="3dbed-267">toorollout of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="3dbed-268">Se si esegue il push hello criteri di gruppo oggetto tooWindows 8.1 appartenenti a un dominio, i dispositivi, viene eseguito un tentativo di un join; Tuttavia, è consigliabile utilizzare hello [pacchetto Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toojoin tutti i dispositivi di livello inferiore di Windows.</span><span class="sxs-lookup"><span data-stu-id="3dbed-268">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, a join is attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toojoin all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="3dbed-269">Creare un oggetto Criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="3dbed-269">Create a Group Policy object</span></span> 

<span data-ttu-id="3dbed-270">implementazione di hello toocontrol del computer corrente di Windows, è consigliabile distribuire hello **registrare i computer del dominio come dispositivi** dispositivi toohello di oggetto Criteri di gruppo da tooregister.</span><span class="sxs-lookup"><span data-stu-id="3dbed-270">toocontrol hello rollout of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="3dbed-271">Ad esempio, è possibile distribuire hello criteri tooan unità organizzativa o gruppo di sicurezza tooa.</span><span class="sxs-lookup"><span data-stu-id="3dbed-271">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="3dbed-272">**criteri di hello tooset:**</span><span class="sxs-lookup"><span data-stu-id="3dbed-272">**tooset hello policy:**</span></span>

1. <span data-ttu-id="3dbed-273">Aprire **Server Manager**, quindi andare troppo`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="3dbed-273">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="3dbed-274">Passare nodo toohello corrispondente toohello dominio in cui si desidera tooactivate la registrazione automatica dei computer di Windows corrente.</span><span class="sxs-lookup"><span data-stu-id="3dbed-274">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="3dbed-275">Fare clic con il pulsante destro del mouse su **Oggetti Criteri di gruppo** e quindi scegliere **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-275">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="3dbed-276">Immettere un nome da assegnare all'oggetto Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="3dbed-276">Type a name for your Group Policy object.</span></span> <span data-ttu-id="3dbed-277">Ad esempio, *Aggiunta a identità ibrida di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dbed-277">For example, *Hybrid Azure AD join.</span></span> 
5. <span data-ttu-id="3dbed-278">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-278">Click **OK**.</span></span>
6. <span data-ttu-id="3dbed-279">Fare clic con il pulsante destro del mouse sul nuovo oggetto Criteri di gruppo e scegliere **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-279">Right-click your new Group Policy object, and then select **Edit**.</span></span>
7. <span data-ttu-id="3dbed-280">Andare troppo**configurazione Computer** > **criteri** > **modelli amministrativi** > **Windows Componenti** > **registrazione dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-280">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> 
8. <span data-ttu-id="3dbed-281">Fare clic con il pulsante destro del mouse su **Registra i computer aggiunti a un dominio come dispositivi** e quindi scegliere **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-281">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3dbed-282">Questo modello di criteri di gruppo è stato rinominato da versioni precedenti di console Gestione criteri di gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="3dbed-282">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="3dbed-283">Se si utilizza una versione precedente della console hello, andare troppo`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="3dbed-283">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="3dbed-284">Selezionare **Abilitato** e quindi fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-284">Select **Enabled**, and then click **Apply**.</span></span>
8. <span data-ttu-id="3dbed-285">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-285">Click **OK**.</span></span>
9. <span data-ttu-id="3dbed-286">Hello collegamento posizione tooa dell'oggetto Criteri di gruppo di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="3dbed-286">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="3dbed-287">Ad esempio, è possibile collegarlo tooa specifica unità organizzativa.</span><span class="sxs-lookup"><span data-stu-id="3dbed-287">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="3dbed-288">È anche possibile collegarlo tooa gruppo di sicurezza specifico di computer che uniscono in join automaticamente con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dbed-288">You also could link it tooa specific security group of computers that automatically join with Azure AD.</span></span> <span data-ttu-id="3dbed-289">tooset questo criterio per tutti aggiunti a un dominio Windows 10 e Windows Server 2016 i computer nell'organizzazione, l'oggetto toohello dominio del collegamento hello criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="3dbed-289">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="3dbed-290">Pacchetti di Windows Installer per i computer non Windows 10</span><span class="sxs-lookup"><span data-stu-id="3dbed-290">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="3dbed-291">toojoin dominio legacy i computer Windows in un ambiente federato, è possibile scaricare e installare questi pacchetti Windows Installer (MSI) dall'area Download a hello [all'area di lavoro Microsoft per i computer a Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554)pagina.</span><span class="sxs-lookup"><span data-stu-id="3dbed-291">toojoin domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="3dbed-292">È possibile distribuire il pacchetto di hello mediante un sistema di distribuzione software come System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="3dbed-292">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="3dbed-293">pacchetto Hello supporta opzioni di installazione invisibile all'utente standard hello con hello *quiet* parametro.</span><span class="sxs-lookup"><span data-stu-id="3dbed-293">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="3dbed-294">System Center Configuration Manager Current Branch offre ulteriori vantaggi rispetto alle versioni precedenti, ad esempio hello possibilità tootrack completato registrazioni.</span><span class="sxs-lookup"><span data-stu-id="3dbed-294">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="3dbed-295">Per altre informazioni, vedere [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="3dbed-295">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="3dbed-296">programma di installazione Hello crea un'attività pianificata nel sistema hello che viene eseguito nel contesto dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="3dbed-296">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="3dbed-297">attività Hello viene attivata quando effettua l'accesso utente hello tooWindows.</span><span class="sxs-lookup"><span data-stu-id="3dbed-297">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="3dbed-298">attività Hello aggiunge automaticamente il dispositivo di hello con Azure AD con le credenziali utente hello dopo l'autenticazione utilizzando l'autenticazione integrata di Windows.</span><span class="sxs-lookup"><span data-stu-id="3dbed-298">hello task silently joins hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="3dbed-299">toosee attività pianificata di hello, nel dispositivo hello, andare troppo**Microsoft** > **all'area di lavoro**, quindi andare libreria utilità di pianificazione toohello.</span><span class="sxs-lookup"><span data-stu-id="3dbed-299">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-joined-devices"></a><span data-ttu-id="3dbed-300">Passaggio 5: Verificare i dispositivi aggiunti</span><span class="sxs-lookup"><span data-stu-id="3dbed-300">Step 5: Verify joined devices</span></span>

<span data-ttu-id="3dbed-301">È possibile controllare i dispositivi aggiunti a un esito positivo nell'organizzazione utilizzando hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [modulo PowerShell di Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="3dbed-301">You can check successful joined devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="3dbed-302">output di Hello di questo cmdlet vengono visualizzati i dispositivi registrati e aggiunti con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dbed-302">hello output of this cmdlet shows devices that are registered and joined with Azure AD.</span></span> <span data-ttu-id="3dbed-303">tooget tutti i dispositivi, usare hello **-tutti** parametro, quindi filtro loro utilizzando hello **deviceTrustType** proprietà.</span><span class="sxs-lookup"><span data-stu-id="3dbed-303">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="3dbed-304">I dispositivi aggiunti a un dominio hanno il valore **Domain Joined**.</span><span class="sxs-lookup"><span data-stu-id="3dbed-304">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dbed-305">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3dbed-305">Next steps</span></span>

* [<span data-ttu-id="3dbed-306">Gestione toodevice introduzione in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dbed-306">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
