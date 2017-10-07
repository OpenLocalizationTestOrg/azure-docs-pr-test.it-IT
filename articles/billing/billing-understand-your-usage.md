---
title: aaaUnderstand di Azure dettagliate sull'utilizzo | Documenti Microsoft
description: Informazioni su come tooread e informazioni sulle sezioni hello relativa all'utilizzo dettagliato CSV per la sottoscrizione di Azure
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: tonguyen
ms.openlocfilehash: c9284bf94bfa9f36cdd5d39e653a35def7c1aa34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-terms-on-your-microsoft-azure-detailed-usage-charges"></a>Comprendere i dettagli degli addebiti basati sui dati di utilizzo dettagliato di Microsoft Azure 
Hello dettagliate sull'utilizzo di file CSV spese contiene ogni giorno e gli addebiti di utilizzo di livello misuratore per hello periodo di fatturazione corrente. 

tooget file dettagliate sull'utilizzo, vedere [come tooget la fatturazione di Azure della fattura e dati di utilizzo giornalieri](billing-download-azure-invoice-daily-usage-date.md).
È disponibile in un formato di file CSV (valori separati dalla virgola) che è possibile aprire in un foglio di calcolo. Se sono disponibili due versioni, scaricare la versione 2. Che è più recente formato di file hello.

Gli addebiti di utilizzo sono hello totale **mensile** addebiti in una sottoscrizione. e non tengono in considerazione eventuali accrediti o sconti applicabili.

## <a name="detailed-terms-and-descriptions-of-your-detailed-usage-file"></a>Termini e descrizioni relativi al file di utilizzo dettagliato
Hello nelle sezioni seguenti vengono descritti termini importanti di hello nella versione 2 del file di hello dettagliate sull'utilizzo.

### <a name="statement"></a>Istruzione
sezione superiore Hello hello dettagliate sull'utilizzo CSV Mostra hello servizi file che è stato utilizzato durante il periodo di fatturazione del mese hello. Hello nella tabella seguente sono elencati i termini di hello e le descrizioni illustrate in questa sezione.

| Termine | Descrizione |
| --- | --- |
|Periodo di fatturazione |periodo di fatturazione Hello quando sono stati utilizzati i misuratori hello |
|Categoria misuratore |Identifica hello servizio principale per l'utilizzo di hello |
|Sottocategoria misuratore |Definisce il tipo di hello del servizio di Azure che può influire sulla velocità di hello |
|Nome misuratore |Identifica hello unità di misura del misuratore hello consumato |
|Area misuratore |Identifica il percorso di hello del Data Center hello per alcuni servizi che i prezzi variano in base alla posizione Data Center |
|SKU |Identifica l'identificatore di hello sistema univoco per ogni misuratore di Azure |
|Unità |Identifica l'unità che servizio hello viene addebitato in hello. Ad esempio, GB, ore, decine di migliaia. |
|Quantità consumata |quantità di Hello del misuratore hello utilizzato durante il periodo di fatturazione hello |
|Quantità inclusa |quantità di Hello del misuratore hello incluso senza alcun costo del periodo di fatturazione corrente |
|Quantità in eccesso |Mostra hello differenza tra hello quantità consumate e hello quantità inclusa. Sarà addebitato questo importo. Per le offerte di pagamento a consumo con quantità non inclusi con l'offerta di hello, questo totale è hello stesso hello quantità consumate. |
|Entro l'impegno |Mostra i costi di misuratore hello da sottrarre all'importo dell'impegno associata con l'offerta 6 o 12 mesi. I costi del contatore vengono detratti in ordine cronologico. |
|Valuta |valuta Hello usata nel periodo di fatturazione corrente |
|Eccedenza |Mostra i costi di misuratore hello che superano l'importo dell'impegno associata con l'offerta 6 o 12 mesi |
|Tariffa dell'impegno |Mostra hello impegno velocità in base alla quantità di memoria impegnata totale hello associata con l'offerta 6 o 12 mesi |
|Tariffa |frequenza di Hello che verranno addebitati unitario fatturabile |
|Valore |Mostra il risultato di hello di moltiplicazione hello colonna Quantity eccedenza dalla colonna frequenza hello. Se non supera le quantità consumate hello hello quantità inclusa, non è previsto alcun addebito in questa colonna. |

