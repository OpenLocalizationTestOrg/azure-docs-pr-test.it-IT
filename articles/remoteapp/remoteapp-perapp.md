---
title: gli utenti di tooindividual applicazioni aaaPublish in una raccolta RemoteApp di Azure (anteprima) | Documenti Microsoft
description: "Informazioni su come pubblicare gli utenti tooindividual App, anziché in base a gruppi, in Azure RemoteApp."
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
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a>Pubblicare gli utenti tooindividual applicazioni in una raccolta RemoteApp di Azure (anteprima)
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Questo articolo viene illustrato come gli utenti di tooindividual applicazioni toopublish in una raccolta di Azure RemoteApp. Questa è una nuova funzionalità in Azure RemoteApp, attualmente in anteprima privata e adottato disponibili tooselect solo a scopo di valutazione.

Origine RemoteApp di Azure abilitata solo una modalità di pubblicazione di applicazioni: amministratore hello pubblicare le app dall'immagine hello e saranno visibili tooall utenti nella raccolta di hello.

Uno scenario comune è tooinclude molte applicazioni in una singola immagine e la distribuzione dei costi di gestione tooreduce di ordine di una raccolta. Spesso non tutte le applicazioni sono rilevanti tooall utenti: gli amministratori preferisce agli utenti di tooindividual App toopublish in modo non visualizzano le applicazioni non necessarie nella propria applicazione feed.

Questa operazione è ora possibile in Azure RemoteApp, attualmente disponibile come funzionalità in anteprima limitata. Ecco un breve riepilogo delle nuove funzionalità di hello:

1. È possibile impostare una delle due modalità seguenti per una raccolta:
   
   * Hello originale modalità di raccolta, in cui è possono visualizzare tutti gli utenti in una raccolta di applicazioni pubblicate tutte. Questa è una modalità predefinita di hello.
   * modalità applicazione nuova Hello, in cui gli utenti visualizzano solo le applicazioni che sono state assegnate esplicitamente toothem
2. Un determinato momento hello modalità applicazione hello può essere abilitata solo tramite i cmdlet PowerShell di Azure RemoteApp.
   
   * Impostare la modalità di tooapplication, assegnazione di utente nella raccolta di hello quando non può essere gestita tramite hello portale di Azure. Assegnazione utente ha toobe gestite tramite cmdlet di PowerShell.
3. Gli utenti visualizzeranno solo le applicazioni di hello pubblicate direttamente toothem. Tuttavia, è comunque possibile per un utente toolaunch hello altre applicazioni disponibili sull'immagine di hello accedendovi direttamente nel sistema operativo di hello.
   
   * Questa funzionalità non fornisce un blocco di protezione delle applicazioni. Limita solo la visibilità in un'applicazione hello feed.
   * Se è necessario tooisolate utenti dalle applicazioni, è necessario raccolte separate toouse a tale scopo.

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a>Come tooget cmdlet PowerShell di Azure RemoteApp
tootry hello nuove funzionalità di anteprima, sarà necessario toouse cmdlet di Azure PowerShell. Non è attualmente possibile toouse hello Azure tooenable portale hello nuova applicazione pubblicazione modalità di gestione.

In primo luogo, accertarsi di avere hello [modulo Azure PowerShell](/powershell/azure/overview) installato.

Avviare console di PowerShell hello in modalità amministratore e hello esecuzione seguente cmdlet:

        Add-AzureAccount

Verranno richiesti il nome utente e la password di Azure. Una volta effettuato l'accesso, sarà in grado di toorun i cmdlet di Azure RemoteApp contro le sottoscrizioni di Azure.

## <a name="how-toocheck-which-mode-a-collection-is-in"></a>Come toocheck quale modalità è in una raccolta
Eseguire hello seguente cmdlet:

        Get-AzureRemoteAppCollection <collectionName>

![Verificare la modalità di raccolta hello](./media/remoteapp-perapp/araacllelvel.png)

proprietà AclLevel Hello può avere hello seguenti valori:

* Raccolta: hello pubblicazione modalità originale. Tutti gli utenti vedono tutte le app pubblicate.
* Dell'applicazione: modalità hello nuova pubblicazione. Gli utenti vedono solo le app hello pubblicato direttamente toothem.

## <a name="how-tooswitch-tooapplication-publishing-mode"></a>La modalità di pubblicazione tooapplication tooswitch
Eseguire hello seguente cmdlet:

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

Stato di pubblicazione dell'applicazione verrà mantenuto: inizialmente tutti gli utenti visualizzino tutte le app pubblicate di hello originale.

## <a name="how-toolist-users-who-can-see-a-specific-application"></a>Come gli utenti toolist chi possono visualizzare un'applicazione specifica
Eseguire hello seguente cmdlet:

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Elenca tutti gli utenti possono vedere applicazione hello.

Nota: È possibile visualizzare gli alias dell'applicazione hello (denominati "alias app" nella sintassi hello) tramite l'esecuzione di Get-AzureRemoteAppProgram - NomeRaccolta <collectionName>.

## <a name="how-tooassign-an-application-tooa-user"></a>Come un utente dell'applicazione tooa tooassign
Eseguire hello seguente cmdlet:

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

utente Hello visualizzata applicazione hello nel client di Azure RemoteApp hello e sarà in grado di tooconnect tooit.

## <a name="how-tooremove-an-application-from-a-user"></a>Come tooremove un'applicazione da un utente
Eseguire hello seguente cmdlet:

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Inviare commenti e suggerimenti
Siamo lieti di ricevere commenti e suggerimenti su questa funzionalità in anteprima. Compilare hello [sondaggio](http://www.instant.ly/s/FDdrb) toolet ci sapere cosa ne pensi.

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a>Non ho avuto una funzionalità di anteprima di probabilità tootry hello?
Se non hanno partecipato in anteprima hello ancora, utilizzare questo [sondaggio](http://www.instant.ly/s/AY83p) toorequest accesso.

