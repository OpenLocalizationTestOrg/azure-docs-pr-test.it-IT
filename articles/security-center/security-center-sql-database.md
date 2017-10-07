---
title: servizio Centro sicurezza PC e i Database SQL di Azure aaaAzure | Documenti Microsoft
description: Questo articolo illustra come il Centro sicurezza consente di proteggere i database nel servizio Database SQL di Azure.
services: sql-database
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f109adfd-daed-4257-9692-2042a1399480
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 173590500f0ce64140f214ada24b9692e01dbd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-sql-database-service"></a>Centro sicurezza di Azure e servizio Database SQL di Azure
[Centro sicurezza di Azure](https://azure.microsoft.com/documentation/services/security-center/) consente di impedire, rilevare e rispondere toothreats. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

Questo articolo illustra come il Centro sicurezza consente di proteggere i database nel servizio Database SQL di Azure.

## <a name="why-use-security-center"></a>Perché usare il Centro sicurezza?
Centro sicurezza PC consente di proteggere i dati nel Database SQL, fornendo visibilità sicurezza hello del server e database. Con il Centro sicurezza è possibile:

* Definire i criteri per la crittografia e il controllo del database SQL.
* Monitoraggio della sicurezza hello di risorse del Database SQL per tutte le sottoscrizioni.
* Identificare e correggere rapidamente i problemi di sicurezza.
* Integrare gli avvisi generati dal [rilevamento delle minacce del database SQL di Azure](../sql-database/sql-database-threat-detection.md).

Inoltre toohelping proteggere le risorse del Database SQL, Centro sicurezza PC fornisce inoltre il monitoraggio della protezione e gestione per macchine virtuali di Azure, servizi Cloud, servizi di App, le reti virtuali e altro ancora. Per altre informazioni sul Centro sicurezza, fare clic [qui](security-center-intro.md).

## <a name="prerequisites"></a>Prerequisiti
tooget avviato con il Centro sicurezza PC, è necessario disporre di un tooMicrosoft sottoscrizione Azure. livello gratuito di Hello del Centro sicurezza PC è abilitata con la sottoscrizione. Per altre informazioni sui livelli gratuito e standard del Centro sicurezza, vedere [Centro sicurezza Prezzi](https://azure.microsoft.com/pricing/details/security-center/).

Il Centro sicurezza supporta l'accesso in base al ruolo. toolearn più informazioni sul controllo accesso basato sui ruoli (RBAC) in Azure, vedere [controllo di accesso basato sui ruoli di Azure Active Directory](../active-directory/role-based-access-control-configure.md). Hello domande frequenti su Centro di sicurezza vengono fornite informazioni su [la modalità di gestione autorizzazioni in Centro sicurezza PC](security-center-faq.md#permissions).

## <a name="access-security-center"></a>Accedere al Centro sicurezza
Tramite il Centro sicurezza PC hello [portale di Azure](https://azure.microsoft.com/features/azure-portal/). [Accedi al portale toohello](https://portal.azure.com/) e seleziona hello **opzione Centro sicurezza PC**.

![Opzione Centro sicurezza][1]

Hello **Centro sicurezza PC** apre blade.
![Pannello Centro sicurezza][2]

## <a name="set-security-policy"></a>Impostare i criteri di sicurezza
Un criterio di sicurezza definisce il set di hello di controlli che sono consigliati per le risorse nel gruppo di risorse o di sottoscrizione specificato hello. Centro sicurezza PC, definire criteri per le sottoscrizioni o i gruppi di risorse in base della società tooyour le esigenze di sicurezza e riservatezza dei dati di hello in ogni sottoscrizione o tipo hello delle applicazioni.

È possibile impostare un criterio tooshow consigli per SQL transparent data encryption (TDE) e di controllo SQL.

* Quando si attiva **controllo SQL e minaccia rilevamento**, Centro sicurezza PC consiglia che il controllo di accesso tooAzure Database essere abilitato per la conformità avanzate di rilevamento e motivi di indagine.
* Quando si abilita la crittografia **SQL Transparent Data Encryption**, il Centro sicurezza suggerisce l'abilitazione della crittografia dati inattivi per il database SQL di Azure, i backup associati e file di log delle transazioni.

tooset un criterio di sicurezza, seleziona hello **criteri** riquadro nel Pannello di hello Centro sicurezza PC. In hello **criteri di sicurezza** blade, sottoscrizione selezionare hello in cui si desidera che Criteri di sicurezza tooenable hello. Selezionare **criteri di prevenzione** e attivare **su** hello consigli relativi alla sicurezza che si desidera toouse in questa sottoscrizione.
![Criteri di sicurezza][3]

vedere, più toolearn [impostare criteri di sicurezza](security-center-policies.md).

## <a name="manage-security-recommendation"></a>Gestire una raccomandazione di sicurezza
Centro sicurezza PC analizza periodicamente lo stato di sicurezza hello delle risorse di Azure. Quando identifica potenziali vulnerabilità della sicurezza, crea raccomandazioni. indicazioni Hello semplificato il processo di hello di configurazione dei controlli di hello necessita.

Dopo aver impostato un criterio di sicurezza, il Centro sicurezza PC analizza stato protezione hello i potenziali vulnerabilità tooidentify di risorse. indicazioni Hello vengono visualizzati in un formato di tabella in cui ogni riga rappresenta una raccomandazione particolare. Utilizzare hello nella tabella seguente come toohelp un riferimento che è comprendere hello disponibili indicazioni su Database SQL di Azure e quali ogni raccomandazione non se si applica. Selezionando una raccomandazione si viene reindirizzati tooan articolo che spiega come tooimplement hello indicazione del Centro sicurezza PC.

| Raccomandazione | Descrizione |
| --- | --- |
| [Enable Auditing &amp; Threat detection on SQL servers](security-center-enable-auditing-on-sql-servers.md) (Abilita il controllo e il rilevamento delle minacce nei server SQL) |Raccomanda di abilitare il controllo e il rilevamento delle minacce per i server di database SQL (solo per il servizio Database SQL; non prevede l'esecuzione di Microsoft SQL Server sulle macchine virtuali). |
| [Enable Auditing & Threat detection on SQL databases](security-center-enable-auditing-on-sql-databases.md) (Abilita il controllo e il rilevamento delle minacce nei database SQL) |Raccomanda di abilitare il controllo e il rilevamento delle minacce per i database del servizio database SQL (solo per il servizio Database SQL; non prevede l'esecuzione di Microsoft SQL Server sulle macchine virtuali). |
| [Abilita Transparent Data Encryption](security-center-enable-transparent-data-encryption.md) |Raccomanda di abilitare la crittografia per i database SQL (solo per il servizio Database SQL). |

toosee indicazioni per le risorse di Azure, seleziona hello **indicazioni** riquadro nel Pannello di hello Centro sicurezza PC. In hello **indicazioni** pannello, selezionare i dettagli toosee una raccomandazione. In questo esempio si seleziona **Enable Auditing & Threat detection on SQL servers** (Abilita il controllo e il rilevamento delle minacce nei server SQL).

![Raccomandazioni][4]

Come indicato di seguito viene mostrato il Centro sicurezza PC hello istanze di SQL Server in cui il rilevamento di minaccia e di controllo non sono abilitati. Dopo l'attivazione del controllo, è possibile configurare le impostazioni di rilevamento minacce e di posta elettronica tooreceive impostazioni degli avvisi di sicurezza. Rilevamento minacce Avvisa quando rileva attività del database anomale che indicano la potenziale database toohello rischi di sicurezza. Hello avvisi vengono visualizzati nel dashboard di hello Centro sicurezza PC.
![Controllo e rilevamento delle minacce][5]

Seguire i passaggi di hello in [rilevamento minacce del Database SQL nel portale di Azure hello](../sql-database/sql-database-threat-detection-portal.md) tooturn in e configurare l'individuazione e l'elenco di hello tooconfigure dei messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di attività anomale.

toolearn informazioni sulle indicazioni, vedere [gestione consigli sulla sicurezza](security-center-recommendations.md).

## <a name="monitor-security-health"></a>Monitorare l'integrità della sicurezza
Dopo aver abilitato [criteri di sicurezza](security-center-policies.md) per le risorse di una sottoscrizione, il Centro sicurezza PC analizzerà le risorse tooidentify potenziali vulnerabilità della sicurezza hello.  È possibile visualizzare lo stato di sicurezza hello delle risorse in hello **integrità delle risorse di sicurezza** riquadro. Quando fa clic su **dati** in hello **integrità delle risorse di sicurezza** riquadro, hello **risorse dati** pannello apre con le raccomandazioni di SQL per i problemi come il controllo e trasparente crittografia dei dati non sia abilitata. Include inoltre indicazioni per lo stato di integrità generale hello del database hello.
![Integrità della sicurezza delle risorse][6]

vedere, più toolearn [il monitoraggio dello stato di sicurezza](security-center-monitoring.md).

## <a name="manage-and-respond-toosecurity-alerts"></a>Gestire e rispondere toosecurity avvisi
Centro sicurezza PC automaticamente raccoglie, analizza e consente di integrare dati di log dalla [rilevamento minacce di SQL Azure](../sql-database/sql-database-threat-detection.md), come altre risorse di Azure, minacce reali toodetect e ridurre i falsi positivi. Viene visualizzato un elenco di avvisi di sicurezza in ordine di priorità del Centro sicurezza PC insieme hello informazioni necessarie tooquickly analizzare problema hello e indicazioni sul tooremediate un attacco.

avvisi toosee, seleziona hello **degli avvisi di sicurezza** riquadro nel Pannello di hello Centro sicurezza PC. In hello **degli avvisi di sicurezza** pannello, seleziona un avviso toolearn più sugli eventi hello che ha attivato avviso hello e cosa, se presente, i passaggi necessari per necessario tootake tooremediate un attacco. In questo esempio si seleziona **Potential SQL Injection** (Potenziale attacco SQL injection).
![Avvisi di sicurezza][7]

Come mostrato di seguito vengono forniti dettagli aggiuntivi che offrono approfondite quali avviso hello attivate, hello destinazione risorsa, quando applicabile hello origine indirizzo IP e indicazioni su come tooremediate.
![Potenziale attacco SQL injection][8]

vedere, più toolearn [la gestione e risponde avvisi toosecurity](security-center-managing-and-responding-alerts.md).

## <a name="next-steps"></a>Passaggi successivi
* [Domande frequenti su Centro sicurezza PC](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Guida alla pianificazione e le operazioni di Centro sicurezza PC](security-center-planning-and-operations-guide.md) : seguire una serie di passaggi e attività toooptimize l'utilizzo di centro di sicurezza in base a requisiti di sicurezza dell'organizzazione e il modello di gestione di cloud.
* [Sicurezza dei dati nel Centro sicurezza](security-center-data-security.md): apprendere come il Centro sicurezza raccoglie ed elabora i dati sulle risorse di Azure, tra cui informazioni di configurazione, metadati, registri eventi, file di dump di arresto anomalo del sistema e altro.
* [Gestione degli eventi di sicurezza](security-center-incident.md) -informazioni su come protezione hello toouse avviso capacità nel Centro sicurezza PC tooassist nella gestione degli eventi di sicurezza.

<!--Image references-->
[1]: ./media/security-center-sql-database/security-center.png
[2]: ./media/security-center-sql-database/security-center-blade.png
[3]: ./media/security-center-sql-database/security-policy.png
[4]: ./media/security-center-sql-database/recommendation.png
[5]: ./media/security-center-sql-database/turn-on-auditing.png
[6]: ./media/security-center-sql-database/monitor-health.png
[7]: ./media/security-center-sql-database/alert.png
[8]: ./media/security-center-sql-database/sql-injection.png
