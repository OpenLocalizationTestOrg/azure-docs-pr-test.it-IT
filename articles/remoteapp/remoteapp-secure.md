---
title: aaaSecure App e risorse in Azure RemoteApp | Documenti Microsoft
description: Informazioni su come toolock all'App e risorse in Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 26325826e92855a12a0087f19a3e32cbe1116449
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Applicazioni protette e risorse in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Azure RemoteApp consente agli utenti l'accesso gestito toocentrally app di Windows, che consente di controllare ciò che gli utenti possono e non possono eseguire.  Questo è particolarmente utile quando l'utente hello connessione da un dispositivo non gestito (ad esempio, i relativi Macbook personali) e si desidera l'accesso utente hello toocontrol o esperienza.

Ad esempio, se si utilizza Active Directory per l'autenticazione utente e si desidera tooprevent agli utenti di copiare dati da un'app, è possibile configurare un utenti tooblock criteri di gruppo Desktop remoto dalla copia di dati.

Un altro esempio è se si desidera che l'accesso a internet tooblock per una particolare app nella raccolta. È possibile creare una regola Windows Firewall che blocchi hello accesso quando si crea l'immagine di hello per la raccolta.

## <a name="implementation-options"></a>Opzioni di implementazione
  Ecco le opzioni di implementazione della chiave hello, che possono essere utilizzate singolarmente o insieme in base alle esigenze:

1. Se la raccolta RemoteApp è aggiunto a un dominio è possibile applicare qualsiasi [criteri di gruppo](https://technet.microsoft.com/library/cc725828.aspx) (con eccezione hello di hello inattivo e Disconnect timeout criteri descritti [qui](../azure-subscription-service-limits.md)).
2. È possibile configurare un criterio (se la raccolta non è aggiunto a un dominio oppure non si dispone di privilegi appropriati hello in Active Directory) di tooGroup alternativo, [criteri locali](https://technet.microsoft.com/library/cc775702.aspx) nell'immagine modello.  Si noti che Criteri di gruppo si sovrascrivono ai criteri locali quando si verifica un conflitto.
3. Alcune impostazioni del sistema operativo o app non sono configurabili tramite criteri, ma può essere tramite una chiave del Registro di sistema utilizzando hello [strumento RegEdit](remoteapp-hybridtrouble.md) durante la configurazione dell'immagine modello.
4. È possibile utilizzare [Windows Firewall](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) tooand di accesso di rete toocontrol dalla macchina di hello in cui è in esecuzione l'applicazione hello. Assicurarsi che non viene bloccata hello URL e le porte definite qui.
5. È possibile utilizzare [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) toocontrol agli utenti di applicazioni e i file eseguibili. Ad esempio, gli utenti esperti possono scoprire come toorun le applicazioni che non ha pubblicato, ma che sono disponibili in hello immagine è stato utilizzato toocreate hello insieme - AppLocker può bloccare questo.

## <a name="detailed-information"></a>Informazioni dettagliate
* Hello seguenti criteri di servizi desktop remoto è probabilmente toobe utili:
  * [Reindirizzamento di Dispositivi e risorse](https://technet.microsoft.com/library/ee791794.aspx)
  * [Reindirizzamento della stampante](https://technet.microsoft.com/library/ee791784.aspx)
  * [Profili](https://technet.microsoft.com/library/ee791865.aspx).
* Si noti che la configurazione reindirizzamenti tramite hello modulo PowerShell di RemoteApp (come illustrato [qui](remoteapp-redirection.md)) si basa su hello macchina tooenforce hello dei criteri client, quindi è opportuno se la sicurezza è l'obiettivo principale di hello criteri hello tooenforce tramite Hello criteri dei modelli immagine locale o tramite criteri di gruppo.
* [Criteri di Windows Server 2012 R2](https://technet.microsoft.com/library/hh831791.aspx).
* [Criteri di Office 2013](https://technet.microsoft.com/library/cc178969.aspx) (inclusi [come toocustomize hello sulla barra degli strumenti di Office](https://technet.microsoft.com/library/cc179143.aspx)).

