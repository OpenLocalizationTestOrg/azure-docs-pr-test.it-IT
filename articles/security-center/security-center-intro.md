---
title: aaaIntroduction tooAzure Centro sicurezza PC | Documenti Microsoft
description: "Informazioni sul Centro sicurezza di Azure, le funzionalità principali e il funzionamento."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a>Introduzione tooAzure Centro sicurezza
Informazioni sul Centro sicurezza di Azure, le funzionalità principali e il funzionamento.

> [!NOTE]
> A partire da anticipata giugno 2017, centro di sicurezza verrà utilizzata toocollect Microsoft Monitoring Agent hello e archiviare i dati. Vedere [migrazione della piattaforma Azure sicurezza Center](security-center-platform-migration.md) toolearn altre. informazioni di Hello in questo articolo rappresentano funzionalità Centro sicurezza dopo la transizione toohello Microsoft Monitoring Agent.
>
>

## <a name="what-is-azure-security-center"></a>Che cos'è il Centro sicurezza di Azure?
 Centro sicurezza PC consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sulla protezione hello delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

## <a name="key-capabilities"></a>Funzionalità principali
 Centro sicurezza PC offre minaccia di semplice utilizzo ed efficace funzionalità di prevenzione, rilevamento e risposta che vengono compilate in tooAzure. Funzionalità principali:

| Fase | Funzionalità |
| --- | --- |
| Prevenzione |Monitoraggi hello lo stato di protezione delle risorse di Azure |
| Prevenzione | Definisce i criteri per le sottoscrizioni di Azure in base ai requisiti di sicurezza dell'azienda, tipi di hello di applicazioni che utilizzano e hello riservatezza dei dati |
| Prevenzione | Usa basate sui criteri di sicurezza indicazioni tooguide i proprietari tramite il processo di hello di implementazione necessari controlli |
| Prevenzione | Distribuisce rapidamente i servizi di sicurezza e i dispositivi di Microsoft e dei partner |
| Rilevamento |Raccoglie e analizza i dati di sicurezza di risorse di Azure, rete hello e soluzioni partner come programmi antimalware e i firewall automaticamente |
| Rilevamento | Usa globale minaccia intelligence da Microsoft hello di prodotti e servizi, hello Microsoft Digital Crimes Unit (DCU), Microsoft Security Response Center (MSRC) e un feed esterno |
| Rilevamento | Applica analisi avanzate, tra cui analisi del comportamento e di Machine Learning |
| Risposta |Fornisce eventi imprevisti o avvisi di sicurezza con priorità |
| Risposta | Offre informazioni dettagliate sui origine hello di attacco hello e risorse interessate |
| Risposta | Vengono suggerite alcune modalità toostop hello attacco corrente e impedire attacchi futuri |

