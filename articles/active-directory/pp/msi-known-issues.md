---
title: "Domande frequenti e problemi noti con gestiti servizio identità (MSI) per Azure Active Directory"
description: "Problemi noti di Identità del servizio gestito per Azure Active Directory."
services: active-directory
documentationcenter: 
author: BryanLa
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: identity
ms.date: 12/15/2017
ms.author: bryanla
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: 7a71010567a76569da969db3d53f71535f96f2d0
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="faq-and-known-issues-with-managed-service-identity-msi-for-azure-active-directory"></a>Domande frequenti e problemi noti con gestiti servizio identità (MSI) per Azure Active Directory

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="does-msi-work-with-azure-cloud-services"></a>Identità del servizio gestito funziona con Servizi cloud di Azure?

No. Non è previsto il supporto di Identità del servizio gestito in Servizi cloud di Azure.

### <a name="does-msi-work-with-the-active-directory-authentication-library-adal-or-the-microsoft-authentication-library-msal"></a>L'Identità del servizio gestito funziona con Active Directory Authentication Library (ADAL) o con Microsoft Authentication Library (MSAL)?

No, l'Identità del servizio gestito non è ancora integrata con ADAL o MSAL. Per informazioni dettagliate sull'acquisizione di un token MSI utilizzando l'endpoint REST MSI, vedere [illustrato come utilizzare un Azure VM gestiti servizio identità (MSI) per l'acquisizione del token](msi-how-to-use-vm-msi-token.md).

### <a name="what-are-the-supported-linux-distributions"></a>Quali sono le distribuzioni di Linux supportate?

Le distribuzioni di Linux seguenti supportano MSI: 

- CoreOS Stable
- CentOS 7.1
- RedHat 7.2
- Ubuntu 15.04

Le altre distribuzioni di Linux attualmente non sono supportate e l'estensione potrebbe non riuscire nelle distribuzioni non supportate.

