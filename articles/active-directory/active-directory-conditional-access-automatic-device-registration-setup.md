---
title: Come configurare la registrazione automatica dei dispositivi Windows con Azure Active Directory aggiunti a un dominio | Microsoft Docs
description: Registrare con Azure Active Directory i dispositivi Windows aggiunti a un dominio in modo automatico e invisibile all'utente.
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
ms.openlocfilehash: dccd7df6a5f85df4179c7ea7cfc476cfb57f48c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="a8960-103">Come configurare la registrazione automatica dei dispositivi Windows con Azure Active Directory aggiunti a un dominio</span><span class="sxs-lookup"><span data-stu-id="a8960-103">How to configure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="a8960-104">Per usare l'[accesso condizionale basato su dispositivo di Azure Active Directory](active-directory-conditional-access-azure-portal.md), i computer devono essere registrati in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8960-104">To use [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a8960-105">È possibile ottenere un elenco dei dispositivi registrati nell'organizzazione con il cmdlet [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) del [modulo Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="a8960-105">You can get a list of registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="a8960-106">Questo articolo illustra la procedura per configurare la registrazione automatica dei dispositivi Windows con Azure AD nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a8960-106">This article provides you with the steps for configuring the automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="a8960-107">Per altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="a8960-107">For more information about:</span></span>

- <span data-ttu-id="a8960-108">Vedere l'articolo relativo all'[accesso condizionale basato su dispositivo di Azure Active Directory](active-directory-conditional-access-azure-portal.md) per informazioni sull'accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="a8960-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="a8960-109">Vedere [Windows 10 per le aziende: modalità d'uso dei dispositivi di lavoro](active-directory-azureadjoin-windows10-devices-overview.md) per informazioni sui dispositivi Windows 10 in azienda e il miglioramento dell'esperienza in caso di registrazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8960-109">Windows 10 devices in the workplace and the enhanced experiences when registered with Azure AD, see [Windows 10 for the enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="a8960-110">Windows 10 Enterprise E3 in CSP, vedere la [panoramica su Windows 10 Enterprise E3 in CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="a8960-110">Windows 10 Enterprise E3 in CSP, see the [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="a8960-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a8960-111">Before you begin</span></span>

<span data-ttu-id="a8960-112">Prima di iniziare a configurare la registrazione automatica dei dispositivi Windows aggiunti a un dominio nell'ambiente in uso, è consigliabile acquisire familiarità con gli scenari supportati e i vincoli.</span><span class="sxs-lookup"><span data-stu-id="a8960-112">Before you start configuring the automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="a8960-113">Per una migliore leggibilità delle descrizioni, in questo argomento viene usata la terminologia seguente.</span><span class="sxs-lookup"><span data-stu-id="a8960-113">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="a8960-114">**Dispositivo Windows corrente**: questo termine indica i dispositivi aggiunti a un dominio che eseguono Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a8960-114">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="a8960-115">**Dispositivi Windows di livello inferiore**: questo termine indica tutti i dispositivi Windows aggiunti a un dominio **supportati** che non eseguono Windows 10 né Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a8960-115">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="a8960-116">Dispositivi Windows correnti</span><span class="sxs-lookup"><span data-stu-id="a8960-116">Windows current devices</span></span>