## <a name="introductory-walkthrough"></a>Procedura dettagliata introduttiva

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione. Questo argomento non costituisce una guida dettagliata.
>
>

 Tramite il Centro sicurezza PC hello [portale di Azure](https://azure.microsoft.com/features/azure-portal/). [Accedi al portale toohello](https://portal.azure.com). Nel menu del portale principale hello, scorrere toohello **Centro sicurezza PC** opzione o seleziona hello **Centro sicurezza PC** riquadro che è stato aggiunto in precedenza toohello dashboard del portale.

![Riquadro Sicurezza nel portale di Azure][1]

Nel Centro sicurezza è possibile impostare i criteri di sicurezza, monitorare le configurazioni di sicurezza e visualizzare gli avvisi di sicurezza.

### <a name="security-policies"></a>Criteri di sicurezza
È possibile definire i criteri per le sottoscrizioni di Azure in base a requisiti di sicurezza della società tooyour. È inoltre possibile personalizzare tali toohello tipi di applicazioni in uso o toohello riservatezza dei dati hello in ogni sottoscrizione. Ad esempio, le risorse usate per lo sviluppo o il test possono avere requisiti di sicurezza diversi da quelli delle applicazioni di produzione. Allo stesso modo, le applicazioni con dati regolamentati, come le informazioni personali, possono richiedere un livello di sicurezza più elevato.

> [!NOTE]
> toomodify un criterio di sicurezza, è necessario essere di un'amministratore della sicurezza hello sottoscrizione o proprietario o collaboratore. toolearn ulteriori informazioni sui ruoli e le operazioni consentite in Centro sicurezza PC, vedere [autorizzazioni nel Centro protezione Azure](security-center-permissions.md).
>
>

In hello **Centro sicurezza PC** blade, seleziona hello **criteri** riquadro per un elenco delle sottoscrizioni e dei gruppi di risorse.   

![Pannello Centro sicurezza][2]

In hello **criteri di sicurezza** pannello selezionare un criterio dettagli di sottoscrizione tooview hello.

**Raccolta dati** abilita la raccolta dei dati per i criteri di sicurezza. L'abilitazione fornisce:

* Analisi giornaliera di tutte le macchine virtuali (VM) supportate per il monitoraggio della sicurezza e le raccomandazioni.
* Raccolta di eventi di sicurezza per l'analisi e il rilevamento delle minacce.

> [!NOTE]
> Raccolta dei dati è configurata a livello di sottoscrizione hello.
>
>

Selezionare **criteri di prevenzione** tooopen hello **criteri di prevenzione** blade. **Mostra i consigli per** consente di scegliere i controlli di sicurezza hello che si desidera toomonitor e hello raccomandazioni che si desidera toosee in base alle esigenze di sicurezza hello di risorse hello sottoscrizione hello.

### <a name="security-recommendations"></a>Suggerimenti per la sicurezza
 Centro sicurezza PC analizza lo stato di sicurezza hello le risorse di Azure tooidentify potenziali vulnerabilità della protezione. Un elenco di suggerimenti in modo semplificato il processo di hello di configurazione di controlli necessari. Tra gli esempi sono inclusi:

* Provisioning antimalware toohelp identificare e rimuovere il software dannoso
* Configurazione di rete sicurezza e gruppi di regole toocontrol traffico tooVMs
* Il provisioning dei firewall applicazione web toohelp difendersi da attacchi che le applicazioni web di destinazione
* Distribuzione degli aggiornamenti di sistema mancanti
* Indirizzamento delle configurazioni del sistema operativo che non corrispondono a hello consiglia le linee di base

Fare clic su hello **indicazioni** riquadro per un elenco di indicazioni. Fare clic su ogni raccomandazione tooview ulteriori informazioni o un problema di hello tootake azione tooresolve.

![Raccomandazioni di sicurezza nel Centro sicurezza di Azure][5]

### <a name="security-state-of-azure-resources"></a>Stato di sicurezza delle risorse di Azure
Hello **prevenzione** sezione dashboard hello Mostra hello generali di sicurezza dell'ambiente hello dal tipo di risorsa, tra cui le macchine virtuali, applicazioni web e altre risorse.   

Selezionare un tipo di risorsa in **prevenzione** tooview ulteriori informazioni, incluso un elenco di qualsiasi potenziali vulnerabilità di sicurezza che sono stati identificati. (**Calcolo** sia selezionata nel seguente esempio hello.)

![Riquadro Integrità delle risorse][6]

### <a name="security-alerts"></a>Avvisi di sicurezza
 Centro sicurezza PC automaticamente raccoglie, analizza e consente di integrare dati di log da risorse di Azure, rete hello e soluzioni partner come programmi antimalware e firewall. Quando vengono rilevate minacce, viene creato un avviso di sicurezza. Ad esempio, è compreso il rilevamento di:

* VM compromesse in comunicazione con indirizzi IP dannosi noti
* Malware avanzato rilevato tramite Segnalazione errori Windows
* Attacchi di forza bruta alle VM
* Avvisi di sicurezza da programmi antimalware e firewall integrati

Facendo clic su hello **degli avvisi di sicurezza** riquadro Visualizza un elenco di avvisi con priorità.

![Avvisi di sicurezza][7]

Selezionare un avviso per visualizzare ulteriori informazioni su attacco hello e i suggerimenti su come tooremediate è.

![Dettagli dell'avviso di sicurezza][8]

### <a name="partner-solutions"></a>Soluzioni partner
Hello **soluzioni Partner** riquadro consente di monitorare in uno stato di sicurezza immediatamente hello partner delle soluzioni dell'utente è integrato con la sottoscrizione di Azure. Centro sicurezza PC consente di visualizzare gli avvisi provenienti da soluzioni hello.

Seleziona hello **soluzioni Partner** riquadro. Viene visualizzato un pannello contenente un elenco di tutte le soluzioni dei partner connessi.

![Soluzioni partner][9]

## <a name="get-started"></a>Attività iniziali
tooget avviato con il Centro sicurezza PC, è necessario tooMicrosoft una sottoscrizione Azure. Il Centro sicurezza viene abilitato con la sottoscrizione di Azure. Se non si ha una sottoscrizione, è possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).

 Tramite il Centro sicurezza PC hello [portale di Azure](https://azure.microsoft.com/features/azure-portal/). Vedere hello [documentazione portale](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn altre.

[Introduzione a Centro sicurezza di Azure](security-center-get-started.md) rapidamente in modo semplificato i componenti di monitoraggio della protezione e gestione dei criteri di hello del Centro sicurezza PC.

## <a name="next-steps"></a>Passaggi successivi
In questo documento, sono state introdotte tooSecurity Center, le funzionalità chiave e la modalità di avvio tooget. toolearn informazioni, vedere hello seguenti risorse:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) , informazioni come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni facilitano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
- [Sicurezza dei dati nel Centro sicurezza di Azure](security-center-data-security.md): informazioni sulla gestione e la protezione dei dati nel Centro sicurezza.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) , ottenere informazioni e notizie sicurezza di Azure hello.

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
