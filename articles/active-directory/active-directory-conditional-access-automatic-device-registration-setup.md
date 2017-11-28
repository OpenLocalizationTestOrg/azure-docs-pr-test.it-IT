---
title: aaaHow tooconfigure la registrazione automatica dei dispositivi appartenenti a un dominio di Windows con Azure Active Directory | Documenti Microsoft
description: Configurare i server appartenenti a un dominio Windows dispositivi tooregister automatico e invisibile con Azure Active Directory.
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
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="8e736-103">Come la registrazione automatica di Windows tooconfigure dominio dispositivi con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e736-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="8e736-104">toouse [accesso condizionale basato su dispositivo di Azure Active Directory](active-directory-conditional-access-azure-portal.md), i computer devono essere registrati con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e736-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8e736-105">È possibile ottenere un elenco di dispositivi registrati nell'organizzazione utilizzando hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [modulo PowerShell di Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="8e736-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="8e736-106">Questo articolo fornisce passaggi hello per configurare la registrazione automatica dei dispositivi appartenenti a un dominio di Windows hello con Azure AD dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8e736-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="8e736-107">Per altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="8e736-107">For more information about:</span></span>

- <span data-ttu-id="8e736-108">Vedere l'articolo relativo all'[accesso condizionale basato su dispositivo di Azure Active Directory](active-directory-conditional-access-azure-portal.md) per informazioni sull'accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="8e736-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="8e736-109">I dispositivi Windows 10 all'area di lavoro di hello e un'esperienza migliorata hello quando registrato con Azure AD, vedere [Windows 10 per enterprise hello: usare dispositivi per lavoro](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e736-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="8e736-110">Windows 10 Enterprise E3 nel CSP, vedere hello [Windows 10 Enterprise E3 in panoramica CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="8e736-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="8e736-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8e736-111">Before you begin</span></span>

<span data-ttu-id="8e736-112">Prima di iniziare a configurare la registrazione automatica dei dispositivi appartenenti a un dominio di Windows hello nell'ambiente in uso, è consigliabile acquisire familiarità con scenari hello supportato e i vincoli di hello.</span><span class="sxs-lookup"><span data-stu-id="8e736-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="8e736-113">migliorare la leggibilità hello tooimprove delle descrizioni di hello, in questo argomento utilizza hello seguenti termini:</span><span class="sxs-lookup"><span data-stu-id="8e736-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="8e736-114">**Dispositivi di Windows correnti** -questo termine si riferisce unita toodomain dispositivi che eseguono Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8e736-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="8e736-115">**Dispositivi di livello inferiore Windows** -questo termine si riferisce tooall **supportati** dispositivi Windows aggiunti a un dominio che non sono in esecuzione Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8e736-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="8e736-116">Dispositivi Windows correnti</span><span class="sxs-lookup"><span data-stu-id="8e736-116">Windows current devices</span></span>

- <span data-ttu-id="8e736-117">Per i dispositivi che eseguono il sistema operativo desktop di hello Windows, è consigliabile utilizzare aggiornamento Aniversary di Windows 10 (versione 1607) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="8e736-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="8e736-118">registrazione di dispositivi corrente di Windows Hello **è** supportato in ambienti non federati, ad esempio configurazioni di sincronizzazione di hash di password.</span><span class="sxs-lookup"><span data-stu-id="8e736-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="8e736-119">Dispositivi Windows di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="8e736-119">Windows down-level devices</span></span>

- <span data-ttu-id="8e736-120">è supportato i seguenti dispositivi di livello inferiore di Windows Hello:</span><span class="sxs-lookup"><span data-stu-id="8e736-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="8e736-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="8e736-121">Windows 8.1</span></span>
    - <span data-ttu-id="8e736-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="8e736-122">Windows 7</span></span>
    - <span data-ttu-id="8e736-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8e736-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="8e736-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="8e736-124">Windows Server 2012</span></span>
    - <span data-ttu-id="8e736-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="8e736-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="8e736-126">registrazione dei dispositivi legacy di Windows Hello **è** supportato in ambienti non federato tramite l'accesso Single Sign On [Azure Active Directory trasparente Single Sign-On](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="8e736-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="8e736-127">registrazione dei dispositivi legacy di Windows Hello **non** supportati per i dispositivi con i profili.</span><span class="sxs-lookup"><span data-stu-id="8e736-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="8e736-128">In caso di roaming delle impostazioni o dei profili, usare Windows 10.</span><span class="sxs-lookup"><span data-stu-id="8e736-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="8e736-129">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8e736-129">Prerequisites</span></span>

