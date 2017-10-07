---
title: "aaaRDG e Server di autenticazione a più fattori di Azure tramite RADIUS | Documenti Microsoft"
description: Si tratta hello Azure multi-factor authentication pagina di supporto nella distribuzione di Gateway Desktop remoto (desktop remoto) e il Server Azure multi-Factor Authentication tramite RADIUS.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fd280e9b6ff90c82927cffe593c4f1fda7047842
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a>Gateway Desktop remoto e server Azure Multi-Factor Authentication utilizzando RADIUS
Spesso, Gateway Desktop remoto (desktop remoto) utilizza hello locale servizi (criteri di rete) tooauthenticate utenti. In questo articolo viene descritto come tooroute RADIUS richiede hello Gateway Desktop remoto (tramite hello dei criteri di rete locale) toohello Server multi-Factor Authentication. Hello combinazione di Azure MFA e Gateway Desktop remoto significa che gli utenti possono accedere gli ambienti di lavoro da qualsiasi posizione durante l'esecuzione dell'autenticazione avanzata. 

Poiché l'autenticazione di Windows per Servizi terminal non è supportato per Server 2012 R2, è possibile utilizzare toointegrate RADIUS e Gateway Desktop remoto con Server di autenticazione a più fattori. 

Installare hello del Server Azure multi-Factor Authentication in un server distinto, quali proxy RADIUS hello richiesta nuovamente toohello dei criteri di rete su hello Server Gateway Desktop remoto. Una volta NPS convalida hello username e password, restituisce un toohello di risposta Server multi-Factor Authentication. Quindi, hello Server MFA esegue secondo fattore di autenticazione di hello e restituisce un gateway toohello risultato.

## <a name="prerequisites"></a>Prerequisiti

- Un server MFA di Azure aggiunto a un dominio. Se non si dispone di uno già installato, attenersi alla procedura hello in [introduzione hello del Server Azure multi-Factor Authentication](multi-factor-authentication-get-started-server.md).
- Un'istanza di Gateway Desktop remoto che esegue l'autenticazione con il server dei criteri di rete.

## <a name="configure-hello-remote-desktop-gateway"></a>Configurare hello Gateway Desktop remoto
Configurare hello Gateway Desktop remoto toosend RADIUS autenticazione tooan Server Azure multi-Factor Authentication. 

1. In Gestione Gateway Desktop remoto, il nome di server hello e scegliere **proprietà**.
2. Passare toohello **archivio per desktop remoto** e selezionare **server centrale,**. 
3. Aggiungere uno o più server di autenticazione a più fattori di Azure come server RADIUS, immettere il nome di hello o indirizzo IP di ogni server. 
4. Creare un segreto condiviso per ogni server.

## <a name="configure-nps"></a>Configurazione dei criteri di rete
Hello Gateway Desktop remoto utilizza criteri di rete toosend hello RADIUS richiesta tooAzure multi-Factor Authentication. tooconfigure dei criteri di rete, prima è modificare le impostazioni di timeout hello tooprevent hello Gateway Desktop remoto dal timeout prima del completamento di verifica in due passaggi hello. È quindi possibile aggiornare le autenticazioni RADIUS tooreceive di criteri di rete dal Server di autenticazione a più fattori. Utilizzare hello procedure tooconfigure dei criteri di rete seguenti:

### <a name="modify-hello-timeout-policy"></a>Modificare i criteri di timeout hello

