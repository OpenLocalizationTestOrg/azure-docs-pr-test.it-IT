---
title: "aaaConfigure Azure MFA Server per la disponibilità elevata | Documenti Microsoft"
description: "Distribuire più istanze del server Microsoft Azure Multi-Factor Authentication in configurazioni che offrono disponibilità elevata."
services: multi-factor-authentication
keywords: Azure MFA,
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 8c6b1921c734c7a7273e443b3591fbbb15cd5e6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-high-availability"></a>Configurare il server Azure MFA per la disponibilità elevata

tooachieve a disponibilità elevata con la distribuzione di Azure MFA Server, è necessario toodeploy più server di autenticazione a più fattori. In questa sezione vengono fornite informazioni su tooachieve una progettazione con bilanciamento del carico le destinazioni di disponibilità elevata nella distribuzione di Azure MFS Server.

## <a name="mfa-server-overview"></a>Panoramica del server MFA

come illustrato nel seguente diagramma hello Hello architettura del servizio Azure MFA Server è costituito da diversi componenti:

 ![Architettura del server MFA](./media/mfa-server-high-availability/mfa-ha-architecture.png)

Un Server di autenticazione a più fattori è un Server di Windows a cui è installato software di hello Azure multi-Factor Authentication. istanza del Server di autenticazione a più fattori Hello deve essere attivato da hello del servizio di autenticazione a più fattori in Azure toofunction. È possibile installare più di un server MFA locale.

primo Server di autenticazione a più fattori che è installato è Hello hello Server master di autenticazione a più fattori per l'attivazione da hello servizio di autenticazione a più fattori di Azure per impostazione predefinita. server MFA master Hello è una copia del database PhoneFactor.pfdata hello scrivibile. Le installazioni successive delle istanze del server MFA sono note con il nome di slave. server secondari di autenticazione a più fattori Hello dispongono di una copia replicata di sola lettura del database PhoneFactor.pfdata hello. I server MFA replicano le informazioni mediante Remote Procedure Call (RPC). Tutti i server, autenticazione a più fattori collettivamente possono essere aggiunti a un dominio o autonomo tooreplicate informazioni.

Schema di autenticazione a più fattori sia slave MFA server comunicano con hello del servizio di autenticazione a più fattori quando è necessaria l'autenticazione a due fattori. Ad esempio, quando un utente tenta l'applicazione di tooan accesso toogain che richiede l'autenticazione a due fattori, utente hello prima essere autenticati da un provider di identità, ad esempio Active Directory (AD).

Dopo l'autenticazione con Active Directory, hello Server MFA comunicherà con il servizio di autenticazione a più fattori hello. Hello MFA Server è in attesa di notifiche da tooallow servizio di autenticazione a più fattori hello o negare un'applicazione hello utente accesso toohello.

Se il server master di autenticazione a più fattori hello è offline, le autenticazioni possono comunque essere elaborate, ma non è possibile elaborare le operazioni che richiedono modifiche toohello MFA database. (Alcuni esempi: hello aggiunta di utenti self-service modifiche PIN e la modifica delle informazioni utente)

## <a name="deployment"></a>Distribuzione

Prendere in considerazione hello seguenti punti importanti per il bilanciamento del carico di Azure MFA Server e i componenti correlati.

* **Usando la disponibilità elevata di RADIUS standard tooachieve**. Se si usano server Azure MFA come server RADIUS, è possibile configurare un server MFA come destinazione di autenticazione RADIUS primaria e altri server Azure MFA come destinazioni di autenticazione secondarie. Tuttavia, disponibilità elevata di tooachieve questo metodo potrebbe non essere pratica perché è necessario attendere un toooccur periodo di timeout quando l'autenticazione ha esito negativo nella destinazione di autenticazione principale hello prima che possa essere autenticato con l'autenticazione secondaria hello destinazione. È più efficiente tooload saldo hello traffico RADIUS tra client RADIUS hello e server RADIUS hello (in questo caso, hello Azure MFA server funge da server RADIUS) in modo che è possibile configurare client RADIUS hello con un singolo URL che puntano a.
* **È necessario toomanually alzare di livello server secondari MFA**. Se il server Azure MFA master di hello è offline, hello Azure MFA server secondari continuano tooprocess le richieste di autenticazione a più fattori. Tuttavia, fino a quando non è disponibile un server master di autenticazione a più fattori, gli amministratori non possono aggiungere utenti o modificare le impostazioni di autenticazione a più fattori e gli utenti non possono apportare modifiche tramite il portale utenti hello. La promozione di un ruolo di master toohello slave dell'autenticazione a più fattori è sempre un processo manuale.
* **Separabilità dei componenti**. Hello Azure MFA Server è costituito da diversi componenti che possono essere installati hello stessa istanza del Server di Windows o in istanze diverse. Questi componenti includono hello portale per gli utenti e servizio Web App Mobile adattatore ADFS hello (agente). Questo separability rende possibili toouse hello Proxy applicazione Web toopublish hello portale per gli utenti e Server Web di App Mobile dalla rete perimetrale hello. Questo tipo di configurazione aggiunge toohello sicurezza complessiva di progettazione, come illustrato nel seguente diagramma hello. Hello portale per gli utenti autenticazione a più fattori e il Server Web di App mobili possono essere distribuiti anche in configurazioni con bilanciamento del carico a disponibilità elevata.

   ![Server MFA con una rete perimetrale](./media/mfa-server-high-availability/mfasecurity.png)

