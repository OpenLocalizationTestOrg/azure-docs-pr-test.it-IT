---
title: "aaaOverview di scalabilità automatica in App Web, servizi Cloud e macchine virtuali di Microsoft Azure | Documenti Microsoft"
description: Panoramica del ridimensionamento automatico in Microsoft Azure. Si applica tooVirtual macchine, servizi Cloud e le applicazioni Web.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a>Panoramica del ridimensionamento automatico in Macchine virtuali di Microsoft Azure, Servizi cloud e App Web
Questo articolo descrive il ridimensionamento automatico di Microsoft Azure è vantaggiosa, e la modalità di avvio tooget utilizzarlo.  

Azure scalabilità automatica di monitoraggio si applica solo troppo[set di scalabilità di macchine virtuali](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [servizi Cloud](https://azure.microsoft.com/services/cloud-services/), e [servizio App: app Web](https://azure.microsoft.com/services/app-service/web/).

> [!NOTE]
> Azure offre due metodi per il ridimensionamento automatico. Una versione precedente di scalabilità automatica applica macchine tooVirtual (set di disponibilità). Questa funzionalità offre supporto limitato e si consiglia di eseguire la migrazione di scalabilità di macchine toovirtual imposta per il supporto della scalabilità automatica più veloce e affidabile. In questo articolo è incluso un collegamento in modo toouse hello tecnologia meno recente.  
>
>

## <a name="what-is-autoscale"></a>Informazioni sul ridimensionamento automatico
Scalabilità automatica consentono la giusta quantità hello toohave di risorse che eseguono toohandle hello carico sull'applicazione. Consente di risorse tooadd toohandle gli aumenti di caricare e salvare anche money rimuovendo le risorse che sono server inattivo. Specificare un numero minimo e massimo di istanze toorun e aggiungere o rimuovere le macchine virtuali automaticamente in base a un set di regole. La definizione di un minimo assicura che l'applicazione sia sempre in esecuzione anche in assenza di carico. La definizione di un massimo limita il costo orario totale possibile. Il ridimensionamento viene eseguito automaticamente tra questi due estremi usando le regole create.

 ![Descrizione del ridimensionamento automatico: aggiunta e rimozione di VM](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

Quando vengono soddisfatte le condizioni delle regole, vengono attivate una o più azioni di ridimensionamento automatico. È possibile aggiungere e rimuovere VM o eseguire altre azioni. Hello diagramma concettuale seguente illustra questo processo.  

 ![Diagramma di flusso del ridimensionamento automatico](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

Hello spiegazione seguente applica toohello parti del diagramma precedente hello.   

## <a name="resource-metrics"></a>Metriche delle risorse
Le risorse generano metriche, che vengono elaborate successivamente dalle regole. Le metriche sono disponibili tramite metodi diversi.
Set di scalabilità di macchine virtuali utilizzano i dati di telemetria dagli agenti di diagnostica di Azure mentre dati di telemetria per le applicazioni Web e servizi Cloud provenienti direttamente da hello infrastruttura di Azure. Alcune statistiche comunemente usate includono utilizzo della CPU, utilizzo della memoria, conteggio dei thread, lunghezza della coda e l'utilizzo del disco. Per un elenco dei dati di telemetria che è possibile usare, vedere [Metriche comuni per i ridimensionamento automatico di Azure Insights](insights-autoscale-common-metrics.md).

## <a name="custom-metrics"></a>Metriche personalizzate
È anche possibile fare uso di eventuali metriche personalizzate generate dalle applicazioni usate. Se è stato configurato il tooApplication di metriche di applicazioni toosend Insights è possibile sfruttare tali decisioni toomake metriche se tooscale o non. 

## <a name="time"></a>Tempo
Le regole basate sulla pianificazione sono basate su UTC. Quando si configurano le regole, è necessario impostare correttamente il fuso orario.  

## <a name="rules"></a>Regole
diagramma di Hello Mostra solo una regola di scalabilità automatica, ma è possibile avere molti di essi. È possibile creare regole complesse sovrapposte, secondo le esigenze della situazione locale.  I tipi di regole includono  

* **Basata su metrica** : ad esempio, eseguire questa azione quando l'utilizzo della CPU è superiore al 50%.
* **Basata sul tempo** : ad esempio, attivare un webhook alle 8:00 di ogni sabato in un determinato fuso orario.

Le regole basate sulle metriche misurano il carico dell'applicazione e aggiungono o rimuovono VM in base a tale carico. Regole basate su pianificazione consentono di tooscale quando si visualizzare i modelli di tempo del carico e si desidera tooscale prima di un aumento del carico possibili o si verifica diminuzione.  

## <a name="actions-and-automation"></a>Azioni e automazione
Le regole possono attivare uno o più tipi di azioni.

* **Ridimensionamento** : per aumentare o ridurre il numero di istanze di macchine virtuali
* **Messaggio di posta elettronica** -inviare posta elettronica toosubscription admins, coamministratori e/o indirizzo di posta elettronica aggiuntivo specificato
* **Automatizzare tramite webhook** : per chiamare webhook che possono attivare più azioni complesse all'interno o all'esterno di Azure. All'interno di Azure è possibile avviare un runbook di automazione di Azure, una funzione Azure o un'app per la logica di Azure. Un esempio di URL di terze parti esterno ad Azure include servizi come Slack e Twilio.

## <a name="autoscale-settings"></a>Impostazioni di scalabilità automatica
Scalabilità automatica utilizzare hello terminologia e struttura.

- Un **impostazione di scalabilità automatica** viene letto da hello scalabilità automatica motore toodetermine se tooscale verso l'alto o verso il basso. Contiene uno o più profili, informazioni sulla risorsa di destinazione hello e le impostazioni di notifica.

    - Un **profilo di scalabilità automatica** è una combinazione di:

        - **impostazione della capacità**, che indica minimo, massimo hello e valori predefiniti per numero di istanze.
        - **set di regole**, ognuna delle quali include un trigger (ora o metrica) e un'azione di scalabilità (verso l'alto o verso il basso).
        - **ricorrenza**, che indica quando il ridimensionamento automatico renderà effettivo il profilo.

        È possibile avere più profili che consentono di tootake cure diversi requisiti sovrapposti. È possibile avere profili di scalabilità automatica diversi per diverse ore del giorno o giorni della settimana hello, ad esempio.

    - Oggetto **impostazione notifica** definisce quali notifiche devono essere eseguiti quando un evento di scalabilità automatica si verifica in base che soddisfano criteri hello di uno dei profili dell'impostazione di scalabilità automatica hello. Scalabilità automatica possono inviare una notifica a uno o più indirizzi di posta elettronica oppure rendere tooone chiamate o più webhook.


![Struttura delle impostazioni, dei profili e delle regole di ridimensionamento automatico in Azure](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

Hello elenco completo dei campi configurabili e descrizioni è disponibile in hello [API REST di scalabilità automatica](https://msdn.microsoft.com/library/dn931928.aspx).

Per esempi di codice, vedere

* [Configurazione avanzata del ridimensionamento automatico con modelli di Resource Manager per set di scalabilità di macchine virtuali](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [API REST per il ridimensionamento automatico](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a>Ridimensionamento orizzontale e verticale
Scalabilità automatica solo Ridimensiona orizzontalmente, che è un aumento ("out") o diminuzione ("") nel numero hello di istanze di macchina virtuale.  Orizzontale è più flessibile in una situazione di cloud, in quanto consente toorun potenzialmente migliaia di macchine virtuali toohandle carico.

La scalabilità verticale è invece diversa, Si mantiene hello stesso numero di macchine virtuali, ma rende hello macchine virtuali più ("up") o meno ("giù") potente. La potenza è misurata in memoria, velocità della CPU, spazio su disco e così via.  Il ridimensionamento verticale presenta più limitazioni. È dipendente dal disponibilità hello di hardware più grande, rapidamente raggiunge un limite superiore e può variare in base a region. In genere anche scalabilità verticale richiede toostop una macchina virtuale e riavvia.

Per altre informazioni, vedere [Aumento delle prestazioni delle macchine virtuali di Azure tramite Automazione di Azure](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="methods-of-access"></a>Metodi di accesso
È possibile configurare il ridimensionamento automatico tramite:

* [Portale di Azure](insights-how-to-scale.md)
* [PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [Interfaccia della riga di comando multipiattaforma](insights-cli-samples.md#autoscale)
* [API REST di Monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a>Servizi supportati per il ridimensionamento automatico
| Service | Schema e documenti |
| --- | --- |
| App Web |[Ridimensionamento di app Web](insights-how-to-scale.md) |
| Servizi cloud |[Ridimensionamento automatico di un servizio cloud](../cloud-services/cloud-services-how-to-scale.md) |
| Macchine virtuali: classico |[Scaling Classic Virtual Machine Availability Sets (Ridimensionamento di set di disponibilità di macchine virtuale classiche)](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| Macchine virtuali: set di scalabilità Windows |[Ridimensionamento dei set di scalabilità di macchine virtuali in Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| Macchine virtuali: set di scalabilità Linux |[Ridimensionamento dei set di scalabilità di macchine virtuali in Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| Macchine virtuali: esempio Windows |[Configurazione avanzata del ridimensionamento automatico con modelli di Resource Manager per set di scalabilità di macchine virtuali](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sulla scalabilità automatica, utilizzare hello Autoscale Walkthroughs elencate in precedenza o consultare toohello seguenti risorse:

* [Metriche comuni per la scalabilità automatica di Monitoraggio di Azure](insights-autoscale-common-metrics.md)
* [Procedure consigliate per la scalabilità automatica in Monitoraggio di Azure](insights-autoscale-best-practices.md)
* [Utilizzo di scalabilità automatica azioni toosend posta elettronica e ai webhook notifiche di avviso](insights-autoscale-to-webhook-email.md)
* [API REST per il ridimensionamento automatico](https://msdn.microsoft.com/library/dn931953.aspx)
* [Risoluzione dei problemi di ridimensionamento automatico con set di scalabilità di macchine virtuali](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)
