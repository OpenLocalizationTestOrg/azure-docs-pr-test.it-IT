---
title: 'Azure AD Connect: aggiornamento automatico | Documentazione Microsoft'
description: "Questo argomento descrive hello incorporate funzionalità di aggiornamento automatico della sincronizzazione di Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b395e8f-fa3c-4e55-be54-392dd303c472
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 70d15eb3adf7758d8a43d278157daa504e059a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-automatic-upgrade"></a>Azure AD Connect: aggiornamento automatico
Questa funzionalità è stata introdotta nella build 1.1.105.0 rilasciata nel mese di febbraio 2016.

## <a name="overview"></a>Panoramica
Non è mai stata più semplice con hello assicurandosi che l'installazione di Azure AD Connect è sempre attivo toodate **l'aggiornamento automatico** funzionalità. Questa funzionalità è abilitata per impostazione predefinita per le installazioni rapide e gli aggiornamenti di DirSync. Quando viene rilasciata una nuova versione, l'installazione viene aggiornata automaticamente.

Aggiornamento automatico è abilitato per impostazione predefinita per l'esempio hello:

* Impostazioni rapide e aggiornamenti di DirSync.
* Uso del database LocalDB di SQL Server Express, richiesto sempre per le impostazioni rapide. Anche DirSync con SQL Server Express usa il database LocalDB.
* Hello account di Active Directory è account MSOL_ di hello predefinito creato tramite le impostazioni Express e DirSync.
* Presenti meno di 100.000 oggetti nel metaverse hello.

stato corrente di Hello di aggiornamento automatico può essere visualizzato con i cmdlet di PowerShell hello `Get-ADSyncAutoUpgrade`. Dispone di hello seguenti stati:

| Stato | Commento |
| --- | --- |
| Enabled |L'aggiornamento automatico è abilitato. |
| Suspended |L'impostazione hello solo per il sistema. Hello sistema non è più gli aggiornamenti automatici tooreceive idoneo. |
| Disabled |L'aggiornamento automatico è disabilitato. |

Per passare da **Enabled** a **Disabled**, è possibile usare `Set-ADSyncAutoUpgrade`. Solo sistema hello deve impostare lo stato di hello **Suspended**.

