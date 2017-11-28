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
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="7e60c-103">Abilitare la sincronizzazione di password tooAzure servizi di dominio Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e60c-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="7e60c-104">Nelle attività precedenti è stato abilitato Azure Active Directory Domain Services per il tenant di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e60c-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="7e60c-105">attività successiva Hello è tooenable sincronizzazione degli hash delle credenziali necessarie per tooAzure autenticazione NT LAN Manager (NTLM) e Kerberos servizi di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7e60c-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="7e60c-106">Dopo aver configurato la sincronizzazione delle credenziali, gli utenti possono accedere toohello dominio gestiti con le proprie credenziali aziendali.</span><span class="sxs-lookup"><span data-stu-id="7e60c-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="7e60c-107">Hello fasi sono diverse per gli account utente e di account utente solo cloud sincronizzate dalla directory locale con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7e60c-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="7e60c-108">Se il tenant di Azure AD ha una combinazione di cloud solo gli utenti e gli utenti da locale AD, è necessario tooperform entrambi i passaggi.</span><span class="sxs-lookup"><span data-stu-id="7e60c-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="7e60c-109">**Gli account utente solo cloud**: [sincronizzare le password per utenti basata esclusivamente sul cloud gli account di dominio gestiti tooyour](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="7e60c-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="7e60c-110">**Account utente locali**: [sincronizzare le password per gli account utente sincronizzati da locale AD tooyour gestiti dominio](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="7e60c-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="7e60c-111">Attività 5: abilitare dominio gestiti con tooyour di sincronizzazione password per gli account utente sincronizzati con locale Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e60c-111">Task 5: enable password synchronization tooyour managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="7e60c-112">È stata sincronizzata A Azure AD configurato tenant toosynchronize con la directory dell'organizzazione locale con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7e60c-112">A synced Azure AD tenant is set toosynchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="7e60c-113">Per impostazione predefinita, Azure AD Connect non sincronizza NTLM e Kerberos tooAzure di hash di credenziali Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7e60c-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes tooAzure AD.</span></span> <span data-ttu-id="7e60c-114">toouse servizi di dominio Active Directory di Azure, è necessario degli hash delle credenziali toosynchronize Azure AD Connect tooconfigure richiesto per l'autenticazione NTLM e Kerberos.</span><span class="sxs-lookup"><span data-stu-id="7e60c-114">toouse Azure AD Domain Services, you need tooconfigure Azure AD Connect toosynchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="7e60c-115">Hello alla procedura seguente abilita la sincronizzazione degli hash delle credenziali hello necessarie dal tenant di Azure AD tooyour directory locale.</span><span class="sxs-lookup"><span data-stu-id="7e60c-115">hello following steps enable synchronization of hello required credential hashes from your on-premises directory tooyour Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="7e60c-116">Se l'organizzazione dispone di account utente sincronizzati dalla directory locale, è necessario abilitare la sincronizzazione degli hash NTLM e Kerberos in ordine toouse hello gestito dominio.</span><span class="sxs-lookup"><span data-stu-id="7e60c-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order toouse hello managed domain.</span></span> <span data-ttu-id="7e60c-117">Un account utente sincronizzato è un account che è stato creato nella directory locale e viene sincronizzato tooyour tenant di Azure AD con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7e60c-117">A synced user account is an account that was created in your on-premises directory and is synchronized tooyour Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="7e60c-118">Installare o aggiornare Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="7e60c-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="7e60c-119">Installare hello consigliato più recente versione di Azure AD Connect in un dominio aggiunti a un computer.</span><span class="sxs-lookup"><span data-stu-id="7e60c-119">Install hello latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="7e60c-120">Se si dispone di un'istanza esistente del programma di installazione di Azure AD Connect, è necessario tooupdate è toouse hello più recente di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7e60c-120">If you have an existing instance of Azure AD Connect setup, you need tooupdate it toouse hello latest version of Azure AD Connect.</span></span> <span data-ttu-id="7e60c-121">tooavoid noti problemi/bug che potrebbero avere già stato risolto, assicurarsi di utilizzare sempre hello la versione più recente di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7e60c-121">tooavoid known issues/bugs that may have already been fixed, ensure you always use hello latest version of Azure AD Connect.</span></span>

<span data-ttu-id="7e60c-122">**[Scaricare Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="7e60c-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="7e60c-123">Versione consigliata: **1.1.553.0** - Data di pubblicazione: 27 giugno 2017.</span><span class="sxs-lookup"><span data-stu-id="7e60c-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="7e60c-124">È necessario installare hello più recente consigliato di rilascio del tenant di Azure AD Connect tooenable hello legacy password delle credenziali (necessarie per l'autenticazione NTLM e Kerberos) toosynchronize tooyour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e60c-124">You MUST install hello latest recommended release of Azure AD Connect tooenable hello legacy password credentials (required for NTLM and Kerberos authentication) toosynchronize tooyour Azure AD tenant.</span></span> <span data-ttu-id="7e60c-125">Questa funzionalità non è disponibile nelle versioni precedenti di Azure AD Connect o con lo strumento DirSync legacy hello.</span><span class="sxs-lookup"><span data-stu-id="7e60c-125">This functionality is not available in prior releases of Azure AD Connect or with hello legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="7e60c-126">Istruzioni di installazione per Azure AD Connect sono disponibili in seguito hello articolo - [Introduzione a Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="7e60c-126">Installation instructions for Azure AD Connect are available in hello following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a><span data-ttu-id="7e60c-127">Abilitare la sincronizzazione di NTLM e Kerberos tooAzure di hash di credenziali Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e60c-127">Enable synchronization of NTLM and Kerberos credential hashes tooAzure AD</span></span>
<span data-ttu-id="7e60c-128">Eseguire lo script di PowerShell seguente in ogni foresta di Active Directory, la sincronizzazione completa delle password tooforce, hello e abilitare tenant di tutti i utenti locali credenziali hash toosync tooyour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e60c-128">Execute hello following PowerShell script on each AD forest, tooforce full password synchronization, and enable all on-premises users’ credential hashes toosync tooyour Azure AD tenant.</span></span> <span data-ttu-id="7e60c-129">Questo script consente gli hash delle credenziali hello necessari per il tenant di tooyour sincronizzazione Azure AD toobe l'autenticazione NTLM o Kerberos.</span><span class="sxs-lookup"><span data-stu-id="7e60c-129">This script enables hello credential hashes required for NTLM/Kerberos authentication toobe synchronized tooyour Azure AD tenant.</span></span>

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

<span data-ttu-id="7e60c-130">A seconda delle dimensioni di hello della directory (numero di utenti, gruppi e così via), la sincronizzazione delle credenziali hash tooAzure AD richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="7e60c-130">Depending on hello size of your directory (number of users, groups etc.), synchronization of credential hashes tooAzure AD takes time.</span></span> <span data-ttu-id="7e60c-131">le password Hello sarà utilizzabile nel dominio gestito di servizi di dominio Active Directory di Azure hello poco dopo gli hash delle credenziali hello sincronizzazione tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7e60c-131">hello passwords will be usable on hello Azure AD Domain Services managed domain shortly after hello credential hashes have synchronized tooAzure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="7e60c-132">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="7e60c-132">Related Content</span></span>
* [<span data-ttu-id="7e60c-133">Abilitare la sincronizzazione di password tooAAD servizi di dominio per un solo cloud di Azure directory di Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e60c-133">Enable password synchronization tooAAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="7e60c-134">Amministrare un dominio gestito di Servizi di dominio Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e60c-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="7e60c-135">Aggiunta a un dominio gestito con servizi di dominio Active Directory di Azure tooan Windows macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7e60c-135">Join a Windows virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="7e60c-136">Aggiunta a un dominio gestito con servizi di dominio Active Directory di Azure tooan Red Hat Enterprise Linux macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7e60c-136">Join a Red Hat Enterprise Linux virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