L'estensione funziona in CentOS 6.9. Tuttavia, a causa della mancanza del supporto di sistema nella versione 6.9, l'estensione non si riavvia automaticamente in caso di arresto anomalo o di arresto. Viene riavviata al riavvio della VM. Per riavviare manualmente l'estensione, vedere [Come si riavvia l'estensione MSI?](#how-do-you-restart-the-msi-extension)

### <a name="how-do-you-restart-the-msi-extension"></a>Come si riavvia l'estensione MSI?
In Windows e alcune versioni di Linux, se si arresta l'estensione, è possibile usare il cmdlet seguente per riavviarla manualmente:

```powershell
Set-AzureRmVMExtension -Name <extension name>  -Type <extension Type>  -Location <location> -Publisher Microsoft.ManagedIdentity -VMName <vm name> -ResourceGroupName <resource group name> -ForceRerun <Any string different from any last value used>
```

Dove: 
- Il nome e il tipo di estensione per Windows è: ManagedIdentityExtensionForWindows
- Il nome e il tipo di estensione per Linux è: ManagedIdentityExtensionForLinux

## <a name="known-issues"></a>Problemi noti

### <a name="automation-script-fails-when-attempting-schema-export-for-msi-extension"></a>Si verifica un errore di "Script di automazione" durante il tentativo di esportazione dello schema per l'estensione dell'identità del servizio gestito

Se l'identità del servizio gestito è abilitata in una macchina virtuale, viene visualizzato l'errore seguente quando si tenta di usare la funzionalità "Script di automazione" per la macchina virtuale o il relativo gruppo di risorse:

![Errore di esportazione dello script di automazione per l'identità del servizio gestito](~/articles/active-directory/media/msi-known-issues/automation-script-export-error.png)

L'estensione della macchina virtuale dell'identità del servizio gestito non supporta attualmente la possibilità di esportare lo schema in un modello di gruppo di risorse. Di conseguenza, il modello generato non include i parametri di configurazione per abilitare l'identità del servizio gestito per la risorsa. È possibile aggiungere manualmente queste sezioni seguendo gli esempi in [Configurare un'Identità del servizio gestito della macchina virtuale tramite un modello](msi-qs-configure-template-windows-vm.md).

Quando è disponibile per l'estensione della macchina virtuale dell'identità del servizio gestito, la funzionalità di esportazione dello schema sarà elencata in [Esportazione di gruppi di risorse contenenti estensioni macchina virtuale](~/articles/virtual-machines/windows/extensions-export-templates.md#supported-virtual-machine-extensions).

### <a name="configuration-blade-does-not-appear-in-the-azure-portal"></a>Il pannello di configurazione non viene visualizzato nel portale di Azure

Se il pannello di configurazione della macchina virtuale non viene visualizzato nella macchina virtuale vuol dire che l'Identità del servizio gestito non è stata ancora abilitata nel portale della propria area geografica.  Ricontrollare in seguito.  È anche possibile abilitare l'Identità del servizio gestito per la macchina virtuale tramite [PowerShell](msi-qs-configure-powershell-windows-vm.md) o l'[interfaccia della riga di comando di Azure](msi-qs-configure-cli-windows-vm.md).

### <a name="cannot-assign-access-to-virtual-machines-in-the-access-control-iam-blade"></a>Impossibile assegnare l'accesso alle macchine virtuali nel pannello Controllo di accesso (IAM)

Se la **macchina virtuale** non viene visualizzata nel portale di Azure come opzione per **Assegna accesso a** in **Controllo di accesso (IAM)** > **Aggiungi autorizzazioni**, vuol dire che l'Identità del servizio gestito non è stata ancora abilitata nel portale della propria area geografica. Ricontrollare in seguito.  È comunque possibile selezionare l'Identità del servizio gestito per l'assegnazione di ruolo eseguendo una ricerca dell'entità servizio dell'Identità del servizio gestito.  Immettere il nome della macchina virtuale nel campo **Seleziona** per visualizzare l'entità servizio nei risultati della ricerca.

### <a name="vm-fails-to-start-after-being-moved-from-resource-group-or-subscription"></a>La macchina virtuale non viene avviata dopo essere stata spostata dal gruppo di risorse o dalla sottoscrizione

Se si sposta una macchina virtuale in esecuzione, questa continuerà a eseguire durante lo spostamento. Tuttavia, dopo lo spostamento, se la macchina virtuale viene arrestata e riavviata, non si avvierà. Questo problema si verifica perché la macchina virtuale non aggiorna il riferimento all'Identità del servizio gestito e continua a puntare a questa nel gruppo di risorse precedente.

**Soluzione alternativa** 
 
Attivare un aggiornamento nella macchina virtuale così da poter ottenere i valori corretti per l'Identità del servizio gestito. È possibile apportare una modifica alla proprietà della macchina virtuale per aggiornare il riferimento all'identità del servizio gestito. Ad esempio, è possibile impostare un nuovo valore di tag nella macchina virtuale con il comando seguente:

```azurecli-interactive
 az  vm update -n <VM Name> -g <Resource Group> --set tags.fixVM=1
```
 
Questo comando imposta un nuovo tag "fixVM" con valore 1 nella macchina virtuale. 
 
Impostando questa proprietà, la macchina virtuale si aggiorna inserendo l'URI della risorsa dell'Identità del servizio gestito corretto. La macchina virtuale dovrebbe a questo punto avviarsi. 
 
Dopo aver avviato la macchina virtuale, il tag può essere rimosso tramite il seguente comando:

```azurecli-interactive
az vm update -n <VM Name> -g <Resource Group> --remove tags.fixVM
```

## <a name="known-issues-with-user-assigned-msi-private-preview-feature"></a>Problemi noti con l'utente assegnato MSI *(funzionalità di anteprima privata)*

- L'unico modo per rimuovere tutti gli utenti assegnati file MSI viene assegnato MSI abilitando il sistema. 
- Provisioning dell'estensione di macchina virtuale a una macchina virtuale potrebbe non riuscire a causa di errori di ricerca DNS. Riavviare la macchina virtuale e riprovare. 
- CLI di Azure: `Az resource show` e `Az resource list` avrà esito negativo in una macchina virtuale con un utente assegnato MSI. In alternativa, usare`az vm/vmss show`
- Esercitazione per archiviazione di Azure è disponibile in Central US EUAP solo al momento. 
- Quando un file MSI di utente assegnato viene concesso l'accesso a una risorsa, il pannello pagine IAM per la risorsa viene "Impossibile accedere ai dati". In alternativa, utilizzare l'interfaccia CLI per Visualizza/Modifica assegnazioni di ruolo per tale risorsa.
- Creazione di un utente assegnato MSI con un carattere di sottolineatura nel nome, non è supportata.
- Quando l'aggiunta di un secondo utente assegnata l'identità, clientID potrebbe non essere disponibili per le richieste di token per tale. Come prevenzione, riavviare l'estensione. MSI VM due bash comandi seguenti:
 - `sudo bash -c "/var/lib/waagent/Microsoft.ManagedIdentity.ManagedIdentityExtensionForLinux-1.0.0.8/msi-extension-handler disable"`
 - `sudo bash -c "/var/lib/waagent/Microsoft.ManagedIdentity.ManagedIdentityExtensionForLinux-1.0.0.8/msi-extension-handler enable"`
- Il VMAgent in Windows non supporta attualmente l'utente assegnato MSI. 
- Assegnazione di un ruolo a un file MSI per accedere a una risorsa attualmente non richiedono autorizzazioni speciali. 
- Quando una macchina virtuale dispone di un utente assegnato MSI, ma nessun sistema assegnato MSI, il portale dell'interfaccia utente risulterà MSI abilitata. Per abilitare MSI assegnato dal sistema, utilizzare un modello di gestione risorse di Azure, un'interfaccia CLI di Azure o un SDK.
