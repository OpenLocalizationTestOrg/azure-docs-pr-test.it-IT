---
title: 'Azure Active Directory Domain Services: guida alla risoluzione dei problemi | Microsoft Docs'
description: Guida alla risoluzione dei problemi di Servizi di dominio di Azure AD
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Guida alla risoluzione dei problemi di Servizi di dominio Azure Active Directory
Questo articolo offre suggerimenti per la risoluzione dei problemi che possono verificarsi quando si configura o si amministra Servizi di dominio di Azure Active Directory (AD).

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>Non è possibile abilitare i Servizi di dominio Azure AD per la directory Azure AD
Questa sezione include risolvere gli errori quando si tenta di tooenable servizi di dominio Active Directory di Azure per la directory e non riesce o ottiene attivata/disattivata too'Disabled indietro '.

Selezionare hello risoluzione corrispondenti toohello messaggio di errore che si verifica.

| **Messaggio di errore** | **Risoluzione** |
| --- |:--- |
| *contoso100.com nome Hello è già in uso nella rete. Specify a name that is not in use.* (Il nome contoso100.com è già in uso nella rete. Specificare un nome non in uso). |[Conflitto di nomi di dominio nella rete virtuale hello](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *Impossibile abilitare Servizi di dominio in questo tenant di Azure AD. servizio Hello non dispone delle autorizzazioni appropriate toohello applicazione denominata 'Sync servizi di dominio Active Directory di Azure'. Eliminare un'applicazione hello chiamata 'Sync servizi di dominio Active Directory di Azure' e provare tooenable servizi di dominio per il tenant di Azure AD.* |[Servizi di dominio non dispone di autorizzazioni adeguate toohello sincronizzazione di servizi di dominio Azure AD applicazione](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *Impossibile abilitare Servizi di dominio in questo tenant di Azure AD. Servizi di dominio dell'applicazione nel tenant di Azure AD non hanno hello Hello necessarie autorizzazioni tooenable servizi di dominio. Eliminare un'applicazione hello con d87dcbc6-a371-462e-88e3-28ad15ec4e64 di identificatore applicazione hello e provare tooenable servizi di dominio per il tenant di Azure AD.* |[Hello applicazione Servizi di dominio non è configurato correttamente nel tenant](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *Impossibile abilitare Servizi di dominio in questo tenant di Azure AD. applicazione di Microsoft Azure AD Hello è disabilitata nel tenant di Azure AD. Abilitare un'applicazione hello con hello applicazione identificatore 00000002-0000-0000-c000-000000000000, quindi provare tooenable servizi di dominio per il tenant di Azure AD.* |[applicazione di Microsoft Graph Hello è disabilitato nel tenant di Azure AD](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>Conflitto di nomi di dominio
**Messaggio di errore:**

*contoso100.com nome Hello è già in uso nella rete. Specify a name that is not in use.* (Il nome contoso100.com è già in uso nella rete. Specificare un nome non in uso).

**Correzione:**

Verificare che non è un dominio esistente con hello stesso nome di dominio sulla rete virtuale. Ad esempio, si supponga di che avere un dominio denominato 'contoso.com' già disponibile nella rete virtuale selezionata hello. In un secondo momento, si tenta di un dominio gestito di servizi di dominio Active Directory di Azure con hello tooenable stesso nome di dominio (ovvero ' contoso.com') nella rete virtuale. Si verifica un errore durante il tentativo di servizi di dominio tooenable Azure AD.

Questo errore è a causa di conflitti tooname hello nome di dominio sulla rete virtuale. In questo caso, è necessario utilizzare tooset un nome diverso, il dominio gestito di servizi di dominio Active Directory di Azure. In alternativa, è possibile annullare il provisioning di dominio esistente hello e quindi procedere servizi di dominio tooenable Azure AD.

### <a name="inadequate-permissions"></a>Autorizzazioni non adeguate
**Messaggio di errore:**

*Impossibile abilitare Servizi di dominio in questo tenant di Azure AD. servizio Hello non dispone delle autorizzazioni appropriate toohello applicazione denominata 'Sync servizi di dominio Active Directory di Azure'. Eliminare un'applicazione hello chiamata 'Sync servizi di dominio Active Directory di Azure' e provare tooenable servizi di dominio per il tenant di Azure AD.*

**Correzione:**

Controllare toosee se è presente un'applicazione con il nome di hello 'Sync servizi di dominio Active Directory di Azure' nella directory di Azure AD. Se l'applicazione esiste, eliminarla e quindi abilitare di nuovo Active Directory Domain Services.

Eseguire hello seguendo i passaggi toocheck presenza hello di un'applicazione hello e toodelete, se esiste un'applicazione hello:

1. Passare toohello **portale di Azure classico** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. Seleziona hello **Active Directory** nodo nel riquadro di sinistra hello.
3. Tenant hello selezionare Azure Active Directory (directory) per il quale si desidera tooenable di servizi di dominio Active Directory di Azure.
4. Passare toohello **applicazioni** scheda.
5. Seleziona hello **applicazioni proprietà dell'azienda** opzione nell'elenco a discesa hello.
6. Cercare un'applicazione denominata **Azure AD Domain Services Sync**. Se un'applicazione hello esiste, procedere toodelete è.
7. Dopo avere eliminato l'applicazione hello, provare nuovamente i servizi di dominio tooenable Azure AD.

### <a name="invalid-configuration"></a>Configurazione non valida.
**Messaggio di errore:**

*Impossibile abilitare Servizi di dominio in questo tenant di Azure AD. Servizi di dominio dell'applicazione nel tenant di Azure AD non hanno hello Hello necessarie autorizzazioni tooenable servizi di dominio. Eliminare un'applicazione hello con d87dcbc6-a371-462e-88e3-28ad15ec4e64 di identificatore applicazione hello e provare tooenable servizi di dominio per il tenant di Azure AD.*

**Correzione:**

Controllare toosee se si dispone di un'applicazione con il nome di hello 'AzureActiveDirectoryDomainControllerServices' (con un identificatore dell'applicazione di d87dcbc6-a371-462e-88e3-28ad15ec4e64) nella directory di Azure AD. Se l'applicazione esiste, è necessario toodelete e quindi i servizi di dominio Azure AD abilitare di nuovo.

Utilizzare hello dopo l'applicazione hello toofind script di PowerShell ed eliminarlo.

> [!NOTE]
> Questo script usa i cmdlet di **Azure AD PowerShell versione 2**. Per un elenco completo di tutti i cmdlet disponibili e il modulo di hello toodownload, leggere hello [la documentazione di riferimento di AzureAD PowerShell](https://msdn.microsoft.com/library/azure/mt757189.aspx).
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Microsoft Graph disabilitato
**Messaggio di errore:**

Domain Services could not be enabled in this Azure AD tenant. applicazione di Microsoft Azure AD Hello è disabilitata nel tenant di Azure AD. Abilitare un'applicazione hello con hello applicazione identificatore 00000002-0000-0000-c000-000000000000, quindi provare tooenable servizi di dominio per il tenant di Azure AD.

**Correzione:**

Controllare toosee se un'applicazione con l'identificatore hello 00000002-0000-0000-c000-000000000000 è disabilitata. Questa applicazione è un'applicazione Microsoft Azure AD hello e offre il tenant di Azure AD tooyour accesso API Graph. Servizi di dominio Active Directory di Azure è necessario questo toosynchronize toobe abilitato applicazione il tooyour tenant di Azure AD gestite dominio.

tooresolve questo errore, abilitare l'applicazione e quindi provare i servizi di dominio tooenable per tenant di Azure AD.

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a>Gli utenti siano grado toosign in toohello dominio gestito di servizi di dominio di Active Directory di Azure
Se uno o più utenti nel tenant di Azure AD non è possibile toosign nel dominio gestito toohello appena creato, eseguire hello risoluzione dei problemi relativi alla procedura seguente:

* **Accedi con formato UPN:** provare toosign nel formato UPN hello (ad esempio, 'joeuser@contoso.com') anziché il formato di nome account SAM hello ('CONTOSO\joeuser'). Hello SAMAccountName può essere generato automaticamente per gli utenti il cui prefisso UPN è troppo lungo o hello stesso come un altro utente nel dominio gestito hello. formato UPN Hello è garantita toobe univoco all'interno di un tenant di Azure AD.

> [!NOTE]
> È consigliabile utilizzare hello UPN formato toosign toohello dominio gestito di servizi di dominio Active Directory di Azure.
>
>

* Assicurarsi di aver [abilitata la sincronizzazione delle password](active-directory-ds-getting-started-password-sync.md) in base ai passaggi hello descritti nella Guida introduttiva hello.
* **Account esterno:** assicurarsi che l'account utente di hello interessato non è un account esterno nel tenant di hello Azure AD. Esempi di account esterni sono gli account Microsoft (ad esempio "joe@live.com") o gli account utente di una directory esterna di Azure AD. Poiché i servizi di dominio Azure Active Directory non dispone di credenziali per questi account utente, questi utenti non possono accedere toohello di dominio gestiti.
* **Sincronizzare gli account:** se gli account utente di hello interessato vengono sincronizzati da una directory locale, verificare che:

  * È stato distribuito o aggiornato toohello [consigliato di versione più recente versione di Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
  * È stato configurato Azure AD Connect troppo[eseguire una sincronizzazione completa](active-directory-ds-getting-started-password-sync.md).
  * A seconda delle dimensioni di hello della directory, può richiedere alcuni minuti per gli account utente e credenziali hash toobe disponibile in servizi di dominio Active Directory di Azure. Verificare che l'attesa per il tempo necessario prima di ritentare l'autenticazione (a seconda delle dimensioni di hello della directory - poche ore tooa o due giorni per la directory di grandi dimensioni).
  * Se il problema di hello persiste dopo la verifica hello passaggi precedenti, provare a riavviare hello servizio Microsoft Azure AD Sync. Dal computer di sincronizzazione, avviare un prompt dei comandi ed eseguire hello seguenti comandi:

    1. net stop 'Microsoft Azure AD Sync'
    2. net start 'Microsoft Azure AD Sync'
* **Account solo cloud**: se l'account utente interessato hello è un account utente solo cloud, assicurarsi che l'utente hello cambiata la password dopo aver abilitato Servizi di dominio Active Directory di Azure. Questa operazione comporta la credenziale hello degli hash necessari per i servizi di dominio AD Azure toobe generato.

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>Gli utenti rimossi dal tenant di Azure AD non vengono rimossi dal dominio gestito
Azure AD impedisce l'eliminazione accidentale di oggetti utente. Quando si elimina un account utente dal tenant di Azure AD, oggetto utente corrispondente hello è spostato toohello Cestino. Quando l'operazione di eliminazione è dominio gestito tooyour sincronizzati, viene generata hello corrispondente toobe account utente contrassegnato come disabilitato. Questa funzionalità consente di recuperare o annullare l'eliminazione di account utente di hello in un secondo momento.

account utente resta in hello disabilitato lo stato del dominio gestito Hello, anche se è ricreare un account utente con hello stesso UPN in directory di Azure AD. account utente di hello tooremove dal dominio gestito, è necessario tooforce eliminarla dal tenant di Azure AD.

account utente di hello tooremove completamente dal dominio gestito, eliminare utente hello in modo permanente dal tenant di Azure AD. Utilizzare i cmdlet di PowerShell di Remove-MsolUser hello con hello '-RemoveFromRecycleBin' opzione, come descritto in questo [articolo MSDN](https://msdn.microsoft.com/library/azure/dn194132.aspx).

## <a name="contact-us"></a>Contattaci
Contattare il team del prodotto Azure Active Directory Domain Services hello troppo[condividere commenti e suggerimenti o per il supporto](active-directory-ds-contact-us.md).
