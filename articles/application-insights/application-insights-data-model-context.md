---
title: aaaAzure modello dati di telemetria Insights di applicazione - contesto dati di telemetria | Documenti Microsoft
description: Modello di contesto dei dati di telemetria di Application Insights
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a>Contesto dei dati di telemetria: modello di dati di Application Insights

Ogni elemento di telemetria può contenere campi di contesto fortemente tipizzati. Ogni campo consente uno specifico scenario di monitoraggio. Utilizzare hello proprietà personalizzate della raccolta toostore personalizzati o specifici dell'applicazione le informazioni contestuali.


##<a name="application-version"></a>Versione dell'applicazione

Le informazioni nei campi di contesto dell'applicazione hello sono sempre sull'applicazione hello che invia i dati di telemetria hello. Versione dell'applicazione è utilizzata tooanalyze tendenza modifiche nel comportamento dell'applicazione hello e le relative distribuzioni toohello correlazione.

Lunghezza massima: 1024


##<a name="client-ip-address"></a>Indirizzo IP client

indirizzo IP di Hello del dispositivo client hello. Sono supportati sia IPv4 che IPv6. Quando i dati di telemetria viene inviato da un servizio, il contesto di percorso hello è sull'utente hello che ha avviato l'operazione di hello in servizio hello. Application Insights estrarre le informazioni di posizione geografica hello da indirizzo IP del client hello e quindi troncarlo. L'IP client da solo non può quindi essere usato come informazione personale dell'utente finale. 

Lunghezza massima: 46


##<a name="device-type"></a>Tipo di dispositivo

Originariamente questo campo è stato utilizzato il tipo di hello tooindicate hello hello finale dell'utente di dispositivo di un'applicazione hello utilizzato. Oggi utilizzato principalmente toodistinguish JavaScript telemetria con hello tipo di dispositivo 'Browser' dalla telemetria sul lato server con il tipo di dispositivo hello 'Computer'.

Lunghezza massima: 64


##<a name="operation-id"></a>ID operazione

Identificatore univoco dell'operazione di hello radice. Questo identificatore consente telemetria toogroup tra più componenti. Per informazioni dettagliate, vedere [Correlazione di dati di telemetria](application-insights-correlation.md). id operazione Hello viene creato da una richiesta o una visualizzazione di pagina. Tutti gli altri dati di telemetria imposta questo valore del campo toohello per hello contenente la vista richiesta o della pagina. 

Lunghezza massima: 128


##<a name="parent-operation-id"></a>ID operazione padre

Identificatore univoco del padre dell'elemento di dati di telemetria hello di Hello. Per informazioni dettagliate, vedere [Correlazione di dati di telemetria](application-insights-correlation.md).

Lunghezza massima: 128


##<a name="operation-name"></a>Nome operazione

nome di Hello (gruppo) dell'operazione di hello. nome dell'operazione Hello viene creato da una richiesta o una visualizzazione di pagina. Tutti gli altri elementi di dati di telemetria impostare questo valore del campo toohello per hello contenente la vista richiesta o della pagina. Nome dell'operazione viene utilizzato per la ricerca di tutti gli elementi di dati di telemetria hello per un gruppo di operazioni (ad esempio ' GET Home/Index'). Questa proprietà di contesto viene utilizzato tooanswer domande quali "quali sono hello tipico eccezioni in questa pagina."

Lunghezza massima: 1024


##<a name="synthetic-source-of-hello-operation"></a>Sintetica origine dell'operazione di hello

Il nome dell'origine sintetica. Alcuni dati di telemetria da un'applicazione hello può rappresentare traffico sintetico. È possibile crawler indicizzazione hello web sito, il test di disponibilità del sito o le tracce da librerie di diagnostica come Application Insights SDK se stesso.

Lunghezza massima: 1024


##<a name="session-id"></a>ID sessione

ID di sessione - istanza hello di interazione dell'utente di hello con app hello. Le informazioni nei campi di contesto di sessione hello sono sempre sull'utente finale di hello. Quando i dati di telemetria viene inviato da un servizio, il contesto della sessione hello è sull'utente hello che ha avviato l'operazione di hello in servizio hello.

Lunghezza massima: 64


##<a name="anonymous-user-id"></a>ID utente anonimo

L'ID utente anonimo. Rappresenta l'utente finale di hello di un'applicazione hello. Quando i dati di telemetria viene inviato da un servizio, contesto utente hello è sull'utente hello che ha avviato l'operazione di hello in servizio hello.

[Campionamento](app-insights-sampling.md) è uno della quantità di hello tecniche toominimize hello di telemetria raccolto. Campionamento algoritmo tentativi tooeither esempio in o out hello tutti correlati telemetria. L'ID utente anonimo viene usato per generare un punteggio di campionamento. L'ID utente anonimo deve essere quindi un valore sufficientemente casuale. 

L'utilizzo di nome utente toostore di id utente anonimo è un utilizzo improprio del campo hello. Usare un ID utente autenticato.

Lunghezza massima: 128


##<a name="authenticated-user-id"></a>ID utente autenticato

Id utente autenticato. Hello opposto dell'id utente anonimo, questo campo rappresenta utente hello con un nome descrittivo. Le sue informazioni personali non vengono infatti raccolte per impostazione predefinita dalla maggior parte degli SDK.

Lunghezza massima: 1024


##<a name="account-id"></a>ID account

Nelle applicazioni multi-tenant, si tratta hello account ID o nome, l'utente che ha hello opera con. Esempi possono essere gli ID sottoscrizione al portale di Azure, il nome del blog o la piattaforma di blogging.

Lunghezza massima: 1024


##<a name="cloud-role"></a>Ruolo del cloud

Nome di un'applicazione hello hello ruolo è una parte. Esegue il mapping direttamente il nome del ruolo toohello in azure. Può inoltre essere utilizzati toodistinguish micro servizi, che fanno parte di una singola applicazione.

Lunghezza massima: 256


##<a name="cloud-role-instance"></a>Istanza del ruolo del cloud

Nome dell'istanza di hello in cui è in esecuzione un'applicazione hello. Il nome computer in locale, il nome dell'istanza in Azure.

Lunghezza massima: 256


##<a name="internal-sdk-version"></a>Informazione interna: versione dell'SDK

La versione dell'SDK. Per informazioni, vedere https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification.

Lunghezza massima: 64


##<a name="internal-node-name"></a>Informazione interna: nome del nodo

Questo campo rappresenta il nome di nodo hello utilizzato per la fatturazione. Utilizzare la toooverride hello il rilevamento standard dei nodi.

Lunghezza massima: 256


## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come troppo[estendere e filtrare i dati di telemetria](app-insights-api-filtering-sampling.md).
- Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).
- Estrarre la [configurazione](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) di una raccolta di proprietà di contesto standard.
