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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Abilitare la sincronizzazione di password tooAzure servizi di dominio Active Directory
Nelle attività precedenti è stato abilitato Azure Active Directory Domain Services per il tenant di Azure Active Directory (Azure AD). attività successiva Hello è tooenable sincronizzazione degli hash delle credenziali necessarie per tooAzure autenticazione NT LAN Manager (NTLM) e Kerberos servizi di dominio Active Directory. Dopo aver configurato la sincronizzazione delle credenziali, gli utenti possono accedere toohello dominio gestiti con le proprie credenziali aziendali.

Hello fasi sono diverse per gli account utente e di account utente solo cloud sincronizzate dalla directory locale con Azure AD Connect. Se il tenant di Azure AD ha una combinazione di cloud solo gli utenti e gli utenti da locale AD, è necessario tooperform entrambi i passaggi.

<br>

> [!div class="op_single_selector"]
> * **Gli account utente solo cloud**: [sincronizzare le password per utenti basata esclusivamente sul cloud gli account di dominio gestiti tooyour](active-directory-ds-getting-started-password-sync.md)
> * **Account utente locali**: [sincronizzare le password per gli account utente sincronizzati da locale AD tooyour gestiti dominio](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>Attività 5: abilitare dominio gestiti con tooyour di sincronizzazione password per gli account utente sincronizzati con locale Active Directory
È stata sincronizzata A Azure AD configurato tenant toosynchronize con la directory dell'organizzazione locale con Azure AD Connect. Per impostazione predefinita, Azure AD Connect non sincronizza NTLM e Kerberos tooAzure di hash di credenziali Active Directory. toouse servizi di dominio Active Directory di Azure, è necessario degli hash delle credenziali toosynchronize Azure AD Connect tooconfigure richiesto per l'autenticazione NTLM e Kerberos. Hello alla procedura seguente abilita la sincronizzazione degli hash delle credenziali hello necessarie dal tenant di Azure AD tooyour directory locale.

> [!NOTE]
> Se l'organizzazione dispone di account utente sincronizzati dalla directory locale, è necessario abilitare la sincronizzazione degli hash NTLM e Kerberos in ordine toouse hello gestito dominio. Un account utente sincronizzato è un account che è stato creato nella directory locale e viene sincronizzato tooyour tenant di Azure AD con Azure AD Connect.
>
>

### <a name="install-or-update-azure-ad-connect"></a>Installare o aggiornare Azure AD Connect
Installare hello consigliato più recente versione di Azure AD Connect in un dominio aggiunti a un computer. Se si dispone di un'istanza esistente del programma di installazione di Azure AD Connect, è necessario tooupdate è toouse hello più recente di Azure AD Connect. tooavoid noti problemi/bug che potrebbero avere già stato risolto, assicurarsi di utilizzare sempre hello la versione più recente di Azure AD Connect.

**[Scaricare Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**

Versione consigliata: **1.1.553.0** - Data di pubblicazione: 27 giugno 2017.

> [!WARNING]
> È necessario installare hello più recente consigliato di rilascio del tenant di Azure AD Connect tooenable hello legacy password delle credenziali (necessarie per l'autenticazione NTLM e Kerberos) toosynchronize tooyour Azure AD. Questa funzionalità non è disponibile nelle versioni precedenti di Azure AD Connect o con lo strumento DirSync legacy hello.
>
>

Istruzioni di installazione per Azure AD Connect sono disponibili in seguito hello articolo - [Introduzione a Azure AD Connect](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a>Abilitare la sincronizzazione di NTLM e Kerberos tooAzure di hash di credenziali Active Directory
Eseguire lo script di PowerShell seguente in ogni foresta di Active Directory, la sincronizzazione completa delle password tooforce, hello e abilitare tenant di tutti i utenti locali credenziali hash toosync tooyour Azure AD. Questo script consente gli hash delle credenziali hello necessari per il tenant di tooyour sincronizzazione Azure AD toobe l'autenticazione NTLM o Kerberos.

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

A seconda delle dimensioni di hello della directory (numero di utenti, gruppi e così via), la sincronizzazione delle credenziali hash tooAzure AD richiede tempo. le password Hello sarà utilizzabile nel dominio gestito di servizi di dominio Active Directory di Azure hello poco dopo gli hash delle credenziali hello sincronizzazione tooAzure Active Directory.

<br>

## <a name="related-content"></a>Contenuti correlati
* [Abilitare la sincronizzazione di password tooAAD servizi di dominio per un solo cloud di Azure directory di Active Directory](active-directory-ds-getting-started-password-sync.md)
* [Amministrare un dominio gestito di Servizi di dominio Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Aggiunta a un dominio gestito con servizi di dominio Active Directory di Azure tooan Windows macchina virtuale](active-directory-ds-admin-guide-join-windows-vm.md)
* [Aggiunta a un dominio gestito con servizi di dominio Active Directory di Azure tooan Red Hat Enterprise Linux macchina virtuale](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
