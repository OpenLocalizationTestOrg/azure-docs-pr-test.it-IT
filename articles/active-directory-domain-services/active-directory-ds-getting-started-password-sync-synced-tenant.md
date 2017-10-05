---
title: 'Azure AD Domain Services: abilitare la sincronizzazione password | Documentazione Microsoft'
description: Introduzione a Servizi di dominio Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 947ea3c9d789ecf5a754001aafcda6f8bcd41047
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="6f121-103">Abilitare la sincronizzazione password con Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="6f121-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="6f121-104">Nelle attività precedenti è stato abilitato Azure Active Directory Domain Services per il tenant di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f121-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="6f121-105">L'attività successiva prevede l'abilitazione della sincronizzazione degli hash delle credenziali necessari per l'autenticazione NTLM (NT LAN Manager) e Kerberos con Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6f121-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="6f121-106">Al termine della configurazione della sincronizzazione delle credenziali, gli utenti potranno accedere al dominio gestito con le credenziali aziendali.</span><span class="sxs-lookup"><span data-stu-id="6f121-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="6f121-107">La procedura da eseguire è diversa per gli account utente solo cloud rispetto agli account utente sincronizzati dalla directory locale tramite Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6f121-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="6f121-108">Se il tenant di Azure AD include una combinazione di utenti solo cloud e utenti dell'istanza locale di AD, è necessario eseguire entrambe le procedure.</span><span class="sxs-lookup"><span data-stu-id="6f121-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="6f121-109">**Account utente solo cloud**: [Sincronizzare le password per gli account utente solo cloud con il dominio gestito](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="6f121-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="6f121-110">**Account utente locali**: [Sincronizzare le password per gli account utente sincronizzati dall'istanza locale di AD con il dominio gestito](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="6f121-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="6f121-111">Attività 5: Abilitare la sincronizzazione password nel dominio gestito per gli account utente sincronizzati con l'istanza locale di AD</span><span class="sxs-lookup"><span data-stu-id="6f121-111">Task 5: enable password synchronization to your managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="6f121-112">Un tenant di Azure AD viene impostato per la sincronizzazione con la directory locale dell'organizzazione con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6f121-112">A synced Azure AD tenant is set to synchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="6f121-113">Per impostazione predefinita, Azure AD Connect non sincronizza gli hash delle credenziali NTLM e Kerberos con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f121-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes to Azure AD.</span></span> <span data-ttu-id="6f121-114">Per usare Servizi di dominio Azure AD, è necessario configurare Azure AD Connect per sincronizzare gli hash delle credenziali necessari per l'autenticazione NTLM e Kerberos.</span><span class="sxs-lookup"><span data-stu-id="6f121-114">To use Azure AD Domain Services, you need to configure Azure AD Connect to synchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="6f121-115">I passaggi seguenti consentono di sincronizzare gli hash delle credenziali necessari dalla directory locale con il tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f121-115">The following steps enable synchronization of the required credential hashes from your on-premises directory to your Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="6f121-116">Se l'organizzazione include account utente sincronizzati dalla directory locale, è necessario abilitare la sincronizzazione degli hash NTLM e Kerberos per usare il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="6f121-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order to use the managed domain.</span></span> <span data-ttu-id="6f121-117">Un account utente sincronizzato è un account creato nella directory locale e viene sincronizzato con il tenant di Azure AD tramite Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6f121-117">A synced user account is an account that was created in your on-premises directory and is synchronized to your Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="6f121-118">Installare o aggiornare Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="6f121-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="6f121-119">Installare l'ultima versione consigliata di Azure AD Connect in un computer aggiunto a un dominio.</span><span class="sxs-lookup"><span data-stu-id="6f121-119">Install the latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="6f121-120">Se esiste già un'istanza del programma di installazione di Azure AD Connect, è necessario aggiornarla per usare la versione più recente di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6f121-120">If you have an existing instance of Azure AD Connect setup, you need to update it to use the latest version of Azure AD Connect.</span></span> <span data-ttu-id="6f121-121">Per evitare problemi o bug noti che potrebbero essere già stati corretti, assicurarsi di usare sempre la versione più recente di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6f121-121">To avoid known issues/bugs that may have already been fixed, ensure you always use the latest version of Azure AD Connect.</span></span>

<span data-ttu-id="6f121-122">**[Scaricare Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="6f121-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="6f121-123">Versione consigliata: **1.1.553.0** - Data di pubblicazione: 27 giugno 2017.</span><span class="sxs-lookup"><span data-stu-id="6f121-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="6f121-124">L'installazione dell'ultima versione consigliata di Azure AD Connect è NECESSARIA per abilitare le credenziali di password legacy (obbligatorio per l'autenticazione NTLM e Kerberos) da sincronizzare nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f121-124">You MUST install the latest recommended release of Azure AD Connect to enable the legacy password credentials (required for NTLM and Kerberos authentication) to synchronize to your Azure AD tenant.</span></span> <span data-ttu-id="6f121-125">Questa funzionalità non è disponibile nelle versioni precedenti di Azure AD Connect o con lo strumento DirSync legacy.</span><span class="sxs-lookup"><span data-stu-id="6f121-125">This functionality is not available in prior releases of Azure AD Connect or with the legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="6f121-126">Le istruzioni per l'installazione di Azure AD Connect sono disponibili nell'articolo [Introduzione ad Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="6f121-126">Installation instructions for Azure AD Connect are available in the following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-to-azure-ad"></a><span data-ttu-id="6f121-127">Abilitare la sincronizzazione di hash di credenziali NTLM e Kerberos in Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f121-127">Enable synchronization of NTLM and Kerberos credential hashes to Azure AD</span></span>
<span data-ttu-id="6f121-128">Eseguire lo script di PowerShell seguente in ogni foresta di Active Directory per forzare la sincronizzazione password completa e abilitare la sincronizzazione degli hash delle credenziali degli utenti locali con il tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f121-128">Execute the following PowerShell script on each AD forest, to force full password synchronization, and enable all on-premises users’ credential hashes to sync to your Azure AD tenant.</span></span> <span data-ttu-id="6f121-129">Questo script consente di sincronizzare gli hash delle credenziali necessari per l'autenticazione NTLM/Kerberos con il tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f121-129">This script enables the credential hashes required for NTLM/Kerberos authentication to be synchronized to your Azure AD tenant.</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

<span data-ttu-id="6f121-130">A seconda delle dimensioni della directory (numero di utenti, gruppi e così via), la sincronizzazione degli hash delle credenziali con Azure AD richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="6f121-130">Depending on the size of your directory (number of users, groups etc.), synchronization of credential hashes to Azure AD takes time.</span></span> <span data-ttu-id="6f121-131">Le password saranno utilizzabili nel dominio gestito dei servizi di dominio Azure Active Directory non appena le hash di credenziali saranno sincronizzate con Azure.</span><span class="sxs-lookup"><span data-stu-id="6f121-131">The passwords will be usable on the Azure AD Domain Services managed domain shortly after the credential hashes have synchronized to Azure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="6f121-132">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="6f121-132">Related Content</span></span>
* [<span data-ttu-id="6f121-133">Abilitare la sincronizzazione password in Servizi di dominio Azure AD per una directory di Azure AD solo cloud</span><span class="sxs-lookup"><span data-stu-id="6f121-133">Enable password synchronization to AAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="6f121-134">Amministrare un dominio gestito di Servizi di dominio Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f121-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="6f121-135">Aggiungere una macchina virtuale Windows a un dominio gestito di Servizi di dominio Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f121-135">Join a Windows virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="6f121-136">Aggiungere una macchina virtuale Red Hat Enterprise Linux a un dominio gestito di Servizi di dominio Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f121-136">Join a Red Hat Enterprise Linux virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
