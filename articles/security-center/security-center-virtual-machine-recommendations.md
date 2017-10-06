---
title: aaaProtecting le macchine virtuali nel Centro sicurezza di Azure | Documenti Microsoft
description: "Questo documento illustra le raccomandazioni presenti nel Centro sicurezza di Azure che facilitano la protezione delle macchine virtuali e garantiscano la conformità ai criteri di sicurezza."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 926c04974f61215b4a3e02646f23dafb87c793e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a>Protezione delle macchine virtuali nel Centro sicurezza di Azure
Centro sicurezza di Azure consente di analizzare lo stato di sicurezza hello delle risorse di Azure. Quando il Centro sicurezza PC identifica potenziali vulnerabilità di sicurezza, viene creato indicazioni che consentono di eseguire il processo di hello di configurazione dei controlli di hello necessita.  Consigli si applicano a tipi di risorse tooAzure: macchine virtuali (VM), rete, SQL e le applicazioni.

Questo articolo illustra indicazioni applicabili tooVMs.  Le raccomandazioni sulle macchine virtuali sono incentrate sulla raccolta dei dati, sull'applicazione degli aggiornamenti del sistema, sul provisioning di antimalware, sulla crittografia dei dischi delle macchine virtuali e altro ancora.  Tabella di hello utilizzare riportata di seguito come un riferimento di toohelp comprendere indicazioni VM disponibili hello e a cosa ciascuno di essi verrà se lo si applica.

## <a name="available-vm-recommendations"></a>Raccomandazioni disponibili per le macchine virtuali
| Raccomandazione | Descrizione |
| --- | --- |
| [Abilita la raccolta di dati per le sottoscrizioni](security-center-enable-data-collection.md) |Si consiglia di attivare la raccolta dei dati nei criteri di sicurezza hello per ognuna delle sottoscrizioni e tutte le macchine virtuali (VM) le sottoscrizioni. |
| [Abilitare la crittografia per l'account di archiviazione di Azure](security-center-enable-encryption-for-storage-account.md) | Consiglia di abilitare la crittografia del servizio Archiviazione di Azure per i dati inattivi Crittografia del servizio di archiviazione (SSE) funziona mediante la crittografia dei dati di hello quando ne viene scritto archiviazione tooAzure e li decrittografa prima di recupero. SSE è attualmente disponibile solo per hello servizio Blob di Azure e può essere utilizzato per i BLOB in blocchi, BLOB di pagine e BLOB di aggiunta. vedere, più toolearn [la crittografia del servizio di archiviazione per i dati inattivi](../storage/common/storage-service-encryption.md).</br>La crittografia del servizio Archiviazione di Azure è supportata solo negli account di archiviazione di Resource Manager. Gli account di archiviazione classici non sono attualmente supportati. hello toounderstand classico e modelli di distribuzione di gestione delle risorse, vedere [modelli di distribuzione Azure](../azure-classic-rm.md). |
| [Remediate OS vulnerabilities (Risolvi vulnerabilità del sistema operativo)](security-center-remediate-os-vulnerabilities.md) |Si consiglia di allineare le configurazioni del sistema operativo con hello consiglia le regole di configurazione, ad esempio, non consentire toobe le password salvate. |
| [Applicare gli aggiornamenti di sistema](security-center-apply-system-updates.md) |Consiglia di distribuire la protezione del sistema mancanti e gli aggiornamenti critici tooVMs. |
| [Applicare un controllo di accesso alla rete JIT](security-center-just-in-time.md) | Consiglia di applicare l'accesso Just-In-Time alla macchina virtuale. Hello solo nella funzione di tempo è in anteprima e disponibile nel livello Standard del Centro sicurezza PC hello. Vedere [prezzi](security-center-pricing.md) toolearn ulteriori informazioni su Centro sicurezza di livelli di prezzo. |
| [Riavvia dopo gli aggiornamenti del sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Si consiglia di riavviare un processo di hello VM toocomplete di applicazione degli aggiornamenti di sistema. |
| [Installa Endpoint Protection](security-center-install-endpoint-protection.md) |Si consiglia di eseguire il provisioning tooVMs programmi antimalware (solo per macchine virtuali Windows). |
| [Risolvi gli avvisi sull'integrità di Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Si consiglia di correggere gli errori relativi alla protezione degli endpoint. |
| [Abilita l'agente di macchine virtuali](security-center-enable-vm-agent.md) |Abilita agente VM di hello è toosee che richiedono che le macchine virtuali. Hello agente della macchina virtuale debba essere installato nelle macchine virtuali in patch tooprovision ordine l'analisi, l'analisi della linea di base e i programmi antimalware. Hello agente VM viene installato per impostazione predefinita per le macchine virtuali distribuite da hello Azure Marketplace. articolo Hello [agente VM ed estensioni-parte 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) vengono fornite informazioni su come tooinstall hello agente della macchina virtuale. |
| [Applicare Crittografia dischi](security-center-apply-disk-encryption.md) |Suggerisce di crittografare i dischi delle macchine virtuali con Crittografia dischi di Azure (VM Windows e Linux). La crittografia è consigliabile per hello del sistema operativo e i volumi di dati di una macchina virtuale. |
| [Aggiornare la versione sistema operativo](security-center-update-os-version.md) |Consiglia di aggiornare versione di hello del sistema operativo (sistema operativo) per il servizio Cloud toohello più recente disponibile per la famiglia di sistemi operativi.  toolearn ulteriori informazioni sui servizi Cloud, vedere hello [Cenni preliminari sui servizi Cloud](../cloud-services/cloud-services-choose-me.md). |
| [La valutazione della vulnerabilità non è installata](security-center-vulnerability-assessment-recommendations.md) |Consiglia di installare una soluzione di valutazione della vulnerabilità nella VM. |
| [Correggi le vulnerabilità](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Consente le vulnerabilità di sistema e dell'applicazione toosee rilevate dalla soluzione di valutazione delle vulnerabilità hello installato nella macchina virtuale. |

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni sui suggerimenti che si applicano tooother tipi di risorse di Azure, vedere l'esempio hello:

* [Protecting your applications in Azure Security Center](security-center-application-recommendations.md)
* [Protezione della rete nel Centro sicurezza di Azure](security-center-network-recommendations.md)
* [Protezione del servizio SQL di Azure nel Centro sicurezza di Azure](security-center-sql-service-recommendations.md)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
