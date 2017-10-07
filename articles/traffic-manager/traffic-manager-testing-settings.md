---
title: le impostazioni di gestione traffico di Azure aaaVerify | Documenti Microsoft
description: Questo articolo contiene le informazioni necessarie per verificare le impostazioni di Gestione traffico.
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a>Verificare le impostazioni di Gestione traffico

tootest le impostazioni di gestione traffico, è necessario toohave più client, in varie posizioni, da cui è possibile eseguire i test. Quindi, connettere gli endpoint hello nel profilo di Traffic Manager, uno alla volta.

* Impostare bassa hello valore TTL del DNS in modo che le modifiche vengono propagate rapidamente (ad esempio, 30 secondi).
* Conoscere gli indirizzi IP di servizi cloud di Azure e siti Web nel profilo hello che si esegue il test di hello.
* Utilizzare gli strumenti che consentono di risolvere un indirizzo IP tooan del nome DNS e visualizzazione tale indirizzo.

Si stanno archiviando toosee che i nomi DNS hello risolvere tooIP indirizzi degli endpoint di hello nel profilo. risoluzione nomi Hello deve essere coerente con metodo di routing del traffico hello definito nel profilo di gestione traffico hello. È possibile utilizzare strumenti hello come **nslookup** o **esaminare** tooresolve i nomi DNS.

Hello negli esempi seguenti consentono di testare il profilo di Traffic Manager.

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a>Controllare il profilo di Gestione traffico in Windows con nslookup e ipconfig

1. Aprire un comando o prompt Windows PowerShell come amministratore.
2. Tipo `ipconfig /flushdns` tooflush hello cache del resolver DNS.
3. Digitare `nslookup <your Traffic Manager domain name>`. Ad esempio, hello comando controlli hello nome di dominio con prefisso hello seguente *myapp.contoso*

        nslookup myapp.contoso.trafficmanager.net

    Un risultato tipico Mostra hello le seguenti informazioni:

    + Hello nome DNS e indirizzo IP del server DNS di hello viene accessibili tooresolve questo nome di dominio di Traffic Manager.
    + nome di dominio di Traffic Manager Hello digitato nella riga di comando hello dopo "nslookup" e il dominio di Traffic Manager hello hello IP indirizzo toowhich viene risolto. secondo indirizzo IP di Hello è un toocheck importante hello. Deve corrispondere a un pubblico indirizzo IP virtuale (VIP) per uno dei servizi cloud hello o siti Web inclusi nel profilo di Traffic Manager si sta testando hello.

## <a name="how-tootest-hello-failover-traffic-routing-method"></a>Come metodo di routing del traffico tootest hello failover

1. Lasciare tutti gli endpoint attivi.
2. Usando un unico client, richiedere la risoluzione DNS per il nome di dominio aziendale mediante nslookup o un'utilità simile.
3. Assicurarsi che hello risolto l'indirizzo IP corrispondente endpoint primario hello.
4. Arrestare l'endpoint primario oppure rimuovere hello monitoraggio file in modo che Traffic Manager presume che l'applicazione hello è inattivo.
5. Attendere hello DNS Time-to-Live (TTL) del profilo di Traffic Manager hello più altri due minuti. Ad esempio, se la durata TTL del DNS è 300 secondi (5 minuti), è necessario attendere sette minuti.
6. Scaricare la cache del client DNS e richiedere una risoluzione DNS usando nslookup. In Windows, è possibile scaricare la cache DNS con il comando hello ipconfig /flushdns.
7. Assicurarsi che hello risolto l'indirizzo IP individua l'endpoint secondario.
8. Ripetere il processo hello, arrestare, a sua volta ogni endpoint. Verificare che hello DNS restituisce l'indirizzo IP hello dell'endpoint successivo hello nell'elenco di hello. Quando tutti gli endpoint sono inattivi, si dovrebbe ottenere nuovamente l'indirizzo IP hello del endpoint primario hello.

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a>Come tootest hello ponderati in metodo di routing del traffico

1. Lasciare tutti gli endpoint attivi.
2. Usando un unico client, richiedere la risoluzione DNS per il nome di dominio aziendale mediante nslookup o un'utilità simile.
3. Assicurarsi che hello risolto l'indirizzo IP corrispondente a uno degli endpoint.
4. Scaricare la cache del client DNS e continuare a ripetere i passaggi 2 e 3 per ciascun endpoint. Vengono visualizzati i diversi indirizzi IP restituiti per ognuno degli endpoint.

## <a name="how-tootest-hello-performance-traffic-routing-method"></a>Come metodo di routing del traffico prestazioni hello tootest

tooeffectively testare un metodo di routing del traffico di prestazioni, è necessario disporre di client in diverse parti di hello world. È possibile creare i client in diverse aree di Azure che possono essere utilizzati tootest i servizi. Se si dispone di una rete globale, è possibile accedere tooclients in altre parti di hello world in modalità remota ed eseguire i test da qui.

In alternativa, sono disponibili servizi gratuiti di analisi approfondita e DNS basati su Web. Alcuni di questi strumenti consentono hello possibilità toocheck nomi DNS da diverse posizioni in tutto il mondo hello. Per alcuni esempi, eseguire una ricerca con le parole chiave "Ricerca DNS". Servizi di terze parti, ad esempio Gomez o Keynote possono essere utilizzato tooconfirm che dei profili distribuiscano il traffico come previsto.

## <a name="next-steps"></a>Passaggi successivi

* [Informazioni sui metodi di routing di Gestione traffico](traffic-manager-routing-methods.md)
* [Considerazioni sulle prestazioni di gestione traffico](traffic-manager-performance-considerations.md)
* [Risoluzione dei problemi relativi allo stato Danneggiato di Gestione traffico](traffic-manager-troubleshooting-degraded.md)
