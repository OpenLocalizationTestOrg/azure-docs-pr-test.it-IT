---
title: Rilevare i problemi dei dispositivi nella soluzione di monitoraggio remoto - Azure | Microsoft Docs
description: Questa esercitazione mostra come usare regole e azioni per rilevare automaticamente problemi dei dispositivi in base alle soglie nella soluzione di monitoraggio remoto.
services: 
suite: iot-suite
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-suite
ms.date: 12/12/2017
ms.topic: article
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.workload: NA
ms.openlocfilehash: e00c4ab2fc8bb13a765f7c2154555607dddfc651
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2017
---
# <a name="detect-issues-using-threshold-based-rules"></a>Rilevare i problemi usando regole basate su soglie

Questa esercitazione mostra le funzionalità del motore regole nella soluzione di monitoraggio remoto. Per presentare queste funzionalità, l'esercitazione usa uno scenario nell'applicazione IoT Contoso.

Contoso ha implementato una regola che genera un allarme critico quando la pressione segnalata da un dispositivo **Chiller** (Refrigeratore) è maggiore di 250 PSI. In qualità di operatore, è necessario identificare i dispositivi **Chiller** (Refrigeratore) che possono avere sensori problematici osservando i picchi di pressione iniziali. Per identificare questi dispositivi, è necessario creare una regola per generare un avviso quando la pressione è maggiore di 150 PSI.

In questa esercitazione si apprenderà come:

>[!div class="checklist"]
> * Visualizzare le regole nella soluzione
> * Creare una nuova regola
> * Modificare una regola esistente
> * Eliminare una regola

## <a name="prerequisites"></a>Prerequisiti

Per seguire questa esercitazione, è necessaria un'istanza distribuita della soluzione di monitoraggio remoto nella sottoscrizione di Azure.

Se la soluzione di monitoraggio remoto non è stata ancora distribuita, è necessario completare l'esercitazione [Distribuire la soluzione preconfigurata di monitoraggio remoto](iot-suite-remote-monitoring-deploy.md).

## <a name="view-the-rules-in-your-solution"></a>Visualizzare le regole nella soluzione

Il **regole e le azioni** pagina nella soluzione viene visualizzato un elenco di tutte le regole corrente:

![Pagina Rules & Actions (Regole e azioni)](media/iot-suite-remote-monitoring-automate/rulesactions.png)

Per visualizzare solo le regole valide per i dispositivi **Chiller** (Refrigeratore), applicare un filtro:

![Filtrare l'elenco delle regole](media/iot-suite-remote-monitoring-automate/rulesactionsfilter.png)

Quando si seleziona una regola nell'elenco, è possibile visualizzare altre informazioni sulla regola o modificarla:

![Visualizzare i dettagli delle regole](media/iot-suite-remote-monitoring-automate/rulesactionsdetail.png)

Per disabilitare, abilitare o eliminare una o più regole, selezionare più regole nell'elenco:

![Selezionare più regole](media/iot-suite-remote-monitoring-automate/rulesactionsmultiselect.png)

## <a name="create-a-new-rule"></a>Creare una nuova regola

Per aggiungere una nuova regola che generi un avviso quando la pressione in un dispositivo **Chiller** (Refrigeratore) è maggiore di 150 PSI, scegliere **New rule** (Nuova regola):

![Creare una regola](media/iot-suite-remote-monitoring-automate/rulesactionsnewrule.png)

Usare i valori seguenti per creare la regola:

| Impostazione          | Valore                                 |
| ---------------- | ------------------------------------- |
| NOME             | Chiller warning (Avviso refrigeratore)                       |
| Sorgente           | **Chillers** gruppo di dispositivi             |
| Field (Campo)    | pressure                              |
| Operator (Operatore) | Maggiore di                          |
| Value (Valore)    | 150                                   |
| Livello di gravità   | Avviso                               |
| DESCRIZIONE      | Chiller pressure has exceeded 150 PSI (La pressione del refrigeratore è maggiore di 150 PSI) |

Per salvare la nuova regola, scegliere **Apply** (Applica).

È possibile visualizzare quando la regola è attivata per il **regole e le azioni** pagina oppure il **Dashboard** pagina.

## <a name="edit-an-existing-rule"></a>Modificare una regola esistente

Per apportare una modifica a una regola esistente, selezionare la regola nell'elenco delle regole. Nel pannello **Rule Detail** (Dettagli regola) scegliere **Edit mode** (Modalità di modifica).

![Modificare una regola](media/iot-suite-remote-monitoring-automate/rulesactionsedit.png)

## <a name="disable-a-rule"></a>Disabilitare una regola

Per disattivare temporaneamente una regola, è possibile disabilitarla nell'elenco delle regole. Scegliere la regola da disabilitare e quindi scegliere **Disable** (Disabilita). Il valore di **Status** (Stato) per la regole nell'elenco cambia per indicare che la regola è ora disabilitata. È possibile riabilitare una regola precedentemente disabilitata usando la stessa procedura.

![Disabilitare una regola](media/iot-suite-remote-monitoring-automate/rulesactionsdisable.png)

È possibile abilitare e disabilitare più regole contemporaneamente selezionandone diverse nell'elenco.

## <a name="delete-a-rule"></a>Eliminare una regola

Per eliminare in modo permanente una regola, scegliere la regola nell'elenco delle regole e quindi scegliere **Delete** (Elimina).

È possibile eliminare più regole contemporaneamente selezionandone diverse nell'elenco.

## <a name="next-steps"></a>Passaggi successivi

Questa esercitazione ha mostrato come:

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * Visualizzare le regole nella soluzione
> * Creare una nuova regola
> * Modificare una regola esistente
> * Eliminare una regola

Ora che si è appreso come rilevare i problemi usando regole basate su soglie, i passaggi successivi consigliati consentono di apprendere come:

* [Gestire e configurare i dispositivi](./iot-suite-remote-monitoring-manage.md).
* [Risolvere e correggere i problemi dei dispositivi](./iot-suite-remote-monitoring-maintain.md).
* [Testare la soluzione con dispositivi simulati](iot-suite-remote-monitoring-test.md).

<!-- Next tutorials in the sequence -->