<span data-ttu-id="8e736-130">Prima di iniziare l'abilitazione di hello la registrazione automatica dei dispositivi appartenenti a un dominio all'interno dell'organizzazione, è necessario assicurarsi che si esegue una versione aggiornata di Azure AD toomake connettersi.</span><span class="sxs-lookup"><span data-stu-id="8e736-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="8e736-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="8e736-131">Azure AD Connect:</span></span>

- <span data-ttu-id="8e736-132">Consente di mantenere associazione hello tra account di computer hello in locale di Active Directory (AD) e oggetto dispositivo hello in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e736-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="8e736-133">Abilita altre funzionalità correlate al dispositivo come Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="8e736-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="8e736-134">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="8e736-134">Configuration steps</span></span>

<span data-ttu-id="8e736-135">In questo argomento include i passaggi di hello necessarie per tutti gli scenari di configurazione tipica.</span><span class="sxs-lookup"><span data-stu-id="8e736-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="8e736-136">Utilizzare hello tabella tooget una panoramica dei passaggi di hello necessari per lo scenario seguente:</span><span class="sxs-lookup"><span data-stu-id="8e736-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="8e736-137">Passi</span><span class="sxs-lookup"><span data-stu-id="8e736-137">Steps</span></span>                                      | <span data-ttu-id="8e736-138">Dispositivi Windows correnti e sincronizzazione dell'hash delle password</span><span class="sxs-lookup"><span data-stu-id="8e736-138">Windows current and password hash sync</span></span> | <span data-ttu-id="8e736-139">Dispositivi Windows correnti e federazione</span><span class="sxs-lookup"><span data-stu-id="8e736-139">Windows current and federation</span></span> | <span data-ttu-id="8e736-140">Dispositivi Windows di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="8e736-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="8e736-141">Passaggio 1: Configurare il punto di connessione del servizio</span><span class="sxs-lookup"><span data-stu-id="8e736-141">Step 1: Configure service connection point</span></span> | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |
| <span data-ttu-id="8e736-145">Passaggio 2: Configurare il rilascio delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="8e736-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Controllo][1]                    | ![Controllo][1]        |
| <span data-ttu-id="8e736-148">Passaggio 3: Abilitare dispositivi non Windows 10</span><span class="sxs-lookup"><span data-stu-id="8e736-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Controllo][1]        |
| <span data-ttu-id="8e736-150">Passaggio 4: Controllare la distribuzione e l'implementazione</span><span class="sxs-lookup"><span data-stu-id="8e736-150">Step 4: Control deployment and rollout</span></span>     | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |
| <span data-ttu-id="8e736-154">Passaggio 5: Verificare i dispositivi registrati</span><span class="sxs-lookup"><span data-stu-id="8e736-154">Step 5: Verify registered devices</span></span>          | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="8e736-158">Passaggio 1: Configurare il punto di connessione del servizio</span><span class="sxs-lookup"><span data-stu-id="8e736-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="8e736-159">oggetto di Hello service connection point (SCP) viene utilizzato dai dispositivi durante la registrazione di hello toodiscover informazioni sul tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e736-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="8e736-160">In locale Active Directory (AD), oggetto SCP hello per hello la registrazione automatica dei dispositivi appartenenti a un dominio deve essere presente nella partizione denominazione contesto hello configurazione di foresta hello del computer.</span><span class="sxs-lookup"><span data-stu-id="8e736-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="8e736-161">Esiste un solo contesto dei nomi di configurazione per foresta.</span><span class="sxs-lookup"><span data-stu-id="8e736-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="8e736-162">In una configurazione di Active Directory a più foreste, punto di connessione del servizio hello deve esistere in tutte le foreste contenente i computer appartenenti a un dominio.</span><span class="sxs-lookup"><span data-stu-id="8e736-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="8e736-163">È possibile utilizzare hello [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello contesto dei nomi configurazione della foresta.</span><span class="sxs-lookup"><span data-stu-id="8e736-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="8e736-164">Per una foresta con nome di dominio Active Directory hello *fabrikam.com*, contesto dei nomi di configurazione hello è:</span><span class="sxs-lookup"><span data-stu-id="8e736-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="8e736-165">In una foresta, l'oggetto hello SCP per hello la registrazione automatica dei dispositivi appartenenti a un dominio si trova in:</span><span class="sxs-lookup"><span data-stu-id="8e736-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="8e736-166">A seconda di come è stato distribuito Azure AD Connect, oggetto SCP hello potrebbe sono già stata configurata.</span><span class="sxs-lookup"><span data-stu-id="8e736-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="8e736-167">È possibile verificare l'esistenza di hello dell'oggetto hello e recuperare i valori di individuazione di hello mediante hello lo script di Windows PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="8e736-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="8e736-168">Hello **$scp. Parole chiave** output mostra le informazioni sul tenant hello Azure AD, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8e736-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="8e736-169">Se il punto di connessione servizio hello non esiste, è possibile creare eseguendo hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet nel server di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8e736-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="8e736-170">Credenziali di amministratore dell'organizzazione è necessario toorun questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8e736-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="8e736-171">cmdlet di Hello:</span><span class="sxs-lookup"><span data-stu-id="8e736-171">hello cmdlet:</span></span>

- <span data-ttu-id="8e736-172">Crea punto di connessione del servizio hello in Azure AD Connect è connesso alla foresta di Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="8e736-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="8e736-173">È necessario hello toospecify `AdConnectorAccount` parametro.</span><span class="sxs-lookup"><span data-stu-id="8e736-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="8e736-174">Si tratta di account hello è configurato come account connettore di Azure AD connect di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e736-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="8e736-175">Hello script riportato di seguito viene illustrato un esempio per l'utilizzo di cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="8e736-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="8e736-176">In questo script `$aadAdminCred = Get-Credential` richiede tootype un nome utente.</span><span class="sxs-lookup"><span data-stu-id="8e736-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="8e736-177">È necessario tooprovide hello utente nome nel formato di hello user principal name (UPN) (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="8e736-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="8e736-178">Hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8e736-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="8e736-179">Usa il modulo Active Directory PowerShell hello, che si basa su servizi Web Active Directory in esecuzione in un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="8e736-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="8e736-180">Il servizio Servizi Web Active Directory è supportato nei controller di dominio che eseguono Windows Server 2008 R2 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="8e736-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="8e736-181">È supportato solo da hello **MSOnline PowerShell versione del modulo 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="8e736-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="8e736-182">toodownload questo modulo, utilizzare questo [collegamento](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="8e736-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="8e736-183">Per i controller di dominio che eseguono Windows Server 2008 o versioni precedenti, utilizzare script hello seguente punto di connessione del servizio toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="8e736-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="8e736-184">In una configurazione a più foreste, è consigliabile utilizzare hello script toocreate hello servizio punto di connessione in ogni foresta in cui sono presenti computer seguenti:</span><span class="sxs-lookup"><span data-stu-id="8e736-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="8e736-185">Passaggio 2: Configurare il rilascio delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="8e736-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="8e736-186">Di Azure federato configurazione di Active Directory, i dispositivi si basano su Active Directory Federation Services (ADFS) o un'entità 3 federation service tooauthenticate tooAzure AD in locale.</span><span class="sxs-lookup"><span data-stu-id="8e736-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="8e736-187">I dispositivi si autenticano tooget un tooregister del token di accesso su hello Azure Active Directory Device Registration Service (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="8e736-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="8e736-188">Dispositivi correnti l'autenticazione tramite autenticazione integrata di Windows tooan active endpoint WS-Trust (versione 1.3 o 2005) ospitato nel servizio federativo di hello locale di Windows.</span><span class="sxs-lookup"><span data-stu-id="8e736-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="8e736-189">Quando si usa AD FS, è necessario abilitare **adfs/services/trust/13/windowstransport** o **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="8e736-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="8e736-190">Se si utilizza il Proxy di autenticazione Web hello, assicurarsi anche che questo endpoint verrà pubblicato tramite proxy hello.</span><span class="sxs-lookup"><span data-stu-id="8e736-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="8e736-191">È possibile vedere quali gli endpoint sono abilitati tramite la console di gestione AD FS hello in **servizio > endpoint**.</span><span class="sxs-lookup"><span data-stu-id="8e736-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="8e736-192">Se non si dispone di AD FS come il servizio federativo locale, istruzioni hello di toomake del fornitore che supportano WS-Trust 1.3 o gli endpoint 2005 e che questi sono pubblicati tramite hello file di scambio di metadati (MEX).</span><span class="sxs-lookup"><span data-stu-id="8e736-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="8e736-193">Hello attestazioni riportate di seguito devono essere presente nel token hello ricevuti dal servizio di Azure DRS per toocomplete registrazione dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8e736-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="8e736-194">Azure DRS creerà un oggetto dispositivo in Azure AD con alcune di queste informazioni che viene quindi utilizzate dall'oggetto dispositivo di Azure AD Connect tooassociate hello appena creato con hello computer account locale.</span><span class="sxs-lookup"><span data-stu-id="8e736-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="8e736-195">Se si dispone di più di un nome di dominio verificato, è necessario hello tooprovide attestazioni per i computer seguenti:</span><span class="sxs-lookup"><span data-stu-id="8e736-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="8e736-196">Se già si emette un'attestazione ImmutableID (ad esempio, un ID di accesso alternativo) è necessario tooprovide un'attestazione corrispondente per i computer:</span><span class="sxs-lookup"><span data-stu-id="8e736-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="8e736-197">In hello le sezioni seguenti, reperire informazioni relative a:</span><span class="sxs-lookup"><span data-stu-id="8e736-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="8e736-198">i valori Hello deve avere ogni attestazione</span><span class="sxs-lookup"><span data-stu-id="8e736-198">hello values each claim should have</span></span>
- <span data-ttu-id="8e736-199">Come si presenta una definizione in AD FS</span><span class="sxs-lookup"><span data-stu-id="8e736-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="8e736-200">definizione di Hello consente tooverify se sono presenti valori hello o se è necessario toocreate li.</span><span class="sxs-lookup"><span data-stu-id="8e736-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="8e736-201">Se non si utilizza ADFS per il server federativo locale, seguire queste attestazioni tooissue del fornitore istruzioni toocreate hello configurazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="8e736-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="8e736-202">Rilasciare l'attestazione del tipo di account</span><span class="sxs-lookup"><span data-stu-id="8e736-202">Issue account type claim</span></span>

<span data-ttu-id="8e736-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Questa attestazione deve contenere un valore di **dispositivo**, che identifica il dispositivo hello come un computer aggiunto al dominio.</span><span class="sxs-lookup"><span data-stu-id="8e736-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="8e736-204">In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="8e736-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="8e736-205">Problema objectGUID di hello computer account locale</span><span class="sxs-lookup"><span data-stu-id="8e736-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="8e736-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Questa attestazione deve contenere hello **objectGUID** valore hello locale account computer.</span><span class="sxs-lookup"><span data-stu-id="8e736-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="8e736-207">In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="8e736-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="8e736-208">Problema objectSID hello computer account locale</span><span class="sxs-lookup"><span data-stu-id="8e736-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="8e736-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Questa attestazione deve contenere hello hello **objectSid** valore hello locale account computer.</span><span class="sxs-lookup"><span data-stu-id="8e736-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="8e736-210">In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="8e736-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="8e736-211">Rilasciare l'attestazione issuerID per il computer in presenza di più nomi di dominio verificati in Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e736-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="8e736-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Questa attestazione deve contenere hello identificatore URI (Uniform Resource) di uno qualsiasi dei hello verificare i nomi di dominio che si connettono hello locale federation service (AD FS o parte 3) il rilascio hello del token.</span><span class="sxs-lookup"><span data-stu-id="8e736-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="8e736-213">In ADFS, è possibile aggiungere regole di trasformazione rilascio come quelli hello seguente in un ordine specifico dopo hello quelli precedenti.</span><span class="sxs-lookup"><span data-stu-id="8e736-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="8e736-214">Si noti che una regola tooexplicitly problema hello regola per gli utenti è necessario.</span><span class="sxs-lookup"><span data-stu-id="8e736-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="8e736-215">In regole hello indicate di seguito, viene aggiunto una prima regola che identifica l'utente e l'autenticazione del computer.</span><span class="sxs-lookup"><span data-stu-id="8e736-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

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


<span data-ttu-id="8e736-216">Nell'attestazione hello precedente,</span><span class="sxs-lookup"><span data-stu-id="8e736-216">In hello claim above,</span></span>

- <span data-ttu-id="8e736-217">`$<domain>`URL del servizio hello AD FS</span><span class="sxs-lookup"><span data-stu-id="8e736-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="8e736-218">`<verified-domain-name>`è un segnaposto, è necessario tooreplace con uno dei nomi di dominio verificato in Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e736-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="8e736-219">Per ulteriori informazioni sui nomi di dominio verificato, vedere [aggiungere tooAzure di nome Active Directory un dominio personalizzato](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="8e736-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="8e736-220">tooget un elenco dei domini aziendali verificati, è possibile utilizzare hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8e736-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="8e736-222">Rilasciare l'attestazione ImmutableID per il computer quando ne esiste una per gli utenti (ad esempio, è impostato un ID di accesso alternativo)</span><span class="sxs-lookup"><span data-stu-id="8e736-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="8e736-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**: questa attestazione deve contenere un valore valido per i computer.</span><span class="sxs-lookup"><span data-stu-id="8e736-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="8e736-224">In AD FS, è possibile creare una regola di trasformazione rilascio come segue:</span><span class="sxs-lookup"><span data-stu-id="8e736-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="8e736-225">Regole di trasformazione di helper script toocreate hello AD FS rilascio</span><span class="sxs-lookup"><span data-stu-id="8e736-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="8e736-226">Hello lo script seguente consente di creazione hello dell'emissione hello trasformare le regole descritte sopra.</span><span class="sxs-lookup"><span data-stu-id="8e736-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

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

### <a name="remarks"></a><span data-ttu-id="8e736-227">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="8e736-227">Remarks</span></span> 

- <span data-ttu-id="8e736-228">Questo script aggiunge hello toohello esistente regole.</span><span class="sxs-lookup"><span data-stu-id="8e736-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="8e736-229">Script hello non vengono eseguite due volte perché hello set di regole è necessario aggiungere due volte.</span><span class="sxs-lookup"><span data-stu-id="8e736-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="8e736-230">Verificare che nessuna regola corrispondente esistenza per queste attestazioni (condizioni hello corrispondente) prima di eseguire script hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="8e736-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="8e736-231">Se si dispongono di più nomi di dominio verificato (come mostrato nel portale di Azure AD hello o tramite il cmdlet Get-MsolDomains hello), impostare il valore di hello di **$multipleVerifiedDomainNames** in hello di script troppo**$true**.</span><span class="sxs-lookup"><span data-stu-id="8e736-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="8e736-232">Assicurarsi anche di rimuovere qualsiasi attestazione issuerid esistente che potrebbe essere stata creata da Azure AD Connect o con altri mezzi.</span><span class="sxs-lookup"><span data-stu-id="8e736-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="8e736-233">Di seguito è riportato un esempio di questa regola:</span><span class="sxs-lookup"><span data-stu-id="8e736-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="8e736-234">Se è già stata eseguita un' **ImmutableID** attestazioni per gli account utente, impostare il valore di hello di **$immutableIDAlreadyIssuedforUsers** in hello di script troppo**$true**.</span><span class="sxs-lookup"><span data-stu-id="8e736-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="8e736-235">Passaggio 3: Abilitare dispositivi Windows di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="8e736-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="8e736-236">Se alcuni dei dispositivi aggiunti a un dominio sono dispositivi Windows di livello inferiore, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="8e736-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="8e736-237">Impostare un criterio in Azure AD tooenable dispositivi tooregister utenti.</span><span class="sxs-lookup"><span data-stu-id="8e736-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="8e736-238">Configurare il toosupport di attestazioni locale federation service tooissue **l'autenticazione integrata di Windows (IWA)** per la registrazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8e736-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="8e736-239">Aggiungere hello Azure AD dispositivo autenticazione endpoint toohello locale nelle zone Intranet tooavoid certificato richiesto per l'autenticazione dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="8e736-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="8e736-240">Impostare i criteri in Azure AD tooenable dispositivi tooregister utenti</span><span class="sxs-lookup"><span data-stu-id="8e736-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="8e736-241">tooregister dispositivi di livello inferiore di Windows, è necessario che tale hello impostazione utenti tooallow tooregister dispositivi in Azure AD sia impostato toomake.</span><span class="sxs-lookup"><span data-stu-id="8e736-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="8e736-242">Nel portale di Azure hello, è possibile trovare questa impostazione in:</span><span class="sxs-lookup"><span data-stu-id="8e736-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="8e736-243">Hello criterio seguente deve essere impostato troppo**tutti**: **gli utenti possono registrare i propri dispositivi con Azure AD**</span><span class="sxs-lookup"><span data-stu-id="8e736-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Registrare i dispositivi](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="8e736-245">Configurare il servizio federativo locale</span><span class="sxs-lookup"><span data-stu-id="8e736-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="8e736-246">Il servizio federativo locale deve supportare hello emittente **authenticationmehod** e **wiaormultiauthn** attestazioni durante la ricezione di un tipo di autenticazione richiesta componente toohello Azure Active Directory che contiene un resouce_params parametri con un valore codificato come illustrato qui di seguito:</span><span class="sxs-lookup"><span data-stu-id="8e736-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="8e736-247">Quando arriva una richiesta di questo tipo, servizio federativo locale di hello deve autenticare l'utente di hello utilizzando l'autenticazione integrata di Windows e al completamento dell'operazione, è necessario emettere hello due attestazioni di seguito:</span><span class="sxs-lookup"><span data-stu-id="8e736-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="8e736-248">In ADFS, è necessario aggiungere una regola di trasformazione rilascio tale metodo di autenticazione hello passate-through.</span><span class="sxs-lookup"><span data-stu-id="8e736-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="8e736-249">**tooadd questa regola:**</span><span class="sxs-lookup"><span data-stu-id="8e736-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="8e736-250">Nella console di gestione ADFS hello AD andare troppo`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="8e736-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="8e736-251">Oggetto di relazione di trust relying party di hello piattaforma delle identità di Microsoft Office 365 e quindi scegliere **Modifica regole attestazione**.</span><span class="sxs-lookup"><span data-stu-id="8e736-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="8e736-252">In hello **regole di trasformazione rilascio** , selezionare **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="8e736-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="8e736-253">In hello **regola attestazione** elenco modello, selezionare **inviare attestazioni mediante una regola personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="8e736-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="8e736-254">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8e736-254">Select **Next**.</span></span>
6. <span data-ttu-id="8e736-255">In hello **nome regola attestazione** digitare **Auth Method Claim Rule**.</span><span class="sxs-lookup"><span data-stu-id="8e736-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="8e736-256">In hello **regola attestazione** casella, hello tipo seguente regola:</span><span class="sxs-lookup"><span data-stu-id="8e736-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="8e736-257">Nel server federativo, digitare il comando PowerShell hello seguente dopo la sostituzione  **\<RPObjectName\>**  hello relying party nome di oggetto per l'oggetto di relazione di trust AD Azure relying party.</span><span class="sxs-lookup"><span data-stu-id="8e736-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="8e736-258">Tale oggetto è solitamente denominato **Piattaforma delle identità di Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="8e736-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="8e736-259">Aggiungere zone Intranet locale di hello Azure AD dispositivo autenticazione endpoint toohello</span><span class="sxs-lookup"><span data-stu-id="8e736-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="8e736-260">certificato tooavoid richiede quando gli utenti di registrare dispositivi autenticano tooAzure AD è possibile distribuire un hello tooadd di criteri tooyour dispositivi appartenenti a un dominio seguente URL toohello Intranet locale in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="8e736-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="8e736-261">Passaggio 4: Controllare la distribuzione e l'implementazione</span><span class="sxs-lookup"><span data-stu-id="8e736-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="8e736-262">Quando sono stati completati i passaggi di hello necessario, i dispositivi appartenenti a un dominio sono tooautomatically pronto register con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e736-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="8e736-263">Tutti i dispositivi aggiunti a un dominio che eseguono la versione Aggiornamento dell'anniversario di Windows 10 e Windows Server 2016 vengono registrati automaticamente in Azure AD al riavvio del dispositivo o all'accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8e736-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="8e736-264">I nuovi dispositivi registrare con Azure AD al dispositivo hello riavvio al termine dell'operazione di aggiunta dominio hello.</span><span class="sxs-lookup"><span data-stu-id="8e736-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="8e736-265">I dispositivi che sono stati precedentemente aggiunti all'area di lavoro tooAzure Active Directory (ad esempio per Intune) transizione troppo"*aggiunti a un dominio, AAD registrato*"; tuttavia comporta un tempo per toocomplete questo processo per tutti i dispositivi a causa di toohello normale flusso di attività utente e dominio.</span><span class="sxs-lookup"><span data-stu-id="8e736-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="8e736-266">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="8e736-266">Remarks</span></span>

- <span data-ttu-id="8e736-267">È possibile utilizzare un'implementazione di hello toocontrol oggetto Criteri di gruppo registrazione automatica di Windows 10 e i computer appartenenti a un dominio di Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8e736-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="8e736-268">Windows 10 aggiornamento di novembre 2015 automaticamente registri con Azure AD **solo** se è impostato l'oggetto Criteri di gruppo di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="8e736-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="8e736-269">toorollout hello la registrazione automatica dei computer di livello inferiore di Windows, è possibile distribuire un [pacchetto Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers selezionato.</span><span class="sxs-lookup"><span data-stu-id="8e736-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="8e736-270">Se si esegue il push hello criteri di gruppo oggetto tooWindows 8.1 appartenenti a un dominio, i dispositivi, verrà tentata la registrazione; Tuttavia, è consigliabile utilizzare hello [pacchetto Windows Installer](#windows-installer-packages-for-non-windows-10-computers) tooregister tutti i dispositivi di livello inferiore di Windows.</span><span class="sxs-lookup"><span data-stu-id="8e736-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="8e736-271">Creare un oggetto Criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="8e736-271">Create a Group Policy object</span></span> 

<span data-ttu-id="8e736-272">implementazione di hello toocontrol di registrazione automatica del computer corrente di Windows, è consigliabile distribuire hello **registrare i computer del dominio come dispositivi** dispositivi toohello di oggetto Criteri di gruppo da tooregister.</span><span class="sxs-lookup"><span data-stu-id="8e736-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="8e736-273">Ad esempio, è possibile distribuire hello criteri tooan unità organizzativa o gruppo di sicurezza tooa.</span><span class="sxs-lookup"><span data-stu-id="8e736-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="8e736-274">**criteri di hello tooset:**</span><span class="sxs-lookup"><span data-stu-id="8e736-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="8e736-275">Aprire **Server Manager**, quindi andare troppo`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="8e736-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="8e736-276">Passare nodo toohello corrispondente toohello dominio in cui si desidera tooactivate la registrazione automatica dei computer di Windows corrente.</span><span class="sxs-lookup"><span data-stu-id="8e736-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="8e736-277">Fare clic con il pulsante destro del mouse su **Oggetti Criteri di gruppo** e quindi scegliere **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="8e736-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="8e736-278">Immettere un nome da assegnare all'oggetto Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="8e736-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="8e736-279">Ad esempio, *tooAzure la registrazione automatica AD*.</span><span class="sxs-lookup"><span data-stu-id="8e736-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="8e736-280">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e736-280">Select **OK**.</span></span>
5. <span data-ttu-id="8e736-281">Fare clic con il pulsante destro del mouse sul nuovo oggetto Criteri di gruppo e scegliere **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="8e736-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="8e736-282">Andare troppo**configurazione Computer** > **criteri** > **modelli amministrativi** > **Windows Componenti** > **registrazione dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="8e736-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="8e736-283">Fare clic con il pulsante destro del mouse su **Registra i computer aggiunti a un dominio come dispositivi** e quindi scegliere **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="8e736-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8e736-284">Questo modello di criteri di gruppo è stato rinominato da versioni precedenti di console Gestione criteri di gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="8e736-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="8e736-285">Se si utilizza una versione precedente della console hello, andare troppo`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="8e736-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="8e736-286">Selezionare **Abilitato** (Abilitato) e quindi **Apply** (Applica).</span><span class="sxs-lookup"><span data-stu-id="8e736-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="8e736-287">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e736-287">Select **OK**.</span></span>
9. <span data-ttu-id="8e736-288">Hello collegamento posizione tooa dell'oggetto Criteri di gruppo di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="8e736-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="8e736-289">Ad esempio, è possibile collegarlo tooa specifica unità organizzativa.</span><span class="sxs-lookup"><span data-stu-id="8e736-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="8e736-290">È anche possibile collegarlo tooa gruppo di sicurezza specifico di computer in cui venga registrato automaticamente con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e736-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="8e736-291">tooset questo criterio per tutti aggiunti a un dominio Windows 10 e Windows Server 2016 i computer nell'organizzazione, l'oggetto toohello dominio del collegamento hello criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="8e736-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="8e736-292">Pacchetti di Windows Installer per i computer non Windows 10</span><span class="sxs-lookup"><span data-stu-id="8e736-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="8e736-293">tooregister dominio legacy i computer Windows in un ambiente federato, è possibile scaricare e installare questi pacchetti Windows Installer (MSI) dall'area Download a hello [all'area di lavoro Microsoft per i computer a Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554) pagina.</span><span class="sxs-lookup"><span data-stu-id="8e736-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="8e736-294">È possibile distribuire il pacchetto di hello mediante un sistema di distribuzione software come System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="8e736-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="8e736-295">pacchetto Hello supporta opzioni di installazione invisibile all'utente standard hello con hello *quiet* parametro.</span><span class="sxs-lookup"><span data-stu-id="8e736-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="8e736-296">System Center Configuration Manager Current Branch offre ulteriori vantaggi rispetto alle versioni precedenti, ad esempio hello possibilità tootrack completato registrazioni.</span><span class="sxs-lookup"><span data-stu-id="8e736-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="8e736-297">Per altre informazioni, vedere [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="8e736-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="8e736-298">programma di installazione Hello crea un'attività pianificata nel sistema hello che viene eseguito nel contesto dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="8e736-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="8e736-299">attività Hello viene attivata quando effettua l'accesso utente hello tooWindows.</span><span class="sxs-lookup"><span data-stu-id="8e736-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="8e736-300">attività Hello registra automaticamente il dispositivo hello con Azure AD con le credenziali utente hello dopo l'autenticazione utilizzando l'autenticazione integrata di Windows.</span><span class="sxs-lookup"><span data-stu-id="8e736-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="8e736-301">toosee attività pianificata di hello, nel dispositivo hello, andare troppo**Microsoft** > **all'area di lavoro**, quindi andare libreria utilità di pianificazione toohello.</span><span class="sxs-lookup"><span data-stu-id="8e736-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="8e736-302">Passaggio 5: Verificare i dispositivi registrati</span><span class="sxs-lookup"><span data-stu-id="8e736-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="8e736-303">È possibile controllare l'esito positivo dispositivi registrati nell'organizzazione utilizzando hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [modulo PowerShell di Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="8e736-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="8e736-304">output di Hello di questo cmdlet Mostra dispositivi registrati in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e736-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="8e736-305">tooget tutti i dispositivi, usare hello **-tutti** parametro, quindi filtro loro utilizzando hello **deviceTrustType** proprietà.</span><span class="sxs-lookup"><span data-stu-id="8e736-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="8e736-306">I dispositivi aggiunti a un dominio hanno il valore **Domain Joined**.</span><span class="sxs-lookup"><span data-stu-id="8e736-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e736-307">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e736-307">Next steps</span></span>

* [<span data-ttu-id="8e736-308">Domande frequenti sulla registrazione automatica dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="8e736-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="8e736-309">Risoluzione dei problemi di registrazione automatica del dominio aggiunti a un computer tooAzure AD – Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8e736-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="8e736-310">Risoluzione dei problemi di registrazione automatica del dominio aggiunto tooAzure computer Active Directory-- Windows 10</span><span class="sxs-lookup"><span data-stu-id="8e736-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="8e736-311">Accesso condizionale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e736-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
