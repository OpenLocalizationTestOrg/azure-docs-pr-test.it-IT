---
title: Eseguire la migrazione dall'autorizzazione del Servizio di controllo di accesso di Azure Active Directory all'autorizzazione con firma di accesso condiviso | Microsoft Docs
description: Eseguire la migrazione di applicazioni dal Servizio di controllo di accesso alla firma di accesso condiviso
services: service-bus-messaging
documentationcenter: 
author: clemensv
manager: timlt
editor: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2017
ms.author: sethm
ms.openlocfilehash: 7a2a55a6ad6a721a39c9f064aad817f841dd3235
ms.sourcegitcommit: 6f33adc568931edf91bfa96abbccf3719aa32041
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="migrate-from-azure-active-directory-access-control-service-to-shared-access-signature-authorization"></a>Eseguire la migrazione dall'autorizzazione del Servizio di controllo di accesso di Azure Active Directory all'autorizzazione con firma di accesso condiviso

Applicazioni di Service Bus sono stati precedentemente scegliere di usare due modelli di autorizzazione diversi: il [firma di accesso condiviso (SAS)](service-bus-sas.md) modello token forniti direttamente dal Bus di servizio e un modello di federazione in cui la gestione di le regole di autorizzazione presiede all'interno di [Azure Active Directory](/azure/active-directory/) token ottenuto da ACS e servizio Access Control (ACS) vengono passati al Bus di servizio per autorizzare l'accesso alle funzionalità desiderata.

Il modello di autorizzazione del Servizio di controllo di accesso è stato sostituito da tempo dall'[autorizzazione con firma di accesso condiviso](service-bus-authentication-and-authorization.md) come modello preferito e attualmente la documentazione, il materiale sussidiario e gli esempi usano l'autorizzazione con firma di accesso condiviso. Inoltre non è più possibile creare nuovi spazi dei nomi del bus di servizio associati al Servizio di controllo di accesso.

Il vantaggio della firma di accesso condiviso è che non dipende immediatamente da un altro servizio, ma può essere usata direttamente da un client senza intermediari fornendo l'accesso client al nome e alla chiave della regola della firma di accesso condiviso. La firma di accesso condiviso può anche essere facilmente integrata con un approccio in cui un client deve prima superare un controllo di autorizzazione con un altro servizio e quindi viene inviato un token. Il secondo approccio è simile al criterio di utilizzo del Servizio di controllo di accesso, ma abilita l'invio di token di accesso in base a condizioni specifiche dell'applicazione difficili da definire nel Servizio di controllo di accesso.

Per tutte le applicazioni esistenti che dipendono dal Servizio di controllo di accesso è particolarmente consigliabile che gli utenti eseguano la migrazione delle applicazioni in modo da usare la firma di accesso condiviso.

## <a name="migration-scenarios"></a>Scenari di migrazione

Il Servizio di controllo di accesso e il bus di servizio sono integrati tramite le informazioni condivise di *chiave di firma*. La chiave di firma viene usata da uno spazio dei nomi ACS per firmare i token di autorizzazione e dal bus di servizio per verificare che il token sia stato rilasciato dallo spazio dei nomi ACS associato. Lo spazio dei nomi ACS contiene le identità del servizio e le regole di autorizzazione. Le regole di autorizzazione definiscono quale identità del servizio o quale token rilasciato da un provider di identità esterno ottiene quale tipo di accesso a una parte del grafo dello spazio dei nomi del bus di servizio, sotto forma di corrispondenza di prefisso più lungo.

Ad esempio, una regola ACS può concedere l'attestazione di **invio** sul prefisso di percorso `/` a un'identità del servizio, ovvero un token rilasciato dal Servizio di controllo di accesso basato su questa regola concede i diritti client per l'invio a tutte le entità nello spazio dei nomi. Se il prefisso di percorso è `/abc`, l'identità può inviare solo a entità denominate `abc` o organizzate sotto questo prefisso. Si presuppone che i lettori di queste indicazioni sulla migrazione abbiano già familiarità con questi concetti.

Gli scenari di migrazione rientrano in tre ampie categorie:

