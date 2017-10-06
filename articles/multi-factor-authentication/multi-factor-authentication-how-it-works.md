---
title: aaaAzure multi-Factor Authentication - funzionamento
description: "Azure multi-Factor Authentication consente di salvaguardare accesso toodata e applicazioni rispettando richiesta dell'utente per un semplice processo. Offre ulteriore sicurezza richiedendo una seconda forma di autenticazione nonché un'autenticazione avanzata tramite una gamma di opzioni di verifica semplice."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a>Come funziona Azure Multi-Factor Authentication
sicurezza di Hello di verifica in due passaggi è compresa nel suo approccio a più livelli. La manomissione di più fattori rappresenta una sfida significativa per gli autori di attacchi. Anche se un utente malintenzionato riesce toolearn hello password utente, è inutile senza anche in possesso del dispositivo attendibile hello. 

![Verifica](./media/multi-factor-authentication-how-it-works/howitworks.png)

Azure multi-Factor Authentication consente di salvaguardare accesso toodata e applicazioni rispettando richiesta dell'utente per un semplice processo.  Offre ulteriore sicurezza richiedendo una seconda forma di autenticazione nonché un'autenticazione avanzata tramite una gamma di opzioni di verifica semplice.


## <a name="methods-available-for-two-step-verification"></a>Metodi disponibili per la verifica in due passaggi
Quando un utente accede, una verifica aggiuntiva viene inviata toohello utente.  di seguito Hello sono un elenco di metodi che può essere utilizzato per la verifica di secondo.

| Metodo di verifica | Descrizione |
| --- | --- |
| Chiamata telefonica |Telefono registrato tooa dell'utente viene effettuata una chiamata. utente Hello immette un PIN, se necessario, quindi preme # hello. |
| SMS |Il telefono cellulare dell'utente tooa con un codice a sei cifre viene inviato un messaggio di testo. Questo codice Hello immessi nella pagina di accesso hello. |
| Notifica dell'app per dispositivi mobili |Smartphone dell'utente tooa viene inviata una richiesta di verifica. Hello utente immette il PIN, se necessario, quindi seleziona **verificare** su hello app per dispositivi mobili. |
| Codice di verifica dell'app per dispositivi mobili |Hello app per dispositivi mobili, che è in esecuzione Smartphone dell'utente, viene visualizzato un codice di verifica che le modifiche apportate a ogni 30 secondi. utente Hello Trova codice più recente di hello e lo inserisce nella pagina di accesso hello. |
| Token OATH di terze parti | Server di Azure multi-Factor Authentication può essere configurato tooaccept metodi di verifica di terze parti. |

Azure multi-Factor Authentication fornisce metodi di verifica selezionabili per cloud e server. È possibile scegliere i metodi disponibili per gli utenti: telefonata, SMS, notifica dell'app o codici dell'app. Per altre informazioni, vedere i [metodi di verifica selezionabili](multi-factor-authentication-whats-next.md#selectable-verification-methods).

## <a name="next-steps"></a>Passaggi successivi

- Informazioni sulle diversa hello [versioni e i metodi di utilizzo per Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md)

- Scegliere se toodeploy Azure MFA [in locale o cloud hello](multi-factor-authentication-get-started.md)

- Risposte alle [Domande frequenti](multi-factor-authentication-faq.md)