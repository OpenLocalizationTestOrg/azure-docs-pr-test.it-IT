---
title: aaaAzure Centro sicurezza PC e macchine virtuali di Azure | Documenti Microsoft
description: Questo documento consente di toounderstand come Centro sicurezza di Azure possono proteggere il macchine virtuali di Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/24/2017
ms.author: yurid
ms.openlocfilehash: d5e80e9341263a57f3100cb032a066f037e913a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines"></a>Centro sicurezza di Azure e macchine virtuali di Azure
[Centro sicurezza di Azure](https://azure.microsoft.com/services/security-center/) consente di impedire, rilevare e rispondere toothreats. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

Questo articolo illustra come il Centro sicurezza consente di proteggere le macchine virtuali (VM) di Azure.

## <a name="why-use-security-center"></a>Perché usare il Centro sicurezza?
Il Centro sicurezza consente di proteggere i dati delle macchine virtuali di Azure fornendo visibilità sulle impostazioni di sicurezza di queste ultime. Quando il Centro sicurezza PC protegge le macchine virtuali, saranno disponibile hello seguenti funzionalità:

* Le regole di configurazione delle impostazioni di sicurezza del sistema operativo (sistema operativo) con hello consigliati
* Aggiornamenti della sicurezza del sistema e altri aggiornamenti di importanza critica eventualmente mancanti
* Consigli per la protezione degli endpoint
* Convalida della crittografia del disco
* Valutazione della vulnerabilità e correzioni
* Introduzione al rilevamento delle minacce

Inoltre toohelping proteggere le macchine virtuali di Azure, il Centro sicurezza PC fornisce inoltre il monitoraggio della protezione e gestione per i servizi Cloud, servizi di App, le reti virtuali e altro ancora. 

> [!NOTE]
> Vedere [tooAzure introduzione Centro sicurezza PC](security-center-intro.md) toolearn informazioni sul Centro sicurezza di Azure.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
tooget avviato con il centro di sicurezza di Azure, si sarà necessario tooknow e considerare hello seguenti:

* È necessario disporre tooMicrosoft una sottoscrizione Azure. Per altre informazioni sui livelli gratuito e standard del Centro sicurezza, vedere [Centro sicurezza Prezzi](https://azure.microsoft.com/pricing/details/security-center/).
* Pianificare l'adozione del Centro sicurezza PC, vedere [Guida alla pianificazione e le operazioni di Centro sicurezza di Azure](security-center-planning-and-operations-guide.md) toolearn ulteriori informazioni sulle considerazioni sulla pianificazione e le operazioni.
* Per informazioni relative al supporto dei sistemi operativi, vedere [Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md). 

## <a name="set-security-policy"></a>Impostare i criteri di sicurezza
Toobe esigenze di raccolta dati abilitati in modo che Centro sicurezza di Azure può raccogliere informazioni di hello deve tooprovide indicazioni e gli avvisi generati in base ai criteri di sicurezza hello che è configurare. Nella figura hello seguente, è possibile vedere che **la raccolta dei dati** è stata attivata **su**.

Un criterio di sicurezza definisce il set di hello di controlli che sono consigliati per le risorse nel gruppo di risorse o di sottoscrizione specificato hello. Prima di abilitare i criteri di sicurezza, è necessario disporre di raccolta dati abilitata, il Centro sicurezza PC raccoglie dati dalle macchine virtuali in ordine tooassess allo stato di sicurezza, fornire consigli sulla sicurezza e gli avvisi toothreats. Centro sicurezza PC, definire i criteri per le sottoscrizioni di Azure o i gruppi di risorse in base della società tooyour le esigenze di sicurezza e riservatezza dei dati di hello in ogni sottoscrizione o tipo hello delle applicazioni. 

![Criteri di sicurezza](./media/security-center-virtual-machine/security-center-virtual-machine-fig1.png)

> [!NOTE]
> toolearn informazioni su ogni **criteri di prevenzione** disponibili, vedere [impostare criteri di sicurezza](security-center-policies.md) articolo.
> 
> 

## <a name="manage-security-recommendations"></a>Gestire le raccomandazioni per la sicurezza
Centro sicurezza PC analizza lo stato di sicurezza hello delle risorse di Azure. Quando identifica potenziali vulnerabilità della sicurezza, crea raccomandazioni. indicazioni Hello semplificato il processo di hello di configurazione dei controlli di hello necessita.

Dopo aver impostato un criterio di sicurezza, il Centro sicurezza PC analizza stato protezione hello i potenziali vulnerabilità tooidentify di risorse. indicazioni Hello vengono visualizzati in un formato di tabella in cui ogni riga rappresenta una raccomandazione particolare. tabella Hello riportata di seguito vengono forniti alcuni esempi di indicazioni per macchine virtuali di Azure e a cosa ciascuno di essi verrà se lo si applica. Quando si seleziona un suggerimento, verranno fornite informazioni che illustra come tooimplement hello indicazione del Centro sicurezza PC.

| Raccomandazione | Descrizione |
| --- | --- |
| [Abilita la raccolta di dati per le sottoscrizioni](security-center-enable-data-collection.md) |Si consiglia di attivare la raccolta dei dati nei criteri di sicurezza hello per ognuna delle sottoscrizioni e tutte le macchine virtuali (VM) le sottoscrizioni. |
| [Remediate OS vulnerabilities (Risolvi vulnerabilità del sistema operativo)](security-center-remediate-os-vulnerabilities.md) |Si consiglia di allineare le configurazioni del sistema operativo con hello consiglia le regole di configurazione, ad esempio, non consentire toobe le password salvate. |
| [Applicare gli aggiornamenti di sistema](security-center-apply-system-updates.md) |Consiglia di distribuire la protezione del sistema mancanti e gli aggiornamenti critici tooVMs. |
| [Riavvia dopo gli aggiornamenti del sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Si consiglia di riavviare un processo di hello VM toocomplete di applicazione degli aggiornamenti di sistema. |
| [Installa Endpoint Protection](security-center-install-endpoint-protection.md) |Si consiglia di eseguire il provisioning tooVMs programmi antimalware (solo per macchine virtuali Windows). |
| [Risolvi gli avvisi sull'integrità di Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Si consiglia di correggere gli errori relativi alla protezione degli endpoint. |
| [Abilita l'agente di macchine virtuali](security-center-enable-vm-agent.md) |Abilita agente VM di hello è toosee che richiedono che le macchine virtuali. Hello agente della macchina virtuale debba essere installato nelle macchine virtuali in patch tooprovision ordine l'analisi, l'analisi della linea di base e i programmi antimalware. Hello agente VM viene installato per impostazione predefinita per le macchine virtuali distribuite da hello Azure Marketplace. articolo Hello [agente VM ed estensioni-parte 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) vengono fornite informazioni su come tooinstall hello agente della macchina virtuale. |
| [Applicare Crittografia dischi](security-center-apply-disk-encryption.md) |Suggerisce di crittografare i dischi delle macchine virtuali con Crittografia dischi di Azure (VM Windows e Linux). La crittografia è consigliabile per hello del sistema operativo e i volumi di dati di una macchina virtuale. |
| [La valutazione della vulnerabilità non è installata](security-center-vulnerability-assessment-recommendations.md) |Consiglia di installare una soluzione di valutazione della vulnerabilità nella VM. |
| [Correggi le vulnerabilità](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Consente le vulnerabilità di sistema e dell'applicazione toosee rilevate dalla soluzione di valutazione delle vulnerabilità hello installato nella macchina virtuale. |

> [!NOTE]
> toolearn informazioni sulle indicazioni, vedere [gestione consigli sulla sicurezza](security-center-recommendations.md) articolo.
> 
> 

## <a name="monitor-security-health"></a>Monitorare l'integrità della sicurezza
Dopo aver abilitato [criteri di sicurezza](security-center-policies.md) per le risorse di una sottoscrizione, il Centro sicurezza PC analizzerà le risorse tooidentify potenziali vulnerabilità della sicurezza hello.  È possibile visualizzare lo stato di sicurezza hello delle risorse, insieme a eventuali problemi di hello **integrità delle risorse di sicurezza** blade. Quando fa clic su **macchine virtuali** in hello **protezione delle risorse** riquadro integrità, hello **macchine virtuali** pannello verrà aperto con consigli per le macchine virtuali. 

![Integrità della sicurezza](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a>Gestire e rispondere toosecurity avvisi
Centro sicurezza PC automaticamente raccoglie, analizza e consente di integrare dati di log da risorse di Azure, rete hello e soluzioni partner connesso (ad esempio i firewall ed endpoint protection soluzioni), minacce reali toodetect e ridurre i falsi positivi. Mediante l'utilizzo di un'aggregazione diverse di [funzionalità di rilevamento](security-center-detection-capabilities.md), centro di sicurezza è in grado di toogenerate priorità avviso di sicurezza toohelp rapidamente esaminare hello problema e fornire indicazioni sul tooremediate possibili attacchi.

![Avvisi di sicurezza](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

Selezionare un toolearn avviso di sicurezza ulteriori informazioni su eventi hello che ha attivato avviso hello e cosa, se presente, i passaggi necessari per necessario tootake tooremediate un attacco. Gli avvisi di sicurezza vengono raggruppati per [tipo](security-center-alerts-type.md) e data.

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.

