---
title: "aaaLearn sulle funzionalità delle edizioni dei servizi BizTalk | Documenti Microsoft"
description: "Confrontare le funzionalità delle edizioni di BizTalk Services hello hello: gratuito, Developer, Basic, Standard e Premium. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>Servizi BizTalk: Grafico edizioni

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Servizi BizTalk di Azure offre diverse edizioni. Utilizzare questo toodetermine articolo quale edizione è adatta alle proprie esigenze di scenario e business.

## <a name="compare-hello-editions"></a>Confronto tra le edizioni di hello
**Free (anteprima)**

Consente di creare e gestire connessioni ibride. Una connessione ibrida è un tooconnect facilmente tooan un sito Web di Azure locale del sistema, ad esempio SQL Server.

**Developer**

Include connessioni ibride, l'elaborazione dei messaggi EAI e EDI con un portale di gestione dei partner commerciali facile da usare, il supporto di schemi EDI comuni e l'elaborazione avanzata di EDI su X12 e AS2. Creare scenari EAI servizi nel cloud hello di connessione con qualsiasi tooread protocolli HTTP/S, REST, FTP, WCF e SFTP e scrivere i messaggi.  Utilizzare sistemi LOB locali tooon di connettività con schede pronto all'uso di SAP, Oracle e-business, database Oracle, Siebel e SQL Server. È presente un ambiente a misura di sviluppatore, con strumenti di Visual Studio per sviluppare e distribuire con facilità le applicazioni. Limitato toodevelopment test scopi e solo con alcun livello di contratto di servizio.

**Basic**

Include la maggior parte delle funzionalità per gli sviluppatori di hello con aumenta in connessioni di connessioni ibride, i bridge EAI, accordi EDI e BizTalk Adapter Pack. Offre inoltre la disponibilità elevata e hello opzione tooscale con un contratto di servizio (SLA).

**Standard**

Include tutte le funzionalità di base hello con aumenta in connessioni di connessioni ibride, i bridge EAI, accordi EDI e BizTalk Adapter Pack. Offre inoltre la disponibilità elevata e hello opzione tooscale con un contratto di servizio (SLA).

**Premium**

Include tutte le funzionalità Standard di hello con aumenta in connessioni di connessioni ibride, i bridge EAI, accordi EDI e BizTalk Adapter Pack. Include anche l'archiviazione, la disponibilità elevata e hello opzione tooscale con un contratto di servizio (SLA).

## <a name="editions-chart"></a>Grafico edizioni
Hello nella tabella seguente sono elencate le differenze di hello.

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>Free (anteprima)</th>
        <th>Developer</th>
        <th>Basic</th>
        <th>Standard</th>
        <th>Premium</th>
</tr>

