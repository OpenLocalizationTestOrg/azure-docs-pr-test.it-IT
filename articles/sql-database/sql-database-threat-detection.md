---
title: aaaThreat rilevamento - Database SQL di Azure | Documenti Microsoft
description: "Rilevamento minacce consente attività di database anomale che possono indicare potenziali database toohello rischi di sicurezza."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a>Rilevamento delle minacce nel database SQL

Rilevamento minacce SQL rileva attività anomale che indica di tentativi insoliti e potenzialmente dannoso tooaccess o exploit database.

## <a name="overview"></a>Panoramica

Rilevamento minacce SQL fornisce un nuovo livello di sicurezza, che consente ai clienti toodetect e risposta toopotential minacce che si verificano fornendo gli avvisi di sicurezza sull'attività anomale.  Gli utenti riceveranno un avviso in caso di attività di database sospetta, potenziali vulnerabilità e attacchi SQL injection, nonché in caso di modelli di accesso ai database anomali. Avvisi di rilevamento minacce SQL forniscono i dettagli dell'attività sospette e consigliabile azione sulla tooinvestigate e ridurre il rischio di hello. Agli utenti di esplorare gli eventi di hello sospette utilizzando [SQL Database Auditing](sql-database-auditing.md) toodetermine se sono il risultato di un tentativo tooaccess, violazioni o sfruttare i dati nel database di hello. Rilevamento minacce rende semplice tooaddress potenziali minacce toohello database di senza necessità di hello toobe un esperto della sicurezza o gestire i sistemi di monitoraggio di sicurezza avanzata.

Ad esempio attacchi SQL injection è uno dei hello Web sicurezza problemi delle applicazioni su Internet, le applicazioni utilizzate tooattack basati sui dati hello. Gli utenti malintenzionati sfruttano applicazione vulnerabilità tooinject dannoso istruzioni SQL in campi di ingresso dell'applicazione, sono state violate oppure la modifica dei dati nel database di hello.

Rilevamento minacce SQL integra gli avvisi con [Centro sicurezza di Azure](https://azure.microsoft.com/en-us/services/security-center/), e verrà addebitato ogni server SQL Database protetto in hello stesso prezzo come livello Standard di Centro protezione di Azure, in $15/nodo/mese, dove ogni protetto SQL Server di database viene conteggiato come un nodo. Invitare tootry impostarlo per 60 giorni per liberare. 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a>Impostare la funzionalità di rilevamento minacce del database nel portale di Azure hello
1. Avviare hello Azure portale in [https://portal.azure.com](https://portal.azure.com).
2. Passare a pannello di configurazione toohello di Database SQL da toomonitor hello. Nel pannello impostazioni hello, selezionare **controllo e rilevamento minacce**. 
    ![Riquadro di spostamento][1]
3. In hello **controllo e rilevamento minacce** configurazione pannello turn **ON** controllo, che consentirà di visualizzare le impostazioni di rilevamento minacce hello.
  
    ![Riquadro di spostamento][2]
4. Impostare il rilevamento delle minacce su **SÌ** .
5. Configurare l'elenco di hello di messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di attività del database anomale.
6. Fare clic su **salvare** in hello **rilevamento controllo & minaccia** toosave pannello hello nuove o aggiornate minaccia e controllo delle impostazioni di rilevamento.
       
    ![Riquadro di spostamento][3]

## <a name="set-up-threat-detection-using-powershell"></a>Configurare il rilevamento delle minacce tramite PowerShell

Per un esempio di script, vedere [Configurare il controllo del database SQL e il rilevamento delle minacce usando PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a>Esaminare le attività di database anomale quando viene rilevato un evento sospetto
1. Si riceverà una notifica tramite posta elettronica al rilevamento di attività di database anomale. <br/>
   messaggio di posta elettronica Hello verrà fornite informazioni sull'evento sospetti hello inclusi natura hello di attività anomale hello, nome del database, nome del server, nome dell'applicazione e ora dell'evento hello. Inoltre, hello e posta elettronica verrà fornite informazioni sulle possibili cause e consigliabile azioni tooinvestigate attenuare database toohello minaccia potenziale di hello.<br/>
     
    ![Riquadro di spostamento][4]
2. avviso di posta elettronica Hello include un log di controllo SQL toohello collegamento diretto. Facendo clic su questo hello avvia collegamento Azure portal e apre hello SQL i record di controllo alla ora hello di eventi sospetti hello. Fare clic su ulteriori informazioni sulle attività sospette database hello, rendendo più semplice toofind hello SQL le istruzioni eseguite in un tooview record di controllo (ha avuto accesso, le quali è stata e quando) e determinare se l'evento hello è legittimo o malintenzionati (ad esempio, applicazione è stato sfruttato injection tooSQL vulnerabilità, un utente violato i dati sensibili e così via).<br/>
   ![Riquadro di spostamento][5]


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a>Esplorare gli avvisi di rilevamento minacce del database nel portale di Azure hello

Rilevamento minacce del database SQL integra i suoi avvisi con il [Centro sicurezza di Azure](https://azure.microsoft.com/en-us/services/security-center/). SQL sicurezza animato nel pannello database hello nello stato di hello hello Azure tiene traccia del portale di minacce attive. 

   ![Riquadro di spostamento][6]
   
1. Fare clic sul riquadro di sicurezza SQL hello avvia pannello avvisi di hello Centro sicurezza di Azure e viene fornita una panoramica di minacce SQL attive nel database di hello rilevate. 

  ![Riquadro di spostamento][7]

2. Facendo clic su uno specifico avviso vengono visualizzati altri dettagli e azioni per analizzare la minaccia e risolvere eventuali minacce future.

  ![Riquadro di spostamento][8]


## <a name="next-steps"></a>Passaggi successivi

* Altre informazioni sulle funzionalità di rilevamento minacce, visitare hello [blog di Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/) 
* Altre informazioni sul [controllo del database SQL di Azure](sql-database-auditing.md)
* Altre informazioni sul [Centro sicurezza di Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)
* Per ulteriori informazioni sui prezzi, vedere hello [pagina prezzi di Database SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)  
* Per un esempio di script di PowerShell, vedere [Configurare il controllo del database SQL e il rilevamento delle minacce usando PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


