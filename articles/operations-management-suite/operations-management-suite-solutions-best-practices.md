---
title: procedure consigliate per soluzioni aaaOMSManagement | Documenti Microsoft
description: 
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 08cf1c101e301d24fb5c2bf4bc02a978e508a198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a>Procedure consigliate per la creazione di soluzioni di gestione in Operations Management Suite (OMS) (anteprima)
> [!NOTE]
> Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima. Qualsiasi schema descritto di seguito è soggetto toochange.  

Questo articolo riporta le procedure consigliate per la [creazione di una soluzione di gestione](operations-management-suite-solutions-solution-file.md) in Operations Management Suite (OMS).  Queste informazioni verranno aggiornate quando saranno identificate procedure consigliate aggiuntive.

## <a name="data-sources"></a>Origini dati
- È possibile [configurare le origini dati con un modello di Resource Manager](../log-analytics/log-analytics-template-workspace-configuration.md), ma non devono essere incluse nel file della soluzione.  motivo di Hello è che la configurazione delle origini dati non è attualmente idempotente, vale a dire che la soluzione potrebbe sovrascrivere la configurazione esistente nell'area di lavoro dell'utente hello.<br><br>Ad esempio, la soluzione potrebbe richiedere gli eventi di avviso e di errore dal log eventi dell'applicazione hello.  Se si specifica questo come un'origine dati nella soluzione, si rischia di rimozione di informazioni eventi se hello utente dispone di questa configurazione nell'area di lavoro.  Se sono inclusi tutti gli eventi, quindi si potrebbe essere raccolta numero eccessivo di eventi informazioni nell'area di lavoro dell'utente hello.

- Se la soluzione richiede dati da una delle origini di dati standard hello, è necessario definire questa come prerequisito.  Stato nella documentazione di tale cliente hello necessario configurare hello origine dati in modo autonomo.  
- Aggiungere un [verifica del flusso di dati](../log-analytics/log-analytics-view-designer-tiles.md) messaggio tooany l'utente di hello tooinstruct soluzione nelle viste origini dati che toobe necessità configurato per i dati necessari toobe raccolti.  Questo messaggio viene visualizzato nel riquadro hello della vista hello quando non viene trovati i dati necessari.


## <a name="runbooks"></a>Runbook
- Aggiungere un [pianificazione di automazione](../automation/automation-schedules.md) per ogni runbook nella soluzione che deve toorun in una pianificazione.
- Includere hello [IngestionAPI modulo](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) in toobe la soluzione usata dai runbook scrittura repository Analitica Log toohello dei dati.  Configurare la soluzione di hello troppo[riferimento](operations-management-suite-solutions-solution-file.md#solution-resource) questa risorsa in modo che rimanga se soluzione hello viene rimossa.  Questo consente più soluzioni tooshare hello modulo.
- Utilizzare [le variabili di automazione](../automation/automation-schedules.md) tooprovide valori soluzione toohello che gli utenti possono avere toochange in un secondo momento.  Anche se la soluzione hello variabile hello toocontain configurato, il valore può ancora essere modificato.

## <a name="views"></a>Visualizzazioni
- Tutte le soluzioni devono includere una singola visualizzazione che viene visualizzata nel portale dell'utente hello.  Hello vista può contenere più [parti visualizzazione](../log-analytics/log-analytics-view-designer-parts.md) tooillustrate diversi set di dati.
- Aggiungere un [verifica del flusso di dati](../log-analytics/log-analytics-view-designer-tiles.md) messaggio tooany l'utente di hello tooinstruct soluzione nelle viste origini dati che toobe necessità configurato per i dati necessari toobe raccolti.
- Configurare la soluzione di hello troppo[contengono](operations-management-suite-solutions-solution-file.md#solution-resource) hello vista in modo che viene rimosso se la soluzione hello viene rimosso.

## <a name="alerts"></a>Avvisi
- Definire l'elenco di destinatari di hello come parametro nel file di soluzione hello in modo utente hello possibile definirli quando installano la soluzione hello.
- Configurare la soluzione di hello troppo[riferimento](operations-management-suite-solutions-solution-file.md#solution-resource) le regole di avviso in modo che tale utente può modificare la configurazione.  È possibile toomake modifiche, ad esempio la modifica dell'elenco dei destinatari hello, la modifica di soglia hello di avviso hello o la disattivazione della regola di avviso hello. 


## <a name="next-steps"></a>Passaggi successivi
* Procedura dettagliata hello processo di base per [progettazione e creazione di una soluzione di gestione](operations-management-suite-solutions-creating.md).
* Informazioni su come troppo[creare un file di soluzione](operations-management-suite-solutions-solution-file.md).
* [Aggiungere avvisi e le ricerche salvate](operations-management-suite-solutions-resources-searches-alerts.md) tooyour soluzione di gestione.
* [Aggiungere visualizzazioni](operations-management-suite-solutions-resources-views.md) tooyour soluzione di gestione.
* [Aggiungere i runbook di automazione e altre risorse](operations-management-suite-solutions-resources-automation.md) tooyour soluzione di gestione.