- <span data-ttu-id="a8960-117">Per i dispositivi che eseguono il sistema operativo desktop Windows, è consigliabile usare Windows 10 versione 1607 (Aggiornamento dell'anniversario di Windows 10) o successiva.</span><span class="sxs-lookup"><span data-stu-id="a8960-117">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="a8960-118">La registrazione dei dispositivi Windows correnti **è** supportata in ambienti non federati come le configurazioni con sincronizzazione dell'hash delle password.</span><span class="sxs-lookup"><span data-stu-id="a8960-118">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="a8960-119">Dispositivi Windows di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="a8960-119">Windows down-level devices</span></span>

- <span data-ttu-id="a8960-120">Sono supportati i dispositivi Windows di livello inferiore seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8960-120">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="a8960-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="a8960-121">Windows 8.1</span></span>
    - <span data-ttu-id="a8960-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="a8960-122">Windows 7</span></span>
    - <span data-ttu-id="a8960-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a8960-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="a8960-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a8960-124">Windows Server 2012</span></span>
    - <span data-ttu-id="a8960-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="a8960-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="a8960-126">La registrazione dei dispositivi legacy di Windows **è** supportata in ambienti non federati tramite l'accesso Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="a8960-126">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="a8960-127">Le registrazione di dispositivi legacy di Windows **non è** supportata per i dispositivi che utilizzano profili di roaming.</span><span class="sxs-lookup"><span data-stu-id="a8960-127">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="a8960-128">In caso di roaming delle impostazioni o dei profili, usare Windows 10.</span><span class="sxs-lookup"><span data-stu-id="a8960-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="a8960-129">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a8960-129">Prerequisites</span></span>

<span data-ttu-id="a8960-130">Prima di iniziare ad abilitare la registrazione automatica dei dispositivi aggiunti a un dominio nell'organizzazione, è necessario verificare che sia in esecuzione una versione aggiornata di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a8960-130">Before you start enabling the auto-registration of domain-joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="a8960-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="a8960-131">Azure AD Connect:</span></span>

- <span data-ttu-id="a8960-132">Mantiene l'associazione tra l'account computer nell'istanza locale di Active Directory (AD) e l'oggetto dispositivo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8960-132">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="a8960-133">Abilita altre funzionalità correlate al dispositivo come Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="a8960-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="a8960-134">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="a8960-134">Configuration steps</span></span>

<span data-ttu-id="a8960-135">Questo argomento include i passaggi necessari per tutti gli scenari di configurazione tipici.</span><span class="sxs-lookup"><span data-stu-id="a8960-135">This topic includes the required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="a8960-136">Per una panoramica dei passaggi necessari per il proprio scenario, vedere la tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="a8960-136">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="a8960-137">Passi</span><span class="sxs-lookup"><span data-stu-id="a8960-137">Steps</span></span>                                      | <span data-ttu-id="a8960-138">Dispositivi Windows correnti e sincronizzazione dell'hash delle password</span><span class="sxs-lookup"><span data-stu-id="a8960-138">Windows current and password hash sync</span></span> | <span data-ttu-id="a8960-139">Dispositivi Windows correnti e federazione</span><span class="sxs-lookup"><span data-stu-id="a8960-139">Windows current and federation</span></span> | <span data-ttu-id="a8960-140">Dispositivi Windows di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="a8960-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="a8960-141">Passaggio 1: Configurare il punto di connessione del servizio</span><span class="sxs-lookup"><span data-stu-id="a8960-141">Step 1: Configure service connection point</span></span> | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |
| <span data-ttu-id="a8960-145">Passaggio 2: Configurare il rilascio delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="a8960-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Controllo][1]                    | ![Controllo][1]        |
| <span data-ttu-id="a8960-148">Passaggio 3: Abilitare dispositivi non Windows 10</span><span class="sxs-lookup"><span data-stu-id="a8960-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Controllo][1]        |
| <span data-ttu-id="a8960-150">Passaggio 4: Controllare la distribuzione e l'implementazione</span><span class="sxs-lookup"><span data-stu-id="a8960-150">Step 4: Control deployment and rollout</span></span>     | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |
| <span data-ttu-id="a8960-154">Passaggio 5: Verificare i dispositivi registrati</span><span class="sxs-lookup"><span data-stu-id="a8960-154">Step 5: Verify registered devices</span></span>          | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="a8960-158">Passaggio 1: Configurare il punto di connessione del servizio</span><span class="sxs-lookup"><span data-stu-id="a8960-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="a8960-159">L'oggetto punto di connessione del servizio (SCP, Service Connection Point) viene usato dai dispositivi durante la registrazione per individuare le informazioni del tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8960-159">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="a8960-160">Nell'istanza locale di Active Directory (AD), l'oggetto SCP per la registrazione automatica dei dispositivi aggiunti a un dominio deve essere incluso nella partizione del contesto dei nomi di configurazione della foresta del computer.</span><span class="sxs-lookup"><span data-stu-id="a8960-160">In your on-premises Active Directory (AD), the SCP object for the auto-registration of domain-joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="a8960-161">Esiste un solo contesto dei nomi di configurazione per foresta.</span><span class="sxs-lookup"><span data-stu-id="a8960-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="a8960-162">In una configurazione di Active Directory a più foreste, il punto di connessione del servizio deve essere presente in tutte le foreste contenenti computer aggiunti a un dominio.</span><span class="sxs-lookup"><span data-stu-id="a8960-162">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="a8960-163">Per recuperare il contesto dei nomi di configurazione della foresta è possibile usare il cmdlet [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8960-163">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="a8960-164">Per una foresta con nome di dominio di Active Directory *fabrikam.com*, il contesto dei nomi di configurazione è il seguente:</span><span class="sxs-lookup"><span data-stu-id="a8960-164">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="a8960-165">Nella foresta, l'oggetto SCP per la registrazione automatica dei dispositivi aggiunti a un dominio si trova in:</span><span class="sxs-lookup"><span data-stu-id="a8960-165">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="a8960-166">A seconda di come è stato distribuito Azure AD Connect, l'oggetto SCP potrebbe essere già stato configurato.</span><span class="sxs-lookup"><span data-stu-id="a8960-166">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="a8960-167">È possibile verificare l'esistenza dell'oggetto e recuperare i valori per l'individuazione con lo script di Windows PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="a8960-167">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="a8960-168">L'output di **$scp.Keywords** mostra le informazioni sul tenant di Azure AD, per esempio:</span><span class="sxs-lookup"><span data-stu-id="a8960-168">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="a8960-169">Se il punto di connessione del servizio non esiste, è possibile crearlo eseguendo il cmdlet `Initialize-ADSyncDomainJoinedComputerSync` nel server Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a8960-169">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="a8960-170">Per eseguire questo cmdlet sono necessarie le credenziali di amministratore dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a8960-170">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="a8960-171">Il cmdlet esegue queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="a8960-171">The cmdlet:</span></span>

- <span data-ttu-id="a8960-172">Crea il punto di connessione del servizio nella foresta di Active Directory a cui è connesso Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a8960-172">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="a8960-173">Richiede che si specifichi il parametro `AdConnectorAccount`,</span><span class="sxs-lookup"><span data-stu-id="a8960-173">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="a8960-174">che è l'account configurato come account connettore di Active Directory in Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a8960-174">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="a8960-175">Lo script seguente mostra un esempio dell'uso del cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a8960-175">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="a8960-176">In questo script, `$aadAdminCred = Get-Credential` richiede la digitazione di un nome utente.</span><span class="sxs-lookup"><span data-stu-id="a8960-176">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="a8960-177">È necessario specificare il nome utente in formato UPN (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="a8960-177">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="a8960-178">Il `Initialize-ADSyncDomainJoinedComputerSync` cmdlet esegue queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="a8960-178">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="a8960-179">usa il modulo Active Directory PowerShell, che si basa sull'esecuzione di Servizi Web Active Directory in un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="a8960-179">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="a8960-180">Il servizio Servizi Web Active Directory è supportato nei controller di dominio che eseguono Windows Server 2008 R2 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a8960-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="a8960-181">È supportato solo per il **modulo MSOnline PowerShell versione 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="a8960-181">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="a8960-182">Per scaricare questo modulo, utilizzare il [collegamento](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="a8960-182">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="a8960-183">Per i controller di dominio che eseguono Windows Server 2008 o versioni precedenti, usare lo script seguente per creare il punto di connessione del servizio.</span><span class="sxs-lookup"><span data-stu-id="a8960-183">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="a8960-184">In una configurazione a più foreste, è consigliabile usare lo script seguente per creare il punto di connessione del servizio in ogni foresta in cui sono presenti computer:</span><span class="sxs-lookup"><span data-stu-id="a8960-184">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="a8960-185">Passaggio 2: Configurare il rilascio delle attestazioni</span><span class="sxs-lookup"><span data-stu-id="a8960-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="a8960-186">In una configurazione federata di Azure AD, per eseguire l'autenticazione ad Azure AD i dispositivi si basano su Active Directory Federation Services (AD FS) o su un servizio federativo locale di terze parti.</span><span class="sxs-lookup"><span data-stu-id="a8960-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="a8960-187">I dispositivi eseguono l'autenticazione per ottenere un token di accesso per la registrazione nel servizio Registrazione dispositivo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8960-187">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="a8960-188">Per l'autenticazione, i dispositivi Windows correnti usano l'autenticazione integrata di Windows a un endpoint WS-Trust attivo (versione 1.3 o 2005) ospitato dal servizio federativo locale.</span><span class="sxs-lookup"><span data-stu-id="a8960-188">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="a8960-189">Quando si usa AD FS, è necessario abilitare **adfs/services/trust/13/windowstransport** o **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="a8960-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="a8960-190">Se si sta usando il proxy per l'autenticazione Web, assicurarsi anche che l'endpoint venga pubblicato tramite il proxy.</span><span class="sxs-lookup"><span data-stu-id="a8960-190">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="a8960-191">È possibile verificare gli endpoint abilitati nella console di gestione di AD FS, in **Servizio > Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="a8960-191">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="a8960-192">Se non si usa AD FS come servizio federativo locale, seguire le istruzioni del fornitore per verificare che siano supportati endpoint WS-Trust 1.3 o 2005 e che questi vengano pubblicati tramite file Metadata Exchange (MEX).</span><span class="sxs-lookup"><span data-stu-id="a8960-192">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="a8960-193">Per completare la registrazione dei dispositivi, nel token ricevuto dal servizio Registrazione dispositivo Azure Active Directory devono essere presenti le attestazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="a8960-193">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="a8960-194">Il servizio Registrazione dispositivo Azure Active Directory creerà un oggetto dispositivo in Azure AD con alcune di queste informazioni, che verranno quindi usate da Azure AD Connect per associare l'oggetto dispositivo appena creato all'account computer in locale.</span><span class="sxs-lookup"><span data-stu-id="a8960-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="a8960-195">Se si hanno più nomi di dominio verificati, è necessario specificare l'attestazione seguente per i computer:</span><span class="sxs-lookup"><span data-stu-id="a8960-195">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="a8960-196">Se viene già rilasciata un'attestazione ImmutableID (ad esempio, un ID di accesso alternativo), è necessario specificare un'attestazione corrispondente per i computer:</span><span class="sxs-lookup"><span data-stu-id="a8960-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="a8960-197">Nelle sezioni seguenti sono disponibili informazioni su:</span><span class="sxs-lookup"><span data-stu-id="a8960-197">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="a8960-198">I valori necessari in ogni attestazione</span><span class="sxs-lookup"><span data-stu-id="a8960-198">The values each claim should have</span></span>
- <span data-ttu-id="a8960-199">Come si presenta una definizione in AD FS</span><span class="sxs-lookup"><span data-stu-id="a8960-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="a8960-200">La definizione consente di verificare se i valori sono presenti o devono essere creati.</span><span class="sxs-lookup"><span data-stu-id="a8960-200">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="a8960-201">Se non si usa AD FS per il server federativo locale, seguire le istruzioni del fornitore per creare la configurazione appropriata per il rilascio di queste attestazioni.</span><span class="sxs-lookup"><span data-stu-id="a8960-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="a8960-202">Rilasciare l'attestazione del tipo di account</span><span class="sxs-lookup"><span data-stu-id="a8960-202">Issue account type claim</span></span>

<span data-ttu-id="a8960-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**: questa attestazione deve contenere un valore **DJ** che identifica il dispositivo come un computer aggiunto a un dominio.</span><span class="sxs-lookup"><span data-stu-id="a8960-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="a8960-204">In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="a8960-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="a8960-205">Rilasciare l'attestazione objectGUID dell'account computer locale</span><span class="sxs-lookup"><span data-stu-id="a8960-205">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="a8960-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**: questa attestazione deve contenere il valore di **objectGUID** dell'account computer locale.</span><span class="sxs-lookup"><span data-stu-id="a8960-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="a8960-207">In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="a8960-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="a8960-208">Rilasciare l'attestazione objectSID dell'account computer locale</span><span class="sxs-lookup"><span data-stu-id="a8960-208">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="a8960-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**: questa attestazione deve contenere il valore di **objectSID** dell'account computer locale.</span><span class="sxs-lookup"><span data-stu-id="a8960-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="a8960-210">In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="a8960-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="a8960-211">Rilasciare l'attestazione issuerID per il computer in presenza di più nomi di dominio verificati in Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8960-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="a8960-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**: questa attestazione deve contenere l'URI (Uniform Resource Identifier) di tutti i nomi di dominio verificati che si connettono al servizio federativo locale (AD FS o servizio di terze parti) che rilascia il token.</span><span class="sxs-lookup"><span data-stu-id="a8960-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="a8960-213">In AD FS, è possibile aggiungere regole di trasformazione rilascio simili alle seguenti, nell'ordine specificato, dopo quelle riportate sopra.</span><span class="sxs-lookup"><span data-stu-id="a8960-213">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="a8960-214">Si noti che è necessaria una regola per rilasciare in modo esplicito la regola per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="a8960-214">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="a8960-215">Nelle regole seguenti è stata aggiunta una prima regola che identifica l'autenticazione utente in alternativa all'autenticazione computer.</span><span class="sxs-lookup"><span data-stu-id="a8960-215">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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


<span data-ttu-id="a8960-216">Nell'attestazione precedente,</span><span class="sxs-lookup"><span data-stu-id="a8960-216">In the claim above,</span></span>

- <span data-ttu-id="a8960-217">`$<domain>` è l'URL del servizio ADFS</span><span class="sxs-lookup"><span data-stu-id="a8960-217">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="a8960-218">`<verified-domain-name>` è un segnaposto che è necessario sostituire con uno dei nomi di dominio verificati in Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8960-218">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="a8960-219">Per altre informazioni sui nomi dominio verificati, vedere [Aggiungere un nome di dominio personalizzato ad Azure Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="a8960-219">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="a8960-220">Per ottenere un elenco dei domini aziendali verificati, è possibile usare il cmdlet [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="a8960-220">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="a8960-222">Rilasciare l'attestazione ImmutableID per il computer quando ne esiste una per gli utenti (ad esempio, è impostato un ID di accesso alternativo)</span><span class="sxs-lookup"><span data-stu-id="a8960-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="a8960-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**: questa attestazione deve contenere un valore valido per i computer.</span><span class="sxs-lookup"><span data-stu-id="a8960-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="a8960-224">In AD FS, è possibile creare una regola di trasformazione rilascio come segue:</span><span class="sxs-lookup"><span data-stu-id="a8960-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="a8960-225">Script helper per creare le regole di trasformazione rilascio di AD FS</span><span class="sxs-lookup"><span data-stu-id="a8960-225">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="a8960-226">Lo script seguente semplifica la creazione delle regole di trasformazione rilascio descritte sopra.</span><span class="sxs-lookup"><span data-stu-id="a8960-226">The following script helps you with the creation of the issuance transform rules described above.</span></span>

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
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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

### <a name="remarks"></a><span data-ttu-id="a8960-227">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="a8960-227">Remarks</span></span> 

- <span data-ttu-id="a8960-228">Questo script aggiunge le regole a quelle esistenti.</span><span class="sxs-lookup"><span data-stu-id="a8960-228">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="a8960-229">Non eseguire lo script due volte, perché il set di regole verrebbe aggiunto due volte.</span><span class="sxs-lookup"><span data-stu-id="a8960-229">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="a8960-230">Prima di eseguire di nuovo lo script, verificare che non esistano regole corrispondenti per le attestazioni (in condizioni corrispondenti).</span><span class="sxs-lookup"><span data-stu-id="a8960-230">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="a8960-231">Se si hanno più nomi di dominio verificati (in base a quanto visualizzato nel portale di Azure AD o tramite il cmdlet Get-MsolDomains), impostare il valore di **$multipleVerifiedDomainNames** nello script su **$true**.</span><span class="sxs-lookup"><span data-stu-id="a8960-231">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="a8960-232">Assicurarsi anche di rimuovere qualsiasi attestazione issuerid esistente che potrebbe essere stata creata da Azure AD Connect o con altri mezzi.</span><span class="sxs-lookup"><span data-stu-id="a8960-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="a8960-233">Di seguito è riportato un esempio di questa regola:</span><span class="sxs-lookup"><span data-stu-id="a8960-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="a8960-234">Se è già stata rilasciata un'attestazione **ImmutableID** per gli account utente, impostare il valore di **$immutableIDAlreadyIssuedforUsers** nello script su **$true**.</span><span class="sxs-lookup"><span data-stu-id="a8960-234">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="a8960-235">Passaggio 3: Abilitare dispositivi Windows di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="a8960-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="a8960-236">Se alcuni dei dispositivi aggiunti a un dominio sono dispositivi Windows di livello inferiore, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="a8960-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="a8960-237">Impostare un criterio in Azure AD per consentire agli utenti di registrare i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a8960-237">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="a8960-238">Configurare il servizio federativo locale per il rilascio di attestazioni in modo da supportare l'**autenticazione integrata di Windows** per la registrazione dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a8960-238">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="a8960-239">Aggiungere l'endpoint di autenticazione dei dispositivi di Azure AD alle aree Intranet locali per evitare che vengano visualizzate richieste di certificati durante l'autenticazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8960-239">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="a8960-240">Impostare un criterio in Azure AD per consentire agli utenti di registrare i dispositivi</span><span class="sxs-lookup"><span data-stu-id="a8960-240">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="a8960-241">Per registrare i dispositivi Windows di livello inferiore, è necessario verificare che l'impostazione per consentire agli utenti di registrare i dispositivi in Azure AD sia configurata.</span><span class="sxs-lookup"><span data-stu-id="a8960-241">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="a8960-242">Nel portale di Azure, questa impostazione è disponibile in:</span><span class="sxs-lookup"><span data-stu-id="a8960-242">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="a8960-243">Il criterio **Gli utenti possono registrare i propri dispositivi in Azure AD** deve essere impostato su **Tutti**.</span><span class="sxs-lookup"><span data-stu-id="a8960-243">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Registrare i dispositivi](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="a8960-245">Configurare il servizio federativo locale</span><span class="sxs-lookup"><span data-stu-id="a8960-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="a8960-246">Il servizio federativo locale deve supportare il rilascio delle attestazioni **authenticationmehod** e **wiaormultiauthn** alla ricezione di una richiesta di autenticazione per la relying party di Azure AD contenente un parametro resouce_params con un valore codificato come il seguente:</span><span class="sxs-lookup"><span data-stu-id="a8960-246">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="a8960-247">Quando arriva una richiesta di questo tipo, il servizio federativo locale deve autenticare l'utente con l'autenticazione integrata di Windows e al termine rilasciare le due attestazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8960-247">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="a8960-248">In AD FS, è necessario avere una regola di trasformazione rilascio che trasmetta il metodo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a8960-248">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="a8960-249">**Per aggiungere questa regola:**</span><span class="sxs-lookup"><span data-stu-id="a8960-249">**To add this rule:**</span></span>

1. <span data-ttu-id="a8960-250">Nella console di gestione di AD FS passare a `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="a8960-250">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="a8960-251">Fare clic con il pulsante destro del mouse sull'oggetto trust della relying party della Piattaforma delle identità di Microsoft Office 365 e quindi scegliere **Modifica regole attestazione**.</span><span class="sxs-lookup"><span data-stu-id="a8960-251">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="a8960-252">Nella scheda **Regole di trasformazione rilascio** selezionare **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="a8960-252">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="a8960-253">Nell'elenco dei modelli delle **regole di attestazione** selezionare **Inviare attestazioni mediante una regola personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="a8960-253">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="a8960-254">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a8960-254">Select **Next**.</span></span>
6. <span data-ttu-id="a8960-255">Nella casella di testo **Nome regola attestazione** digitare **Auth Method Claim Rule (Regola attestazioni Metodo di autenticazione)**.</span><span class="sxs-lookup"><span data-stu-id="a8960-255">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="a8960-256">Nella casella **Claim rule** (Regola attestazioni) digitare la regola seguente:</span><span class="sxs-lookup"><span data-stu-id="a8960-256">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="a8960-257">Nel server federativo digitare il comando di PowerShell seguente dopo aver sostituito **\<RPObjectName\>** con il nome dell'oggetto relying party per l'oggetto trust della relying party di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8960-257">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="a8960-258">Tale oggetto è solitamente denominato **Piattaforma delle identità di Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="a8960-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="a8960-259">Aggiungere l'endpoint di autenticazione dei dispositivi di Azure AD alle aree Intranet locali</span><span class="sxs-lookup"><span data-stu-id="a8960-259">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="a8960-260">Per evitare che vengano visualizzate richieste di certificati quando gli utenti dei dispositivi registrati eseguono l'autenticazione ad Azure AD, è possibile effettuare il push di un criterio ai dispositivi aggiunti a un dominio per aggiungere l'URL seguente all'area Intranet locale in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="a8960-260">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="a8960-261">Passaggio 4: Controllare la distribuzione e l'implementazione</span><span class="sxs-lookup"><span data-stu-id="a8960-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="a8960-262">Dopo che i passaggi necessari sono stati completati, i dispositivi aggiunti a un dominio sono pronti per la registrazione automatica in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8960-262">When you have completed the required steps, domain-joined devices are ready to automatically register with Azure AD.</span></span> <span data-ttu-id="a8960-263">Tutti i dispositivi aggiunti a un dominio che eseguono la versione Aggiornamento dell'anniversario di Windows 10 e Windows Server 2016 vengono registrati automaticamente in Azure AD al riavvio del dispositivo o all'accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a8960-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="a8960-264">I nuovi dispositivi vengono registrati in Azure AD al riavvio del dispositivo al termine dell'operazione di aggiunta a un dominio.</span><span class="sxs-lookup"><span data-stu-id="a8960-264">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

<span data-ttu-id="a8960-265">I dispositivi che erano in precedenza collegati all'area di lavoro di Azure Active Directory (ad esempio per Intune), effettuano ora una transizione a "*Aggiunto a dominio, registrazione AAD effettuata*"; tuttavia, il completamento del processo su tutti i dispositivi richiede tempo a causa del normale flusso di attività del dominio e dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a8960-265">Devices that were previously workplace-joined to Azure AD (for example for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="a8960-266">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="a8960-266">Remarks</span></span>

- <span data-ttu-id="a8960-267">Per controllare l'implementazione della registrazione automatica dei computer Windows 10 e Windows Server 2016 aggiunti al dominio, è possibile usare un oggetto Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="a8960-267">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="a8960-268">Con l'aggiornamento di novembre 2015 di Windows 10, la registrazione automatica in Azure AD viene eseguita **solo** se è impostato l'oggetto Criteri di gruppo di implementazione.</span><span class="sxs-lookup"><span data-stu-id="a8960-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="a8960-269">Per implementare la registrazione automatica dei computer Windows di livello inferiore, è possibile distribuire un [pacchetto di Windows Installer](#windows-installer-packages-for-non-windows-10-computers) nei computer selezionati.</span><span class="sxs-lookup"><span data-stu-id="a8960-269">To rollout the automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="a8960-270">Se si effettua il push dell'oggetto Criteri di gruppo a dispositivi Windows 8.1 aggiunti a un dominio, viene tentata la registrazione. È tuttavia consigliabile usare il [pacchetto di Windows Installer](#windows-installer-packages-for-non-windows-10-computers) per registrare tutti i dispositivi Windows di livello inferiore.</span><span class="sxs-lookup"><span data-stu-id="a8960-270">If you push the Group Policy object to Windows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to register all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="a8960-271">Creare un oggetto Criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="a8960-271">Create a Group Policy object</span></span> 

<span data-ttu-id="a8960-272">Per controllare l'implementazione della registrazione automatica dei computer Windows correnti, è consigliabile distribuire l'oggetto Criteri di gruppo **Registra i computer aggiunti a un dominio come dispositivi** nei dispositivi che si vuole registrare.</span><span class="sxs-lookup"><span data-stu-id="a8960-272">To control the rollout of automatic registration of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="a8960-273">Ad esempio, è possibile distribuire i criteri a un'unità organizzativa o a un gruppo di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a8960-273">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="a8960-274">**Per impostare i criteri:**</span><span class="sxs-lookup"><span data-stu-id="a8960-274">**To set the policy:**</span></span>

1. <span data-ttu-id="a8960-275">Aprire **Server Manager** e quindi passare a `Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="a8960-275">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="a8960-276">Passare al nodo corrispondente al dominio in cui si vuole attivare la registrazione automatica dei computer Windows correnti.</span><span class="sxs-lookup"><span data-stu-id="a8960-276">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="a8960-277">Fare clic con il pulsante destro del mouse su **Oggetti Criteri di gruppo** e quindi scegliere **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="a8960-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="a8960-278">Immettere un nome da assegnare all'oggetto Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="a8960-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="a8960-279">Ad esempio, *Registrazione automatica in Azure AD*.</span><span class="sxs-lookup"><span data-stu-id="a8960-279">For example, *Automatic Registration to Azure AD*.</span></span> <span data-ttu-id="a8960-280">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8960-280">Select **OK**.</span></span>
5. <span data-ttu-id="a8960-281">Fare clic con il pulsante destro del mouse sul nuovo oggetto Criteri di gruppo e scegliere **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="a8960-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="a8960-282">Passare a **Configurazione computer** > **Criteri** > **Modelli amministrativi** > **Componenti di Windows** > **Registrazione dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="a8960-282">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="a8960-283">Fare clic con il pulsante destro del mouse su **Registra i computer aggiunti a un dominio come dispositivi** e quindi scegliere **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="a8960-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a8960-284">Questo modello di Criteri di gruppo è stato rinominato dalle versioni precedenti della console Gestione Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="a8960-284">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="a8960-285">Se si usa una versione precedente della console, passare a `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="a8960-285">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="a8960-286">Selezionare **Abilitato** (Abilitato) e quindi **Apply** (Applica).</span><span class="sxs-lookup"><span data-stu-id="a8960-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="a8960-287">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8960-287">Select **OK**.</span></span>
9. <span data-ttu-id="a8960-288">Collegare l'oggetto Criteri di gruppo a una posizione scelta.</span><span class="sxs-lookup"><span data-stu-id="a8960-288">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="a8960-289">Ad esempio, è possibile collegarlo a una determinata unità organizzativa,</span><span class="sxs-lookup"><span data-stu-id="a8960-289">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="a8960-290">oppure a un determinato gruppo di sicurezza di computer che si registrano automaticamente con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8960-290">You also could link it to a specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="a8960-291">Per impostare questi criteri per tutti i computer Windows 10 e Windows Server 2016 aggiunti a un dominio nell'organizzazione, collegare l'oggetto Criteri di gruppo al dominio.</span><span class="sxs-lookup"><span data-stu-id="a8960-291">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="a8960-292">Pacchetti di Windows Installer per i computer non Windows 10</span><span class="sxs-lookup"><span data-stu-id="a8960-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="a8960-293">Per registrare computer Windows di livello inferiore aggiunti a un dominio in un ambiente federato, è possibile scaricare e installare il pacchetto di Windows Installer (con estensione msi) dalla pagina [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) (Microsoft Workplace Join per computer non Windows 10) dell'Area download.</span><span class="sxs-lookup"><span data-stu-id="a8960-293">To register domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="a8960-294">È possibile distribuire il pacchetto usando un sistema di distribuzione software come System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="a8960-294">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="a8960-295">Il pacchetto supporta le opzioni standard di installazione invisibile all'utente con il parametro *quiet*.</span><span class="sxs-lookup"><span data-stu-id="a8960-295">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="a8960-296">System Center Configuration Manager Current Branch offre vantaggi aggiuntivi rispetto alle versioni precedenti, come la possibilità di tenere traccia delle registrazioni completate.</span><span class="sxs-lookup"><span data-stu-id="a8960-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="a8960-297">Per altre informazioni, vedere [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="a8960-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="a8960-298">Il programma di installazione crea nel sistema un'attività pianificata che viene eseguita nel contesto dell'utente</span><span class="sxs-lookup"><span data-stu-id="a8960-298">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="a8960-299">e attivata nel momento in cui l'utente accede a Windows.</span><span class="sxs-lookup"><span data-stu-id="a8960-299">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="a8960-300">L'attività registra automaticamente il dispositivo in Azure AD con le credenziali dell'utente dopo l'autenticazione con l'autenticazione integrata di Windows.</span><span class="sxs-lookup"><span data-stu-id="a8960-300">The task silently registers the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="a8960-301">Per visualizzare l'attività pianificata, nel dispositivo passare a **Microsoft** > **Workplace Join** e quindi passare alla libreria Utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="a8960-301">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="a8960-302">Passaggio 5: Verificare i dispositivi registrati</span><span class="sxs-lookup"><span data-stu-id="a8960-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="a8960-303">È possibile controllare i dispositivi di cui è stata completata la registrazione nell'organizzazione con il cmdlet [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) del [modulo Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="a8960-303">You can check successful registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="a8960-304">L'output del cmdlet mostra i dispositivi registrati in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8960-304">The output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="a8960-305">Per ottenere tutti i dispositivi, usare il parametro **-All** e quindi filtrare i dispositivi con la proprietà **deviceTrustType**.</span><span class="sxs-lookup"><span data-stu-id="a8960-305">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="a8960-306">I dispositivi aggiunti a un dominio hanno il valore **Domain Joined**.</span><span class="sxs-lookup"><span data-stu-id="a8960-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8960-307">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8960-307">Next steps</span></span>

* [<span data-ttu-id="a8960-308">Domande frequenti sulla registrazione automatica dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="a8960-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="a8960-309">Risoluzione dei problemi di registrazione automatica di computer aggiunti a un dominio in Azure AD: Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a8960-309">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="a8960-310">Risoluzione dei problemi di registrazione automatica di computer aggiunti a un dominio in Azure AD: non Windows 10</span><span class="sxs-lookup"><span data-stu-id="a8960-310">Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="a8960-311">Accesso condizionale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8960-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
