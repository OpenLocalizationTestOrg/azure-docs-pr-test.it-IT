---
title: Migrazione della piattaforma Centro protezione aaaAzure | Documenti Microsoft
description: "Questo documento illustra un modo toohello modifiche dati Centro sicurezza di Azure verrà raccolti."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a>Migrazione della piattaforma del Centro sicurezza di Azure

A partire da anticipata giugno 2017, Centro sicurezza di Azure presenta una importante modifica toohello modo sicurezza i dati vengono raccolti e archiviati.  Queste modifiche nuove funzionalità, come dati di protezione ricerca tooeasily hello possibilità di sbloccare e meglio allineata con altri servizi di gestione Azure e monitoraggio dei servizi.

> [!NOTE]
> migrazione della piattaforma Hello dovrebbe influire le risorse di produzione e non sono necessarie da parte degli azioni.


## <a name="whats-happening-during-this-platform-migration"></a>Cosa succede durante la migrazione della piattaforma?

Centro sicurezza PC utilizzato in precedenza, dati di hello Azure Monitoring Agent toocollect protezione dalle macchine virtuali. Sono incluse informazioni sulle configurazioni di sicurezza, che sono utilizzati tooidentify vulnerabilità, e gli eventi di sicurezza sono utilizzati toodetect minacce. Questi dati venivano archiviati negli account di archiviazione in Azure.

In futuro, che il Centro sicurezza PC utilizza hello Microsoft Monitoring Agent: si tratta di hello stesso agente usato dal servizio di Log Analitica e hello Operations Management Suite. Dati raccolti dall'agente vengono archiviati in un esistente *Log Analitica* [dell'area di lavoro](../log-analytics/log-analytics-manage-access.md) associato alla sottoscrizione di Azure o di un nuovo aree di lavoro, tenendo conto hello geolocation di hello VM .

## <a name="agent"></a>Agente

Come parte della transizione hello, hello Microsoft Monitoring Agent (per [Windows](../log-analytics/log-analytics-windows-agents.md) o [Linux](../log-analytics/log-analytics-linux-agents.md)) è installato in tutte le macchine virtuali di Azure da cui viene attualmente raccolto dati.  Se si avvale di hello che VM dispone già di hello Microsoft Monitoring Agent installato, il Centro sicurezza PC hello corrente installato l'agente.

Per un periodo di tempo (in genere pochi giorni), entrambi gli agenti verranno eseguito side-by tooensure transizione senza alcuna perdita di dati. In questo modo Microsoft toovalidate che hello nuova pipeline di dati sia operativo prima della sospensione di utilizzo della pipeline corrente hello. Una volta verificato, hello Azure Monitoring Agent verrà rimossa dalle macchine virtuali. senza che sia richiesto alcun intervento da parte dell'utente. Verrà inviato un messaggio e-mail quando tutti i clienti sono stati migrati.
 
Non è consigliabile disinstallazione manuale di hello Azure Monitoring Agent durante la migrazione di hello come potrebbe comportare gap nei dati di sicurezza. Contattare il [Servizio Supporto Tecnico Clienti Microsoft](https://support.microsoft.com/contactus/) per ulteriore assistenza. 

Microsoft Monitoring Agent per Windows Hello è necessario utilizzare la porta TCP 443, leggere [Centro protezione Azure Troubleshooting Guide](security-center-troubleshooting-guide.md) per ulteriori informazioni.


> [!NOTE] 
> Poiché hello Microsoft Monitoring Agent può essere utilizzato da altri management di Azure e monitoraggio dei servizi, agente hello non verrà disinstallato automaticamente quando si disattiva la raccolta dei dati del Centro sicurezza PC. Tuttavia, è possibile disinstallare agente hello manualmente se necessario.

## <a name="workspace"></a>Area di lavoro

Come descritto in precedenza, dati raccolti da Microsoft Monitoring Agent (per conto di centro di sicurezza) vengono archiviati in entrambi un Analitica Log esistente hello aree di lavoro associato alla sottoscrizione di Azure o di un nuovo aree di lavoro, tenendo hello account georilevazione di hello macchina virtuale.

In hello portale di Azure, è possibile visualizzare un elenco delle aree di lavoro Log Analitica, inclusi quelli creati dal Centro sicurezza PC toosee. Per le nuove aree di lavoro verrà creato un gruppo di risorse correlato. Entrambi seguono questa convenzione di denominazione:

- Area di lavoro: *DefaultWorkspace-[subscription-ID]-[geo]*
- Gruppo di risorse: *DefaultResouceGroup-[geo]* 
 
Per le aree di lavoro create dal Centro sicurezza, i dati vengono conservati per 30 giorni. Per aree di lavoro esistente, memorizzazione si basa sull'area di lavoro hello tariffario.

> [!NOTE]
> I dati raccolti in precedenza dal Centro sicurezza rimangono negli account di archiviazione. Al termine della migrazione hello, è possibile eliminare questi account di archiviazione.

### <a name="oms-security-solution"></a>Soluzione di sicurezza di OMS 

Per i clienti esistenti che non dispongono della soluzione di sicurezza di OMS, la soluzione viene installata automaticamente nell'area di lavoro, ma solo per le macchine virtuali di Azure. Non disinstallare questa soluzione, dal momento che non è disponibile alcuna correzione automatica se questa operazione viene eseguita dalla console di gestione di OMS.


## <a name="other-updates"></a>Altri aggiornamenti

In combinazione con la migrazione di piattaforma hello, stiamo rollout altri aggiornamenti secondari:

- Saranno supportate altre versioni del sistema operativo. Vedere l'elenco di hello [qui](security-center-faq.md#virtual-machines).
- verrà espanso l'elenco di Hello delle vulnerabilità del sistema operativo. Vedere l'elenco di hello [qui](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
- I [prezzi](https://azure.microsoft.com/pricing/details/security-center/) verranno ripartiti su base oraria (in precedenza la ripartizione era su base giornaliera), con conseguente risparmio sui costi per alcuni clienti.
- Verrà richiesto e abilitata automaticamente per i clienti nel piano tariffario Standard hello la raccolta dei dati.
- Il Centro sicurezza di Azure avvierà l'individuazione di soluzioni antimalware che non sono state distribuite tramite le estensioni di Azure. L'individuazione di Symantec Endpoint Protection e Defender per Windows 2016 sarà disponibile per prima.
- Criteri di prevenzione e le notifiche sono configurabili in hello solo *sottoscrizione* livello, ma prezzi può ancora essere impostato su hello *gruppo di risorse* livello