1. In Criteri di rete, aprire hello **client e Server RADIUS** dal menu a sinistra di colonna e selezionare hello **gruppi di Server RADIUS remoti**. 
2. Seleziona hello **gruppo del SERVER GATEWAY Servizi terminal**. 
3. Passare toohello **il bilanciamento del carico** scheda. 
4. Modificare entrambi hello **numero di secondi senza risposta prima che la richiesta venga annullata** hello e **numero di secondi tra le richieste quando il server viene identificato come non disponibile** toobetween 30 e 60 secondi. (Se si ritiene che il server hello scade ancora durante l'autenticazione, è possibile tornare a questa schermata e aumentare hello numero di secondi.)
5. Passare toohello **/Account di autenticazione** scheda e verificare che le porte RADIUS hello specificato corrispondenza hello porte che hello Server multi-Factor Authentication è in ascolto.

### <a name="prepare-nps-tooreceive-authentications-from-hello-mfa-server"></a>Preparare le autenticazioni tooreceive dei criteri di rete dal Server di autenticazione a più fattori hello

1. Fare doppio clic su **client RADIUS** in client RADIUS e server in a sinistra di colonna e selezionare hello **New**.
2. Aggiungere hello del Server Azure multi-Factor Authentication come client RADIUS. Scegliere un nome descrittivo e specificare un segreto condiviso.
3. Aprire hello **criteri** dal menu a sinistra di colonna e selezionare hello **criteri richiesta di connessione**. Verrà visualizzato un criterio denominato TS GATEWAY AUTHORIZATION POLICY, creato durante la configurazione di Gateway Desktop remoto. Questo criterio inoltra le richieste RADIUS toohello Server multi-Factor Authentication.
4. Fare clic con il pulsante destro del mouse su **TS GATEWAY AUTHORIZATION POLICY** e scegliere **Duplica criterio**. 
5. Aprire hello nuovi criteri e passare toohello **condizioni** scheda.
6. Aggiungere una condizione corrispondente al nome descrittivo del Client con il nome descrittivo di hello impostato nel passaggio 2 per client RADIUS del Server Azure multi-Factor Authentication hello hello. 
7. Passare toohello **impostazioni** e selezionare **autenticazione**.
8. Modificare anche i Provider di autenticazione hello**autenticare le richieste in questo server**. Questo criterio assicura che quando dei criteri di rete riceve una richiesta RADIUS dal Server di autenticazione a più fattori di Azure hello, hello autenticazione viene eseguita localmente anziché inviare un raggio richiesta indietro toohello Azure multi-Factor Authentication Server, con la conseguenza di una condizione di ciclo. 
9. tooprevent una condizione di ciclo, assicurarsi che il nuovo criterio di hello è ordinato sopra criterio originale di hello in hello **criteri richiesta di connessione** riquadro.

## <a name="configure-azure-multi-factor-authentication"></a>Configurazione di Azure Multi-Factor Authentication

Hello del Server Azure multi-Factor Authentication è configurato come proxy RADIUS tra Gateway Desktop remoto e dei criteri di rete.  È necessario installarlo in un server di dominio che è distinto dal server Gateway Desktop remoto hello. Utilizzare hello seguente hello tooconfigure procedure del Server Azure multi-Factor Authentication.

1. Scegliere sull'icona autenticazione RADIUS hello hello del Server Azure multi-Factor Authentication. 
2. Controllare hello **Abilita autenticazione RADIUS** casella di controllo.
3. Nella scheda client hello, verificare che le porte hello corrispondano a quelle configurate in Criteri di rete, quindi selezionare **Aggiungi**.
4. Aggiungere l'indirizzo IP del server Gateway Desktop remoto hello, nome dell'applicazione (facoltativo) e un segreto condiviso. Hello shared secret esigenze toobe hello stesso sul Server Azure multi-Factor Authentication hello e Gateway Desktop remoto.
3. Passare toohello **destinazione** scheda e seleziona hello **server RADIUS** pulsante di opzione.
4. Selezionare **Aggiungi** e immettere l'indirizzo IP hello segreto condiviso e porte del server dei criteri di rete hello. A meno che non utilizza una rete centrale, sono hello stesso hello client RADIUS e destinazione RADIUS. segreto condiviso Hello deve corrispondere a quello impostato di hello nella sezione client RADIUS del server dei criteri di rete hello hello.

![Autenticazione RADIUS](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a>Passaggi successivi

- Integrare Azure MFA e [app Web IIS](multi-factor-authentication-get-started-server-iis.md)

- Ottenere le risposte in hello [domande frequenti di Azure multi-Factor Authentication](multi-factor-authentication-faq.md)