* **Password monouso (OTP) con SMS (noto anche come unidirezionale SMS) richiede l'utilizzo di hello di sessioni permanenti se il traffico con bilanciamento del carico**. SMS unidirezionali è un'opzione di autenticazione che fa sì che gli utenti di hello hello Server MFA toosend un messaggio di testo contenente un OTP. Hello immessi hello OTP in un hello toocomplete finestra prompt dei comandi richiesta di autenticazione a più fattori. Se il server di autenticazione a più fattori di Azure di bilanciamento del carico, hello stesso server che ha gestito la richiesta di autenticazione iniziale hello deve essere hello server che riceve il messaggio OTP hello da utente hello. Se un altro Server di autenticazione a più fattori riceve hello risposta OTP, la richiesta di autenticazione hello ha esito negativo. Per ulteriori informazioni, vedere [Password per una tramite SMS aggiunti tooAzure Server MFA](https://blogs.technet.microsoft.com/enterprisemobility/2015/03/02/one-time-password-over-sms-added-to-azure-mfa-server).
* **Distribuzioni di bilanciamento del carico di hello portale per gli utenti e servizio Web App Mobile richiedano le sessioni permanenti**. In caso di bilanciamento del carico hello portale per gli utenti autenticazione a più fattori e hello servizio Web App Mobile, ogni sessione deve toostay su hello nello stesso server.

## <a name="high-availability-deployment"></a>Distribuzione a disponibilità elevata

Hello seguente è illustrata un'implementazione completa di bilanciamento del carico a disponibilità elevata di Azure MFA e i relativi componenti, insieme ad FS per riferimento.

 ![Implementazione a disponibilità elevata del server Azure MFA](./media/mfa-server-high-availability/mfa-ha-deployment.png)

Si noti hello seguenti elementi per area hello conseguentemente numerato di hello precedente diagramma.

1. sono due server di autenticazione a più fattori di Azure (MFA1 e MFA2) Hello carico bilanciato (mfaapp.contoso.com) e sono toouse configurato un database di PhoneFactor.pfdata hello tooreplicate (4443) porta statica. Hello Web Service SDK sia installato in ogni di comunicazione di hello Server MFA tooenable sulla porta TCP 443 con i server ADFS hello. i server di autenticazione a più fattori Hello vengono distribuiti in una configurazione con bilanciamento del carico senza stata. Tuttavia, se si desidera toouse OTP SMS, è necessario utilizzare il bilanciamento del carico con stato.
   ![Server Azure MFA - Elevata disponibilità del server app](./media/mfa-server-high-availability/mfaapp.png)

   > [!NOTE]
   > Poiché RPC utilizza porte dinamiche, è consigliabile non tooopen firewall backup toohello intervallo di porte dinamiche RPC può comportare l'utilizzo. Se si dispone di un firewall **tra** server di applicazioni di autenticazione a più fattori, è necessario configurare l'hello Server MFA toocommunicate di su una porta statica per hello il traffico di replica tra server master e secondari e aprire la porta nel firewall. È possibile forzare la porta statica hello mediante la creazione di un valore del Registro di sistema DWORD in ```HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Positive Networks\PhoneFactor``` chiamato ```Pfsvc_ncan_ip_tcp_port``` e impostare il valore di hello tooan porta statica. Le connessioni sono sempre avviate dal master toohello di hello slave server MFA, la porta statica hello è necessaria solo per master hello, ma poiché è possibile alzare di livello un master di hello toobe slave in qualsiasi momento, è necessario impostare la porta statica hello in tutti i server di autenticazione a più fattori.

2. server di App per dispositivi mobili/MFA del portale utente Hello due (MAS1-accesso-autenticazione a più fattori e autenticazione a più fattori-UP-MAS2) sono il bilanciamento del carico un **stateful** configurazione (mfa.contoso.com). Tenere presente che le sessioni permanenti sono un requisito necessario per il bilanciamento del carico hello portale autenticazione a più fattori per gli utenti e servizio App per dispositivi mobili.
   ![Server Azure MFA - Disponibilità elevata per il portale per gli utenti e per il servizio per app per dispositivi mobili](./media/mfa-server-high-availability/mfaportal.png)
3. farm di Server ADFS Hello è bilanciamento del carico e pubblicato toohello Internet tramite proxy ADFS con bilanciamento del carico nella rete perimetrale hello. Ogni Server ADFS utilizza hello ADFS agente toocommunicate con hello Azure MFA server tramite un URL di singolo con bilanciamento del carico (mfaapp.contoso.com) sulla porta TCP 443.

## <a name="next-steps"></a>Passaggi successivi

* [Installare e configurare il server Azure MFA](multi-factor-authentication-get-started-server.md)
