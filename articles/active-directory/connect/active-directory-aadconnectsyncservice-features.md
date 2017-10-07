---
title: "funzionalità e la configurazione del servizio sincronizzazione Connect aaaAzure AD | Documenti Microsoft"
description: "Descrive le funzionalità sul lato del servizio per il Servizio di sincronizzazione Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a>Funzionalità del servizio di sincronizzazione Azure AD Connect
funzionalità di sincronizzazione Hello di Azure AD Connect include due componenti:

* componente di Hello locale denominato **sincronizzazione di Azure AD Connect**, denominati anche **motore di sincronizzazione**.
* servizio Hello che risiedono in Azure AD, noto anche come **il servizio di sincronizzazione di Azure AD Connect**

Questo argomento viene illustrato come hello seguenti funzionalità di hello **servizio di sincronizzazione di Azure AD Connect** lavoro e come è possibile configurare tramite Windows PowerShell.

Queste impostazioni vengono configurate da hello [modulo di Azure Active Directory per Windows PowerShell](http://aka.ms/aadposh). Scaricarlo e installarlo separatamente da Azure AD Connect. i cmdlet di Hello illustrati in questo argomento sono state introdotte in hello [il rilascio di marzo 2016 (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1). Se i cmdlet di hello illustrati in questo argomento non si dispone o non producono hello stesso risultato, quindi assicurarsi che si esegue la versione più recente di hello.

configurazione di hello toosee nella directory di Azure AD, eseguire `Get-MsolDirSyncFeatures`.  
![Risultato di Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

Molte di queste impostazioni possono essere modificate solo da Azure AD Connect.

Hello seguenti possono essere configurate da `Set-MsolDirSyncFeature`:

| DirSyncFeature | Commento |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |Consente oggetti toojoin userPrincipalName indirizzo SMTP tooprimary aggiunta. |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |Consente di hello sincronizzazione motore tooupdate hello userPrincipalName attributo utenti gestiti licenza (non federati). |

Una volta abilitata una funzionalità, non potrà essere disabilitata di nuovo.

> [!NOTE]
> Da 24 agosto 2016 hello funzionalità *duplicato resilienza attributo* è abilitata per impostazione predefinita per la nuova versione di Azure directory di Active Directory. Questa funzionalità sarà implementata e abilitata anche nelle directory create prima di tale data. Si riceverà una notifica di posta elettronica quando la directory sulle tooget abilitata questa funzionalità.
> 
> 

Hello seguenti impostazioni sono configurate da Azure AD Connect e non può essere modificate da `Set-MsolDirSyncFeature`:

| DirSyncFeature | Commento |
| --- | --- |
| DeviceWriteback |[Azure AD Connect: abilitazione del writeback dei dispositivi](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Servizio di sincronizzazione Azure AD Connect: estensioni della directory](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |Consente a un attributo toobe messi in quarantena quando è un duplicato di un altro oggetto anziché errori l'intero oggetto hello durante l'esportazione. |
| PasswordSync |[Implementazione della sincronizzazione password con il servizio di sincronizzazione Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[Anteprima: Writeback dei gruppi](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |Attualmente non è supportata. |

## <a name="duplicate-attribute-resiliency"></a>Duplicate attribute resiliency
Anziché avere esito negativo tooprovision gli oggetti con nomi duplicati UPN / proxyAddresses, dell'attributo duplicato hello è "messi in quarantena" e viene assegnato un valore temporaneo. Quando è stato risolto il conflitto di hello, hello temporaneo UPN viene modificata automaticamente toohello di valore appropriato. Per altre informazioni, vedere [Sincronizzazione delle identità e resilienza degli attributi duplicati](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="userprincipalname-soft-match"></a>Corrispondenza flessibile di userPrincipalName
Quando questa funzionalità è abilitata, soft-match è abilitata per UPN in aggiunta toohello [indirizzo SMTP primario](https://support.microsoft.com/kb/2641663), che è sempre abilitata. Soft-match è toomatch utilizzati gli utenti del cloud esistente in Azure AD con utenti locali.

Se è necessario toomatch AD account locali con gli account esistenti creati in un cloud hello e non si usa Exchange Online, quindi questa funzionalità è utile. In questo scenario, in genere non è un attributo di motivo tooset hello SMTP nel cloud hello.

Questa funzionalità è attivata per impostazione predefinita per le nuove directory di Azure AD . Per vedere se la funzionalità è abilitata per l'utente corrente, eseguire:  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

Se questa funzionalità non è abilitata per la directory di Azure AD in uso, è possibile abilitarla eseguendo:  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>Sincronizzare gli aggiornamenti di userPrincipalName
In passato, attributo UserPrincipalName toohello di aggiornamenti tramite il servizio di sincronizzazione hello locale è stato bloccato solo se entrambe queste condizioni sono vere:

* utente Hello è gestito (non federati).
* utente Hello non è stata assegnata una licenza.

Per ulteriori informazioni, vedere [utente non corrispondono a nomi di Office 365, Azure o Intune hello UPN locale o ID di accesso alternativo](https://support.microsoft.com/kb/2523192).

L'abilitazione di questa funzionalità consente hello sincronizzazione motore tooupdate hello userPrincipalName quando è modificato in locale e si utilizza la sincronizzazione delle password. Se si usa la federazione, questa funzionalità non è supportata.

Questa funzionalità è attivata per impostazione predefinita per le nuove directory di Azure AD . Per vedere se la funzionalità è abilitata per l'utente corrente, eseguire:  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

Se questa funzionalità non è abilitata per la directory di Azure AD in uso, è possibile abilitarla eseguendo:  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

Dopo aver abilitato questa funzionalità, i valori di userPrincipalName esistenti rimarranno invariati. Al prossimo cambio di hello userPrincipalName attributo on-premise, sincronizzazione delta normale hello sugli utenti aggiornerà hello UPN.  

## <a name="see-also"></a>Vedere anche
* [Servizio di sincronizzazione Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