L'aggiornamento automatico utilizza Azure AD Connect Health per l'infrastruttura di aggiornamento hello. Per toowork di aggiornamento automatico, assicurarsi che sia aperte nel server proxy per URL hello **Azure AD Connect Health** come documentato [gli intervalli di indirizzi IP e gli URL di Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Se hello **Synchronization Service Manager** dell'interfaccia utente è in esecuzione nel server di hello, quindi hello aggiornamento viene sospesa fino a quando non viene chiuso hello dell'interfaccia utente.

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se l'installazione di connessione vengono aggiornati come previsto, quindi seguire queste toofind passaggi out ciò che potrebbe essere errata.

In primo luogo, non è opportuno presupporre hello toobe di aggiornamento automatico ha tentato di hello primo giorno che viene rilasciata una nuova versione. Il tentativo di aggiornamento viene eseguito intenzionalmente con una tempistica casuale. Non allarmarsi se l'installazione non viene aggiornata immediatamente.

Se si ritiene che un elemento non è corretto, quindi eseguire `Get-ADSyncAutoUpgrade` tooensure l'aggiornamento automatico è abilitato.

Assicurarsi, quindi che è stato aperto URL hello necessario nel proxy o firewall. Aggiornamento automatico è usando Azure AD Connect Health, come descritto in hello [Panoramica](#overview). Se si utilizza un proxy, verificare che l'integrità è stato configurato toouse un [server proxy](../connect-health/active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy). Verificare inoltre hello [connettività integrità](../connect-health/active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) tooAzure Active Directory.

Con hello connettività tooAzure AD verificato, è ora toolook in registri eventi di hello. Avviare il Visualizzatore eventi hello ed esaminare hello **applicazione** eventlog. Aggiungere un filtro registro eventi per l'origine hello **connettersi AD Azure aggiornare** e intervallo di id evento hello **300-399**.  
![Filtro del registro eventi per l'aggiornamento automatico](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogfilter.png)  

È ora possibile visualizzare i registri eventi di hello associate allo stato di hello per l'aggiornamento automatico.  
![Filtro del registro eventi per l'aggiornamento automatico](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogresult.png)  

codice di risultato Hello ha un prefisso con una panoramica dello stato di hello.

| Prefisso codice risultato | Descrizione |
| --- | --- |
| Success |installazione di Hello è stato aggiornato correttamente. |
| UpgradeAborted |Una condizione temporanea arrestato aggiornamento hello. Verrà ripetuta nuovamente e previsione hello è che abbia esito positivo in un secondo momento. |
| UpgradeNotSupported |sistema di Hello dispone di una configurazione che sta bloccando il sistema hello da viene aggiornato automaticamente. Verrà ritentato toosee se viene modificato lo stato di hello, ma l'aspettativa di hello è che il sistema hello deve essere aggiornato manualmente. |

Di seguito è riportato un elenco di messaggi più comuni di hello desiderati. Non sono elencate tutte, ma il messaggio hello di risultato deve essere chiaro a quale problema hello è.

| Messaggio dei risultati | Descrizione |
| --- | --- |
| **UpgradeAborted** | |
| UpgradeAbortedCouldNotSetUpgradeMarker |Impossibile scrivere toohello del Registro di sistema. |
| UpgradeAbortedInsufficientDatabasePermissions |gruppo administrators predefinito Hello non dispone delle autorizzazioni toohello database. Aggiornare manualmente toohello la versione più recente di Azure AD Connect tooaddress questo problema. |
| UpgradeAbortedInsufficientDiskSpace |Non è disponibile non è sufficiente toosupport di spazio su disco un aggiornamento. |
| UpgradeAbortedSecurityGroupsNotPresent |Impossibile trovare e risolvere tutti i gruppi di sicurezza utilizzati dal motore di sincronizzazione hello. |
| UpgradeAbortedServiceCanNotBeStarted |il servizio NT Hello **Microsoft Azure AD Sync** non è stato possibile toostart. |
| UpgradeAbortedServiceCanNotBeStopped |il servizio NT Hello **Microsoft Azure AD Sync** non è stato possibile toostop. |
| UpgradeAbortedServiceIsNotRunning |il servizio NT Hello **Microsoft Azure AD Sync** non è in esecuzione. |
| UpgradeAbortedSyncCycleDisabled |opzione SyncCycle hello Hello [dell'utilità di pianificazione](active-directory-aadconnectsync-feature-scheduler.md) è stata disabilitata. |
| UpgradeAbortedSyncExeInUse |Hello [gestore servizio di sincronizzazione dell'interfaccia utente](active-directory-aadconnectsync-service-manager-ui.md) è aperta nel server di hello. |
| UpgradeAbortedSyncOrConfigurationInProgress |installazione guidata di Hello è in esecuzione o è stata pianificata una sincronizzazione di fuori dell'utilità di pianificazione di hello. |
| **UpgradeNotSupported** | |
| UpgradeNotSupportedCustomizedSyncRules |È stata aggiunta la propria configurazione toohello regole personalizzate. |
| UpgradeNotSupportedDeviceWritebackEnabled |È stata attivata hello [writeback dei dispositivi](active-directory-aadconnect-feature-device-writeback.md) funzionalità. |
| UpgradeNotSupportedGroupWritebackEnabled |È stata attivata hello [writeback dei gruppi](active-directory-aadconnect-feature-preview.md#group-writeback) funzionalità. |
| UpgradeNotSupportedInvalidPersistedState |installazione di Hello non è un oggetto impostazioni Express o un aggiornamento di DirSync. |
| UpgradeNotSupportedMetaverseSizeExceeeded |Si dispone più di 100.000 oggetti nel metaverse hello. |
| UpgradeNotSupportedMultiForestSetup |Si è connessi toomore rispetto a un insieme di strutture. L'installazione rapida consente di connettersi solo tooone foresta. |
| UpgradeNotSupportedNonLocalDbInstall |Non si sta usando un database LocalDB di SQL Server Express. |
| UpgradeNotSupportedNonMsolAccount |Hello [account Active Directory Connector](active-directory-aadconnect-accounts-permissions.md#active-directory-account) non è l'account predefinito MSOL_ hello più. |
| UpgradeNotSupportedStagingModeEnabled |Hello del server è impostato toobe in [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode). |
| UpgradeNotSupportedUserWritebackEnabled |È stata attivata hello [writeback degli utenti](active-directory-aadconnect-feature-preview.md#user-writeback) funzionalità. |

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