<tr>
<td><strong>Prezzo iniziale</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011"> Prezzi di Servizi BizTalk di Azure</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full">Calcolatore dei prezzi di Azure</a></td>
</tr>
<tr>
<td><strong>Configurazione minima predefinita</strong></td>
<td>1 unità Free</td>
<td>1 unità Developer</td>
<td>1 unità Basic</td>
<td>1 unità Standard</td>
<td>1 unità Premium</td>
</tr>
<tr>
<td><strong>Ridimensionare</strong></td>
<td>Nessuna scalabilità</td>
<td>Nessuna scalabilità</td>
<td>Sì, con incrementi di 1 unità Basic</td>
<td>Sì, in incrementi di 1 unità Standard</td>
<td>Sì, in incrementi di 1 unità Premium</td>
</tr>
<tr>
<td><strong>Scalabilità orizzontale massima consentita</strong></td>
<td>Nessuna scalabilità</td>
<td>Nessuna scalabilità</td>
<td>Unità too8</td>
<td>Unità too8</td>
<td>Unità too8</td>
</tr>
<tr>
<td><strong>Bridge EAI per unità</strong></td>
<td>Non incluso</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI, AS2</strong>
<br/><br/>
Include contratti TPM</td>
<td>Non incluso</td>
<td>Inclusi. 10 contratti per unità.</td>
<td>Inclusi. 50 contratti per unità.</td>
<td>Inclusi. 250 contratti per unità.</td>
<td>Inclusi. 1000 contratti per unità.</td>
</tr>
<tr>
<td><strong>Connessioni ibride per unità</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>Trasferimento di dati di connessioni ibride (GB) per unità</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>Sistemi LOB locali tooon connessioni di servizio Adapter BizTalk</strong></td>
<td>Non incluso</td>
<td>1 connessione</td>
<td>2 connessioni</td>
<td>5 connessioni</td>
<td>25 connessioni</td>
</tr>
<tr>
<td align="left"><strong>Protocolli/sistemi supportati:</strong>
<ul>
<li>http</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>Bus di servizio</li>
<li>BLOB Azure</li>
<li>API REST</li>
</ul>
</td>
<td>Non incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Disponibilità elevata</strong>
<br/><br/>
Per il contratto di servizio, vedere i <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">prezzi dei servizi BizTalk</a>.
</td>
<td>Non incluso</td>
<td>Non incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Backup e ripristino</strong></td>
<td>Non incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Rilevamento</strong></td>
<td>Non incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Archiviazione</strong><br/><br/>
Include ricevuta di non ripudio (NRR) e download dei messaggi rilevati</td>
<td>Non incluso</td>
<td>Incluso</td>
<td>Non incluso</td>
<td>Non incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Uso di codice personalizzato</strong></td>
<td>Non incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Uso di trasformazioni, inclusi file XSLT personalizzati</strong></td>
<td>Non incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
</table>

> [!NOTE]
> Per garantire la resilienza contro errori hardware, la disponibilità elevata richiede la presenza di macchine virtuali in un'unica unità di BizTalk.
> 
> 

## <a name="faqs"></a>Domande frequenti
#### <a name="what-is-a-biztalk-unit"></a>Che cos'è un'unità di BizTalk?
Un' "unità" è livello atomico di hello di una distribuzione di servizi BizTalk di Azure. Ogni edizione include un'unità con capacità di calcolo e memoria diverse. Un'unità Basic, ad esempio, ha maggiori funzionalità di calcolo di un'unità Developer, una Standard ha maggiori funzionalità di calcolo di una Basic e così via. Quando si parla di scalabilità di Servizi BizTalk, la si intende in termini di unità.

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>Qual è la differenza hello tra servizi BizTalk e macchina virtuale di Azure BizTalk?
Servizi BizTalk fornisce un'architettura Platform-as-a-Service (PaaS) true per la compilazione di soluzioni di integrazione nel cloud hello. Con il modello PaaS hello completamente concentrarsi sulla logica dell'applicazione hello e lasciare tutte hello tooMicrosoft di gestione dell'infrastruttura, tra cui:

* Nessuna necessità toomanage o patch macchine virtuali.
* Microsoft garantisce la disponibilità.
* È possibile controllare la scala su richiesta, richiedendo semplicemente più o meno capacità tramite hello portale di Azure.

