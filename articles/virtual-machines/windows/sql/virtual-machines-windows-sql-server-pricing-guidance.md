---
title: costi aaaManage in modo efficace per SQL Server in macchine virtuali di Azure | Documenti Microsoft
description: Fornisce le procedure consigliate per la scelta di hello destra macchina virtuale SQL Server del modello di costo.
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>Guida ai prezzi per le VM di SQL Server in Azure

Questo argomento riporta indicazioni sui prezzi delle macchine virtuali di SQL Server in Azure. Sono disponibili diverse opzioni che influiscono sul costo, ed è importante toopick hello immagine a destra che consente di bilanciare i costi ai requisiti aziendali.

## <a name="free-licensed-sql-server-editions"></a>Edizioni di SQL Server con licenza gratuita

Se si desidera toodevelop, testare, o compilare un modello di prova, quindi utilizzare hello con licenza gratuita **SQL Server Developer edition**. Questa edizione è tutto ciò che in SQL Server Enterprise edition, pertanto è possibile usarlo toobuild qualsiasi applicazione che si desidera visualizzare. Non è consentito toorun nell'ambiente di produzione. Una macchina virtuale di SQL Server Developer addebiterà solo costo hello di hello macchina virtuale, non per le licenze di SQL Server.

Se si desidera toorun un carico di lavoro leggero nell'ambiente di produzione (< 4 core, < 1 GB di memoria, < 10 GB/database), quindi utilizzare hello con licenza gratuita **SQL Server Express edition**. Una macchina virtuale di SQL Express verrà addebitata solo costo hello di hello macchina virtuale, non alle licenze di SQL.

Per questi carichi di lavoro di sviluppo/test o di produzione leggeri è possibile risparmiare anche scegliendo una VM più piccola ma comunque adeguata a tali carichi di lavoro. Hello DS1v2 potrebbe essere una buona scelta per questi carichi di lavoro.

toocreate una macchina virtuale Azure di SQL Server 2016 con una di queste immagini, vedere hello seguenti collegamenti:

- [VM SQL Server 2016 Developer di Azure](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [VM SQL Server 2016 Express di Azure](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>Edizioni di SQL Server a pagamento

Se si dispone di un carico di lavoro di produzione non lightweight, utilizzare una delle seguenti edizioni di SQL Server hello:

| Edizione di SQL Server | Carico di lavoro |
|-----|-----|
| Web | Siti Web di piccole dimensioni |
| Standard | Carichi di lavoro di piccole dimensioni toomedium |
| Enterprise | Carichi di lavoro di grandi dimensioni o critici|

Si dispone di due opzioni toopay per le licenze di SQL Server per queste edizioni: *pagamento in base all'utilizzo* o *portare la propria licenza*.

### <a name="pay-per-usage"></a>Pagamento in base all'utilizzo

**Licenza di SQL Server hello pagamento in base all'utilizzo** indica che il costo al minuto hello dell'esecuzione di hello macchina virtuale di Azure include il costo di hello di licenza di SQL Server hello. È possibile visualizzare hello prezzi per hello diverse edizioni di SQL Server (Web, Standard, Enterprise) in hello [macchina virtuale di Azure pagina dei prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard). Hello costo è hello uguale per tutte le versioni di SQL Server (2008 R2 too2016). Come con SQL Server licenze hello in generale, i costi di licenza al minuto dipende dal numero di hello di core VM.

Pagamento hello SQL Server in base all'utilizzo di licenza è consigliato per:

- Carichi di lavoro temporanei o periodici. Ad esempio, un'applicazione che deve toosupport un evento per un paio di mesi ogni anno o analisi di business di lunedì.
- Carichi di lavoro con durata o dimensione sconosciuta. Ad esempio un'app che potrebbe non essere necessaria per alcuni mesi o che potrebbe richiedere una maggiore o minore potenza di calcolo, in base alla richiesta.

toocreate una macchina virtuale Azure di SQL Server 2016 con una di queste immagini di pagamento in base all'utilizzo, vedere hello seguenti collegamenti:

- [VM SQL Server 2016 Web di Azure](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [VM SQL Server 2016 Standard di Azure](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [VM SQL Server 2016 Enterprise di Azure](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> Quando si crea una macchina virtuale di SQL Server nel portale di Azure hello, hello stimato il costo mensile visualizzato su hello **scegliere una dimensione** blade non include i costi di licenza di SQL Server. Questo è il costo di hello di hello VM autonoma.
>
> ![Scegliere il pannello Dimensioni macchina virtuale](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Per hello con licenza gratuita Express e Developer Edition di SQL Server, si tratta di costo stimato totale hello. Ma per Web, Standard ed Enterprise, trovare hello aggiuntive sui costi delle licenze di SQL su hello [pagina dei prezzi delle macchine virtuali di Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Nella pagina dei prezzi di hello, selezionare l'edizione di destinazione di SQL Server.

### <a name="bring-your-own-license-byol"></a>Bring Your Own License (BYOL)

**Portare la propria licenza di SQL Server tramite mobilità delle licenze**, definita anche tooas **BYOL**, indica l'utilizzo di un Volume di licenza di SQL Server esistente con Software Assurance in una macchina virtuale di Azure. Una macchina virtuale di SQL Server utilizzando BYOL addebiterà solo per il costo di hello di esecuzione hello macchina virtuale, non per le licenze di SQL Server, dato che è già stata acquisita licenze e Software Assurance tramite un programma di contratti multilicenza.

Bringing Your Own License per SQL Server attraverso Mobilità delle licenze è consigliato per:

- Carichi di lavoro continui. Ad esempio, un'applicazione che richiede operazioni di business toosupport 24x7.
- Carichi di lavoro con dimensione e durata note. Ad esempio, un'applicazione che verrà richiesto per l'intero anno hello e quale richiesta è stata previsti.

toouse BYOL con una macchina virtuale di SQL Server, è necessario disporre una licenza per SQL Server Standard o Enterprise e [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), che è un'opzione obbligatoria tramite alcuni [multilicenza](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programmi e facoltativa acquistare con altri utenti.  prezzi di livelli forniti tramite programmi multilicenza Hello varia in base al tipo di hello del contratto e hello quantità e o impegno tooSQL Server. Ma come regola generale, portare la propria licenza per i carichi di lavoro di produzione continuo hello seguenti vantaggi:

| Vantaggio dell'opzione BYOL | Descrizione |
|-----|-----|
| **Risparmi sui costi** | Bringing Your Own License per SQL Server è più conveniente rispetto al pagamento in base all'utilizzo se un carico di lavoro eseguirà continuativamente SQL Server Standard o Enterprise per *più di 10 mesi*. |
| **Risparmi a lungo termine** | È in Media, *30% più economico all'anno* toobuy o rinnovare una licenza di SQL Server per hello primi tre anni. Inoltre, dopo 3 anni, è necessario toorenew hello licenza più, pagare solo per Software Assurance. A quel punto comporta un *risparmio del 200%*. |
| **Replica secondaria passiva gratuita** | Un altro vantaggio di rendere la propria licenza è hello [liberare le licenze di una replica secondaria passiva](https://azure.microsoft.com/pricing/licensing-faq/) per SQL Server per scopi di disponibilità elevata. Ciò consente di tagliare nella metà hello licenze costo di una distribuzione di SQL Server a disponibilità elevata (ad esempio tramite gruppi di disponibilità AlwaysOn). Hello diritti toorun hello passivo database secondario vengono forniti tramite hello beneficio Software Assurance i server di failover. |

toocreate una macchina virtuale Azure di SQL Server 2016 con una di queste immagini bring-your-proprietari-licenze, vedere le macchine virtuali hello precedute dal prefisso "{BYOL}":

- [VM SQL Server 2016 Enterprise di Azure](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [VM SQL Server 2016 Standard di Azure](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> Si prega di comunicare entro 10 giorni il numero di licenze di SQL Server che si useranno in Azure. salve le immagini precedenti toohello di collegamenti sono incluse le istruzioni su come toodo questo.

## <a name="avoid-unecessary-costs"></a>Evitare i costi non necessari

Se si usano i carichi di lavoro che non vengono eseguiti in modo continuo, prendere in considerazione l'arresto della macchina virtuale hello durante i periodi di hello inattivo. Si paga solo per le risorse utilizzate.

Ad esempio, se si sta semplicemente SQL Server in una macchina virtuale di Azure, è necessario tooincur spese accidentalmente lasciando in esecuzione per settimane. Una soluzione è hello toouse [funzionalità di arresto automatico](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Arresto automatico della VM di SQL](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

L'arresto automatico fa parte di un insieme più ampio di funzionalità simili fornite da [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).

Per altri flussi di lavoro, prendere in considerazione l'arresto e il riavvio automatico delle VM con una soluzione script come [Automazione di Azure](https://azure.microsoft.com/services/automation/).

> [!IMPORTANT]
> L'arresto e la deallocazione della macchina virtuale è gli addebiti tooavoid modo solo hello. Semplicemente l'arresto o utilizzando power opzioni tooshut verso il basso hello VM comporta comunque addebiti di utilizzo.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni di guida generali sui prezzi di Azure, vedere [Evitare costi imprevisti con la gestione dei costi e alla fatturazione di Azure](../../../billing/billing-getting-started.md).

Per hello le macchine virtuali più recenti sui prezzi, incluso SQL Server, vedere hello [macchina virtuale di Azure pagina dei prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).

Esaminare altri argomenti relativi alle macchine virtuali di SQL Server in [Panoramica di SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).