### <a name="daily-usage"></a>Utilizzo giornaliero

Hello giornaliero sezione Utilizzo del file CSV hello Mostra i dettagli di utilizzo che influiscono sulle tariffe di fatturazione hello. Hello nella tabella seguente sono elencati i termini di hello e le descrizioni illustrate in questa sezione.

| Termine | Descrizione |
| --- | --- |
|Data utilizzo |Data di Hello in cui è stato usato il misuratore hello |
|Categoria misuratore |Identifica i servizi di hello principale per cui appartiene questo utilizzo |
|ID misuratore |Hello fatturato identificatore misuratore utilizzati tooprice fatturazione dell'utilizzo |
|Sottocategoria misuratore |Definisce i tipo di servizio di Azure hello che possono influire sulla velocità di hello |
|Nome misuratore |Identifica hello unità di misura del misuratore hello consumato |
|Area misuratore |Identifica il percorso di hello del Data Center hello per alcuni servizi che i prezzi variano in base alla posizione Data Center |
|Unità |Identifica unità hello tale indicatore hello viene addebitato. Ad esempio, GB, ore, decine di migliaia. |
|Quantità consumata |quantità di Hello del misuratore hello che è stato utilizzato per tale giorno |
|Percorso della risorsa |Identifica i Data Center hello in cui è in esecuzione misuratore hello |
|Servizio utilizzato |servizio di piattaforma Azure utilizzato Hello |
|Gruppo di risorse |gruppo di risorse Hello in cui hello misuratore distribuito è in esecuzione in. <br/><br/>Per altre informazioni, vedere [Panoramica di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
|ID istanza | Identificatore Hello misuratore hello. <br/><br/> l'identificatore Hello contiene nome hello specificato per il misuratore hello quando è stata creata. È il nome della risorsa hello di hello o hello completo di ID di risorsa. Per altre informazioni, vedere [L'API di Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). |
|Tag | Tag assegnato toohello misuratore. I record di tag toogroup fatturazione.<br/><br/>Ad esempio, è possibile utilizzare i costi toodistribute tag dal reparto hello che utilizza il misuratore hello. Servizi che supportano l'emissione dei tag sono macchine virtuali, archiviazione e servizi di rete eseguito il provisioning con hello [API di gestione risorse di Azure](https://docs.microsoft.com/rest/api/resources/resources). Per altre informazioni, vedere [Organize your Azure resources with tags](http://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) (Organizzare le risorse di Azure con i tag). |
|Informazioni aggiuntive |Metadati specifici del servizio. Ad esempio un tipo di immagine per una macchina virtuale. |
|Informazioni servizio 1 |nome del progetto Hello servizio hello appartiene tooon la sottoscrizione |
|Informazioni servizio 2 |Campo legacy che acquisisce i metadati specifici del servizio facoltativo |

## <a name="how-do-i-make-sure-that-hello-charges-in-my-detailed-usage-file-are-correct"></a>Come assicurarsi che siano corretti addebiti hello nel file dettagliate sull'utilizzo
Se nel file di utilizzo dettagliato è presente un addebito su cui si vogliono ricevere altre informazioni, vedere [Comprendere la fattura per Microsoft Azure](./billing-understand-your-bill.md)

## <a name="external"></a>A cosa si riferiscono gli addebiti per servizi esterni?
I servizi esterni, noti anche come ordini Marketplace, sono erogati da fornitori di servizi indipendenti e vengono fatturati separatamente. gli addebiti di Hello non vengono visualizzati nella fattura di Azure hello. vedere, più toolearn [comprendere gli addebiti di servizio esterni Azure](billing-understand-your-azure-marketplace-charges.md).

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se si necessita ancora di assistenza, [contattare il supporto tecnico](https://portal.azure.com/?) per ottenere una rapida risoluzione del problema.
