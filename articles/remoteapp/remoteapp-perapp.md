---
title: Pubblicare applicazioni per singoli utenti in una raccolta di Azure RemoteApp (anteprima) | Documentazione Microsoft
description: Informazioni su come pubblicare app per i singoli utenti, invece di basarsi sui gruppi, in Azure RemoteApp.
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a>Pubblicare applicazioni per singoli utenti in una raccolta di Azure RemoteApp (anteprima)
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Questo articolo illustra come pubblicare applicazioni per singoli utenti in una raccolta di Azure RemoteApp. Si tratta di una nuova funzionalità di Azure RemoteApp, attualmente disponibile in anteprima privata e solo per alcuni utenti selezionati per finalità di valutazione.

In origine Azure RemoteApp consentiva solo un modo per pubblicare le applicazioni: l'amministratore pubblicava le app dall'immagine e le app risultavano visibili a tutti gli utenti della raccolta.

Uno scenario comune consiste nell'includere molte applicazioni in una singola immagine e distribuire una sola raccolta per ridurre i costi di gestione. Spesso non tutte le applicazioni sono rilevanti per tutti gli utenti. Gli amministratori preferirebbero pubblicare app per i singoli utenti, in modo che gli utenti non vedano applicazioni non necessari nei rispettivi feed dell'applicazione.

Questa operazione è ora possibile in Azure RemoteApp, attualmente disponibile come funzionalità in anteprima limitata. Ecco un breve riepilogo della nuova funzionalità:

1. È possibile impostare una delle due modalità seguenti per una raccolta:
   
   * La modalità raccolta originale, in cui tutti gli utenti di una raccolta possono visualizzare tutte le applicazioni pubblicate. Si tratta della modalità predefinita.
   * La nuova modalità applicazione, in cui gli utenti possono visualizzare solo le applicazioni assegnate in modo esplicito a loro.
2. In questo momento è possibile abilitare la modalità applicazione solo usando i cmdlet di PowerShell di Azure RemoteApp.
   
   * Se viene abilitata la modalità applicazione, l'assegnazione utente nella raccolta non può essere gestita tramite il portale di Azure. L'assegnazione utente deve essere gestita tramite cmdlet di PowerShell.
3. Gli utenti potranno visualizzare solo le applicazioni pubblicate direttamente per loro. Un utente potrà comunque avviare le altre applicazioni disponibili nell'immagine accedendo direttamente alle applicazioni nel sistema operativo.
   
   * Questa funzionalità non offre un blocco sicuro delle applicazioni. Limita solo la visibilità nel feed dell'applicazione.
   * Se è necessario isolare utenti dalle applicazioni, occorrerà usare raccolte separate.

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a>Come ottenere i cmdlet di PowerShell di Azure RemoteApp
Per provare la nuova funzionalità in anteprima, è necessario usare i cmdlet di Azure PowerShell. Non è attualmente possibile usare il portale di gestione di Azure per abilitare la nuova modalità di pubblicazione delle applicazioni.

Assicurarsi prima di tutto che il [modulo Azure PowerShell](/powershell/azure/overview) sia installato.

Avviare quindi la console di PowerShell in modalità amministratore ed eseguire il cmdlet seguente:

        Add-AzureAccount

Verranno richiesti il nome utente e la password di Azure. Dopo l'accesso, sarà possibile eseguire i cmdlet di Azure RemoteApp con le sottoscrizioni di Azure.

## <a name="how-to-check-which-mode-a-collection-is-in"></a>Come verificare la modalità di una raccolta
Eseguire il cmdlet seguente:

        Get-AzureRemoteAppCollection <collectionName>

![Verificare la modalità raccolta](./media/remoteapp-perapp/araacllelvel.png)

La proprietà AclLevel può avere i valori seguenti:

* Collection: modalità di pubblicazione originale. Tutti gli utenti vedono tutte le app pubblicate.
* Application: nuova modalità di pubblicazione. Gli utenti vedono solo le app pubblicate direttamente per loro.

## <a name="how-to-switch-to-application-publishing-mode"></a>Come cambiare la modalità di pubblicazione dell'applicazione
Eseguire il cmdlet seguente:

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

Lo stato di pubblicazione dell'applicazione verrà conservato. Inizialmente tutti gli utenti vedranno tutte le app pubblicate in origine.

## <a name="how-to-list-users-who-can-see-a-specific-application"></a>Come elencare utenti che possono vedere un'applicazione specifica
Eseguire il cmdlet seguente:

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Vengono elencati tutti gli utenti che possono vedere l'applicazione.

Nota: è possibile vedere gli alias dell'applicazione, definiti "alias app" nella sintassi precedente, eseguendo Get-AzureRemoteAppProgram -CollectionName <collectionName>.

## <a name="how-to-assign-an-application-to-a-user"></a>Come assegnare un'applicazione a un utente
Eseguire il cmdlet seguente:

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

L'utente potrà ora vedere l'applicazione nel client Azure RemoteApp e potrà connettersi all'app.

## <a name="how-to-remove-an-application-from-a-user"></a>Come rimuovere un'applicazione da un utente
Eseguire il cmdlet seguente:

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Inviare commenti e suggerimenti
Siamo lieti di ricevere commenti e suggerimenti su questa funzionalità in anteprima. Compilare il [sondaggio](http://www.instant.ly/s/FDdrb) per condividere la propria opinione.

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a>Se non è stato possibile provare la funzionalità in anteprima
Se non si è ancora autorizzati a provare l'anteprima, usare questo [sondaggio](http://www.instant.ly/s/AY83p) per richiedere l'accesso.