BizTalk Server su Macchine virtuali di Azure offre un'architettura di infrastruttura distribuita come servizio (IaaS). Creare macchine virtuali e configurarli esattamente come per l'ambiente locale, rendendo più semplice toorun le applicazioni esistenti nel cloud hello senza apportare modifiche al codice. Con IaaS, si è ancora responsabile della configurazione di macchine virtuali hello, gestione delle macchine virtuali di hello (ad esempio, l'installazione del software e patch del sistema operativo) e progettazione di un'applicazione hello per la disponibilità elevata.

Se si desidera creare nuove soluzioni di integrazione che riducano al minimo le operazioni di gestione dell'infrastruttura, usare Servizi BizTalk. Se si vuole tooquickly la migrazione di soluzioni BizTalk esistente o per un ambiente on demand toodevelop e test di BizTalk Server applicazioni, utilizzare BizTalk Server in una macchina virtuale di Azure.

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>Qual è la differenza hello tra le connessioni ibride e il servizio Adapter BizTalk?
Servizio Adapter BizTalk Hello viene utilizzato da un servizio BizTalk di Azure. Hello servizio Adapter BizTalk utilizza sistema Line-of-Business (LOB) locale di hello BizTalk Adapter Pack tooconnect tooan. Una connessione ibrida fornisce un modo semplice e intuitiva di tooconnect applicazioni Azure, ad esempio hello funzionalità di App Web nel servizio App di Azure e servizi mobili di Azure, tooan risorse in locale.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>Che cosa significa "Trasferimento di dati di connessioni ibride (GB) per unità"? Si intende al minuto/ora/giorno/mese? Cosa accade quando viene raggiunto il limite di hello?
Hello costo connessione ibrida per unità dipende dall'edizione dei servizi BizTalk hello. In pratica, i costi dipendono dalla quantità di dati da trasferire. Ad esempio, trasferire 10 GB di dati al giorno costa meno che trasferire 100 GB al giorno. Hello utilizzare [calcolatore dei costi](https://azure.microsoft.com/pricing/calculator/?scenario=full) per i costi specifici toodetermine di servizi BizTalk. In genere, i limiti di hello vengono applicati a ogni giorno. Se si supera il limite di hello, qualsiasi eccedenza viene addebitato con frequenza hello $ 1 per GB.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>Quando si crea un contratto nei servizi BizTalk, perché numero hello dei Bridge salire da due anziché uno?
Ogni contratto include due bridge diversi: uno per la comunicazione sul lato di trasmissione e l'altro sul lato di ricezione.

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>Cosa accade quando raggiunto il limite di quota hello numero hello di Bridge o contratti?
Si toodeploy non in grado di qualsiasi nuovo bridge o creano i nuovi contratti. toodeploy altre, è necessario tooscale toomore unità del servizio BizTalk hello o edizione superiore tooa aggiornamento.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>Come la migrazione da un livello di servizi BizTalk tooanother?
edizione gratuita di Hello non è possibile eseguire la migrazione o 'con scalabilità verticale' tooanother livello e non può essere eseguito il backup e ripristino tooanother livello. Se è necessario un altro livello, creare un nuovo BizTalk Service utilizzando il nuovo livello di hello. Gli elementi creati utilizzando l'edizione gratuita di hello, incluse le connessioni ibride, toobe necessario ricreata hello nuovo BizTalk Service. 

Per le edizioni di rimanenti hello, utilizzare hello backup e ripristino per la migrazione gli elementi da un livello tooanother. Eseguire il backup, ad esempio, gli elementi nel livello Standard hello e quindi ripristinarli livello Premium toohello. [Servizi BizTalk: Backup e ripristino](biztalk-backup-restore.md) vengono descritti i percorsi di migrazione supportato hello ed elenca quali elementi sottoposti a backup. Si noti che il backup delle connessioni ibride non viene eseguito. Dopo il backup e ripristino tooa nuovo livello, quindi ricreare le connessioni ibride hello.  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>Servizio Adapter BizTalk hello è incluso nel servizio hello? La modalità di ricezione software hello?
Sì, hello servizio Adapter BizTalk con hello BizTalk Adapter Pack sono inclusi con hello Azure BizTalk Services SDK [scaricare](http://www.microsoft.com/download/details.aspx?id=39087).

## <a name="next-steps"></a>Passaggi successivi
Servizi BizTalk di Azure toocreate in hello Azure, andare troppo[servizi BizTalk: Provisioning mediante hello Azure portal](biztalk-provision-services.md). creazione di applicazioni, andare troppo toostart[servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="additional-resources"></a>Risorse aggiuntive
* [Servizi BizTalk: Provisioning mediante hello portale di Azure](biztalk-provision-services.md)<br/>
* [Servizi BizTalk: Grafico dello stato del provisioning](biztalk-service-state-chart.md)<br/>
* [Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: Backup and restore](biztalk-backup-restore.md)<br/>
* [Servizi BizTalk: limitazione](biztalk-throttling-thresholds.md)<br/>
* [Servizi BizTalk: nome e chiave dell'autorità emittente](biztalk-issuer-name-issuer-key.md)<br/>
* [Come è possibile utilizzare hello Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

