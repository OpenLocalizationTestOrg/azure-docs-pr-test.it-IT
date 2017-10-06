---
title: rilevamento di controllo e minacce aaaEnable in SQL Server nel Centro protezione di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * il rilevamento di abilitare il controllo & minaccia in SQL Server * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a>Abilitare il controllo e il rilevamento delle minacce sui server SQL nel Centro sicurezza di Azure
Il Centro sicurezza di Azure consiglia di attivare il controllo e il rilevamento delle minacce per tutti i database nei server SQL di Azure, se queste funzionalità non sono già abilitate. Il controllo e il rilevamento delle minacce possono agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza.

Dopo aver attivato il controllo è possibile configurare funzionalità di rilevamento minacce impostazioni e i messaggi di posta elettronica tooreceive degli avvisi di sicurezza. Rilevamento minacce consente attività di database anomale che possono indicare potenziali database toohello rischi di sicurezza. Questo permette toodetect e risposta toopotential minacce che si verificano.

Questa indicazione si applica toohello solo servizio di SQL Azure non include SQL Server in esecuzione nelle macchine virtuali in servizi di infrastruttura di Azure (IaaS di Azure).

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questa non è una guida dettagliata.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **indicazioni** pannello seleziona **rilevamento Attiva controllo & minaccia nei server SQL**.  Verrà visualizzata hello **rilevamento Attiva controllo & minaccia nei server SQL** blade.

   ![Abilitare il controllo sui server SQL][1]
2. Scegliere un SQL server tooenable controllo e minaccia il rilevamento. Verrà visualizzata hello **controllo e rilevamento minacce** blade.

3. In hello **controllo e rilevamento minacce** pannello seleziona **ON** in **controllo**.

   ![Attivare le impostazioni del servizio di controllo][2]
4. Seguire i passaggi di hello in [controllo del database SQL nel portale di Azure di hello](../sql-database/sql-database-auditing-portal.md) tooconfigure archiviazione in cui verranno archiviati i log di controllo. Hello account di archiviazione della sottoscrizione per la raccolta dati è hello account di archiviazione predefinito.
5. Seguire i passaggi di hello in [introduzione rilevamento minacce del Database SQL](../sql-database/sql-database-threat-detection.md) tooturn in e configurare il rilevamento di minaccia ed elenco hello tooconfigure di messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di attività anomale.

## <a name="see-also"></a>Vedere anche
In questo articolo ha illustrato come tooimplement hello raccomandazione Centro sicurezza PC "Abilitare il controllo e delle minacce rilevamento sul server SQL Server". toolearn più sulla protezione dei database SQL, vedere l'esempio hello:

* [Protezione del Database SQL](../sql-database/sql-database-security-overview.md)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) -ottenere informazioni e notizie sicurezza di Azure hello.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
