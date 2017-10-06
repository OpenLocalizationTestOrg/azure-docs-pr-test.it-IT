---
title: "aaaRADIUS l'autenticazione e Server di autenticazione a più fattori di Azure | Documenti Microsoft"
description: Si tratta hello Azure multi-factor authentication pagina di supporto nella distribuzione dell'autenticazione RADIUS e Server Azure multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>Integrare l'autenticazione con il server Azure Multi-Factor Authentication
Utilizzare sezione autenticazione RADIUS hello di Azure MFA Server tooenable e configurare l'autenticazione RADIUS. RADIUS è uno standard del protocollo tooaccept le richieste di autenticazione e tooprocess tali richieste. Hello del Server Azure multi-Factor Authentication funge da server RADIUS. Inserire tra il client RADIUS (accessorio VPN) e la destinazione di autenticazione, potrebbe essere Active Directory (AD), una directory LDAP o un altro tooadd di server RADIUS Azure multi-Factor Authentication. Per toofunction Azure multi-Factor Authentication (MFA), è necessario configurare Azure MFA Server hello in modo che possa comunicare con i server client hello sia la destinazione di autenticazione hello. Hello Azure MFA Server accetta richieste da un client RADIUS, convalida le credenziali rispetto hello destinazione di autenticazione, aggiunge Azure multi-Factor Authentication e invia un client RADIUS toohello indietro di risposta. richiesta di autenticazione Hello ha esito positivo solo se l'esito positivo sia l'autenticazione principale hello e hello Azure multi-Factor Authentication.

> [!NOTE]
> Hello MFA Server supporta solo PAP (protocollo di autenticazione di password) e MSCHAPv2 (Microsoft Challenge Handshake Authentication Protocol) RADIUS protocolli quando funge da server RADIUS.  Altri protocolli, come EAP (extensible autenticazione), possono essere utilizzati quando server MFA hello funge da server RADIUS tooanother proxy RADIUS che supporti tale protocollo.
>
> In questa configurazione, token OATH e di SMS unidirezionali non funzionano perché hello MFA Server non può avviare una risposta corretta di verifica RADIUS utilizzando un protocolli alternativo.

![Autenticazione RADIUS](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>Aggiungere un client RADIUS
tooconfigure l'autenticazione RADIUS, installare hello del Server Azure multi-Factor Authentication in un server Windows. Se si dispone di un ambiente Active Directory, server hello deve essere toohello aggiunti a un dominio all'interno di rete hello. Utilizzare hello seguente hello tooconfigure procedure del Server Azure multi-Factor Authentication:

1. In hello del Server Azure multi-Factor Authentication, fare clic sull'icona autenticazione RADIUS hello nel menu a sinistra di hello.
2. Controllare hello **Abilita autenticazione RADIUS** casella di controllo.
3. Nella scheda client hello modificare hello autenticazione e porte di Accounting se hello servizio RADIUS di autenticazione a più fattori di Azure deve toolisten per le richieste RADIUS su porte non standard.
4. Fare clic su **Aggiungi**.
5. Immettere l'indirizzo IP hello di hello accessorio o del server che eseguirà l'autenticazione toohello Server Azure multi-Factor Authentication, il nome di un'applicazione (facoltativo) e un segreto condiviso.

  nome dell'applicazione Hello viene visualizzato nei report di Azure multi-Factor Authentication e potrebbe essere visualizzato all'interno di messaggi di autenticazione SMS o App per dispositivi mobili.

  Hello condivisa hello toobe esigenze secret stesso per entrambi hello del Server Azure multi-Factor Authentication e accessorio o del server.

6. Controllare hello **corrispondenza utente di multi-Factor Authentication richiedono** se tutti gli utenti sono stati o verranno importati nel Server hello e soggetto toomulti-factor authentication. Se un numero significativo di utenti non è ancora stato importato nel Server hello e/o esenti da verifica in due passaggi, lasciare deselezionata la casella hello.
7. Controllare hello **token OATH di fallback Enable** casella se si desiderano i passcode OATH toouse dalle App per dispositivi mobili di verifica come una fallback toohello out of band telefonata, SMS o notifica push.
8. Fare clic su **OK**.

Ripetere i passaggi da 4 a 8 tooadd come molti altri client RADIUS in base alle esigenze.

## <a name="configure-your-radius-client"></a>Configurare il client RADIUS

1. Fare clic su hello **destinazione** scheda.
2. Se hello Azure MFA Server è installato in un server di dominio in un ambiente Active Directory, selezionare il dominio di Windows.
3. Se gli utenti devono essere autenticati in una directory LDAP, selezionare **Binding LDAP**.

  toouse binding LDAP, fare clic sull'icona integrazione Directory hello e modifica configurazione LDAP hello nella scheda Impostazioni hello in modo che hello Server può associare tooyour directory. È possibile trovare istruzioni per la configurazione LDAP in hello [Guida alla configurazione di Proxy LDAP](multi-factor-authentication-get-started-server-ldap.md).

4. Se gli utenti devono essere autenticati in un altro server RADIUS, selezionare il/i server RADIUS.
5. Fare clic su **Aggiungi** richiede tooconfigure hello toowhich hello Azure MFA Server verrà proxy messaggi hello del server RADIUS.
6. Nella finestra di dialogo Aggiungi Server RADIUS di hello, immettere l'indirizzo IP di hello del server RADIUS hello e un segreto condiviso.

  Hello condivisa hello toobe esigenze secret stesso per entrambi hello del Server Azure multi-Factor Authentication e server RADIUS. Se vengono utilizzate porte diverse da server RADIUS hello, modificare la porta di autenticazione hello e porta di Accounting.

7. Fare clic su **OK**.
8. Aggiungere hello Azure MFA Server come client RADIUS in hello altri server RADIUS in modo che sia possibile elaborare le richieste di accesso inviate tooit da hello Azure MFA Server. Utilizzare hello che stesso condivisa segreto configurato nel Server Azure multi-Factor Authentication hello.

Ripetere questi passaggi tooadd più server RADIUS e configurare hello ordine in cui hello Azure MFA Server verranno interrogati li con hello **Sposta su** e **Sposta giù** pulsanti.

Configurazione del Server Azure multi-Factor Authentication hello è stata completata. Hello Server ora è in ascolto sulle porte configurata hello per le richieste di accesso RADIUS dai client hello configurato.   

## <a name="radius-client-configuration"></a>Configurazione del client RADIUS
tooconfigure hello client RADIUS, attenersi alle linee guida di hello:

* Configurare il tooauthenticate accessorio o del server tramite indirizzo IP toohello Azure multi-Factor Authentication del Server RADIUS, che fungerà da server RADIUS hello.
* Utilizzare hello che stesso condivisa segreto che è stato configurato in precedenza.
* Configurare hello RADIUS timeout too30-60 secondi, in modo che vi sia tempo toovalidate hello le credenziali utente, eseguire la verifica in due passaggi, ricevere la risposta e quindi rispondere toohello richiesta di accesso RADIUS.
