---
title: stato aaaTroubleshooting ridotto per gestione traffico di Azure
description: Come i profili di gestione traffico tootroubleshoot quando viene illustrato come dello stato danneggiato.
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>Risoluzione dei problemi relativi allo stato Danneggiato di Gestione traffico

In questo articolo viene descritto come tootroubleshoot un profilo di Traffic Manager di Azure che viene visualizzato uno stato danneggiato. Per questo scenario, è consigliabile che sia stato configurato un profilo di gestione traffico verso toosome dei servizi ospitati cloudapp.net. Se l'integrità di hello di gestione del traffico consente di visualizzare un **danneggiato** potrebbe essere stato, quindi lo stato di hello di uno o più endpoint **danneggiato**:

![Stato degli endpoint Danneggiato](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

Se l'integrità di hello di gestione del traffico consente di visualizzare un **inattivo** stato, entrambi gli endpoint possono essere **disabilitato**:

![Stato Inattivo di Gestione traffico](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>Informazioni sui probe di Gestione traffico

* Gestione traffico considera un toobe endpoint ONLINE solo quando probe hello riceve una risposta HTTP 200 eseguire il backup dal percorso di sondaggio hello. Qualsiasi risposta diversa da 200 viene considerata un errore.
* Un reindirizzamento 30 x ha esito negativo, anche se hello reindirizzato URL restituisce 200.
* Per i probe HTTPS, gli errori di certificati vengono ignorati.
* contenuto effettivo di Hello del percorso di sondaggio hello non è rilevante, purché viene restituito un messaggio 200. Ricerca di un tipo di URL toosome statico contenuto "/ favicon.ico" è una tecnica comune. Contenuto dinamico, ad esempio le pagine ASP hello, non sempre restituisca 200, anche quando un'applicazione hello è integra.
* Una procedura consigliata è tooset hello Probe toosomething percorso dotato di sufficiente toodetermine logica che hello del sito è verso l'alto o verso il basso. In hello delle esempio precedente, impostando hello percorso too"/favicon.ico", si desidera utilizzare solo tale w3wp.exe test sta rispondendo. Questo probe non indica necessariamente che l'applicazione Web è integra. Un'opzione migliore può essere tooset tooa un percorso, ad esempio "/ Probe.aspx" che dispone dello stato di hello toodetermine logica del sito hello. Ad esempio, è possibile utilizzare utilizzo tooCPU di contatori delle prestazioni o misura hello numero di richieste non riuscite. Oppure è possibile tentare le risorse del database tooaccess o toomake stato sessione assicurarsi che l'applicazione web hello funzioni.
* Se tutti gli endpoint in un profilo sono danneggiati, quindi considera tutti gli endpoint di gestione traffico come integri e instrada il traffico tooall endpoint. Questo comportamento assicura che i problemi con hello meccanismo di probe non causino un'interruzione completa del servizio.

## <a name="troubleshooting"></a>Risoluzione dei problemi

tootroubleshoot un errore probe, è necessario uno strumento che viene restituito il codice di stato HTTP hello dall'URL del probe hello. Sono disponibili numerosi strumenti disponibili che mostrano hello risposta HTTP non elaborato.

* [Fiddler](http://www.telerik.com/fiddler)
* [curl](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm)

Inoltre, è possibile utilizzare scheda di rete hello di hello F12 strumenti di debug nelle risposte HTTP hello tooview di Internet Explorer.

Per questo esempio si desidera risposta hello toosee l'URL del probe: http://watestsdp2008r2.cloudapp.net:80/Probe. Hello esempio PowerShell seguente illustra il problema di hello.

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

Output di esempio:

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

Si noti che è pervenuta una risposta di reindirizzamento. Come indicato in precedenza, qualsiasi StatusCode diverso da 200 viene considerato un errore. Modifiche di Traffic Manager hello tooOffline lo stato di endpoint. problema di hello tooresolve, controllo hello sito Web configuration tooensure che hello StatusCode corretto può essere restituiti dal percorso di sondaggio hello. Riconfigurare hello Traffic Manager toopoint tooa percorso di sondaggio che restituisce un messaggio 200.

Se il probe utilizza hello il protocollo HTTPS, potrebbe essere toodisable certificato verifica degli errori SSL/TLS di tooavoid durante il test. Hello istruzioni di PowerShell seguente disabilita la convalida dei certificati per la sessione corrente di PowerShell hello:

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a>Passaggi successivi

[Informazioni sui metodi di routing di Gestione traffico](traffic-manager-routing-methods.md)

[Gestione traffico di Azure](traffic-manager-overview.md)

[Servizi cloud](http://go.microsoft.com/fwlink/?LinkId=314074)

[App Web di Azure](https://azure.microsoft.com/documentation/services/app-service/web/)

[Operazioni per Gestione traffico (informazioni di riferimento API REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Cmdlet di Gestione traffico di Azure][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