1.  **Valori predefiniti non modificati**. Alcuni clienti usano un oggetto [SharedSecretTokenProvider](/dotnet/api/microsoft.servicebus.sharedsecrettokenprovider), passando l'identità del servizio e la relativa chiave privata del **proprietario** generate automaticamente per lo spazio dei nomi ACS, associato allo spazio dei nomi del bus di servizio, senza aggiungere nuove regole.

2.  **Identità del servizio personalizzate con regole semplici**. Alcuni clienti aggiungono nuove identità del servizio e concedono a ogni nuova identità del servizio le autorizzazioni di **invio**, **ascolto** e **gestione** per una specifica entità.

3.  **Identità del servizio personalizzate con regole complesse**. Un numero molto ridotto di clienti dispone di set di regole complesse, in cui i token rilasciati esternamente vengono mappati ai diritti sul servizio di inoltro o in cui a una singola identità del servizio vengono assegnati diritti differenziati su diversi percorsi dello spazio dei nomi tramite più regole.

Per assistenza sulla migrazione di set di regole complesse, è possibile contattare il [supporto tecnico di Azure](https://azure.microsoft.com/support/options/). Gli altri due scenari consentono una migrazione semplice.

### <a name="unchanged-defaults"></a>Valori predefiniti non modificati

Se l'applicazione non ha modificato i valori predefiniti del Servizio di controllo di accesso, è possibile sostituire tutte le occorrenze di [SharedSecretTokenProvider](/dotnet/api/microsoft.servicebus.sharedsecrettokenprovider) con un oggetto [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) e usare il valore **RootManageSharedAccessKey** preconfigurato dello spazio dei nomi anziché l'account **proprietario** del Servizio di controllo di accesso. Si noti che persino con l'account **proprietario** del Servizio di controllo di accesso, in genere questa configurazione non era e non è tuttora consigliata perché l'account/regola fornisce l'autorità di gestione completa sullo spazio dei nomi, inclusa l'autorizzazione ad eliminare eventuali entità.

### <a name="simple-rules"></a>Regole semplici

Se l'applicazione usa identità del servizio personalizzate con regole semplici, la migrazione è semplice nel caso in cui sia stata creata un'identità del servizio ACS per fornire il controllo di accesso su una coda specifica. Questo scenario si verifica spesso nel caso di soluzioni di tipo SaaS, in cui ogni coda viene usata come bridge a una succursale o a un sito tenant e l'identità del servizio viene creata per il sito specifico. In questo caso, è possibile migrare l'identità del servizio corrispondente a una regola di firma di accesso condiviso, direttamente sulla coda. Il nome dell'identità del servizio può diventare il nome della regola della firma di accesso condiviso e la chiave dell'identità del servizio può diventare la chiave della regola della firma di accesso condiviso. I diritti per la regola della firma di accesso condiviso vengono quindi configurati in modo equivalente alla regola ACS applicabile rispettivamente per l'entità.

È possibile eseguire questa nuova configurazione aggiuntiva della firma di accesso condiviso sul posto per qualsiasi spazio dei nomi esistente federato con il Servizio di controllo di accesso e la migrazione dal Servizio di controllo di accesso viene eseguita successivamente usando [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) invece di [SharedSecretTokenProvider](/dotnet/api/microsoft.servicebus.sharedsecrettokenprovider). Lo spazio dei nomi non deve essere necessariamente scollegato da ACS.

### <a name="complex-rules"></a>Regole complesse

Le regole della firma di accesso condiviso non sono concepite come account, ma sono chiavi di firma denominate associate a diritti. Di conseguenza, gli scenari in cui l'applicazione crea numerose identità del servizio e concede diritti di accesso per diverse entità o per l'intero spazio dei nomi richiedono comunque un intermediario per il rilascio di token. È possibile ottenere informazioni aggiuntive per un intermediario di questo tipo [contattando il supporto tecnico](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'autenticazione del bus di servizio, vedere gli argomenti seguenti:

* [Autenticazione e autorizzazione del bus di servizio](service-bus-authentication-and-authorization.md)
* [Autenticazione del bus di servizio con firme di accesso condiviso](service-bus-sas.md)
* [Dati fondamentali del bus di servizio](service-bus-fundamentals-hybrid-solutions.md)

