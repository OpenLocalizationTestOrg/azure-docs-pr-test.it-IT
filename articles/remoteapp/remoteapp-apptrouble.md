---
title: risoluzione dei problemi RemoteApp - aaaAzure errori di connessione e avvio dell'applicazione | Documenti Microsoft
description: Informazioni su come tootroubleshoot problemi con l'avvio e sulla connessione tooapplications in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Risoluzione dei problemi di Azure RemoteApp: Errori di connessione e avvio dell'applicazione
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Le applicazioni ospitate in Azure RemoteApp possono non riuscire toolaunch per diverse ragioni. Questo articolo vengono descritti vari motivi e messaggi di errore, gli utenti potrebbero ricevere quando si tenta di toolaunch applicazioni. Vengono affrontati anche gli errori di connessione (Ma in questo articolo non vengono descritti i problemi quando si accede a client di Azure RemoteApp hello).  

Continuare a leggere per informazioni sui messaggi di errore comuni a causa di errori di avvio e connessione tooapp.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>Messaggio analogo a "Configurazione in corso... Riprovare tra 10 minuti".
Questo errore indica che Azure RemoteApp è la scalabilità verticale toomeet hello capacità necessaria di utenti. In background hello vengono create più istanze di macchina virtuale di Azure RemoteApp esigenze di capacità hello toohandle degli utenti. Ciò in genere richiede circa cinque minuti ma può richiedere fino a too10 minuti. In alcuni casi, ciò non accade abbastanza rapidamente mentre c'è necessità immediata di risorse. Ad esempio alle 9.00 uno scenario in cui molti utenti necessario toouse l'app in Azure RemoteAppn nel hello contemporaneamente. In questo caso tooyou può essere abilitato **modalità capacità** su hello back-end. toodo questo aprire un ticket di supporto tecnico di Azure. Essere determinati tooinclude l'ID sottoscrizione nella richiesta di hello.  

![Messaggio analogo a "Configurazione in corso..."](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a>Impossibile riconnettersi automaticamente tooyour applicazioni riavviare l'applicazione
Questo messaggio di errore viene visualizzato spesso se si usa Azure RemoteApp e quindi inserire il toosleep PC più di 4 ore e quindi si è attivato nel computer e riconnettersi hello Azure RemoteApp client tentativo tooauto e superamento del timeout.  Indicare agli utenti toonavigate toohello indietro applicazione e tentare di tooopen dal client di Azure RemoteApp hello.

![Impossibile riconnettersi automaticamente tooyour applicazioni](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a>Problemi con profili temporanei hello
Questo errore si verifica quando il profilo utente (disco) non è stato possibile toomount e utente hello riceve un profilo temporaneo.  Gli amministratori devono passare insieme toohello hello portale di Azure e quindi passare toohello **sessioni** scheda e tentare troppo**Disconnetti** utente hello. Questo verrà impone una sessione utente hello - la disconnessione completa quindi avere hello utente tentativo toolaunch nuovamente un'app. Se il problema persiste, contattare il supporto tecnico di Azure.

## <a name="azure-remoteapp-has-stopped-working"></a>Azure RemoteApp ha smesso di funzionare
Questo messaggio di errore client di Azure RemoteApp di hello è verificato un problema ed è necessario riavviare toobe. Istruire gli utenti tooclose: selezionare **Chiudi programma** e quindi avviare nuovamente il client di Azure RemoteApp hello.  Se il problema di hello open e ticket di supporto di Azure.

![Azure RemoteApp ha smesso di funzionare](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a>Si è verificato un errore durante l'accesso di Connessione Desktop remoto alla risorsa. Tentare la connessione a hello o contattare l'amministratore di sistema
Si tratta di un messaggio di errore generico. Contattate il supporto tecnico di Azure. 

![Messaggio generico di Azure RemoteApp](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

