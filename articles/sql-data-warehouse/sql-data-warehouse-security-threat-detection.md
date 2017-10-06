---
title: Introduzione al rilevamento minacce del Data Warehouse SQL aaaGet
description: "La modalità di avvio tooget con funzionalità di rilevamento minacce"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a>Introduzione al rilevamento delle minacce
> [!div class="op_single_selector"]
> * [Controllo](sql-data-warehouse-auditing-overview.md)
> * [Introduzione al rilevamento delle minacce](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a>Panoramica
Rilevamento minacce consente attività di database anomale che possono indicare potenziali database toohello rischi di sicurezza. Questa funzionalità è in anteprima ed è supportata per SQL Data Warehouse.

Rilevamento minacce fornisce un nuovo livello di sicurezza, che consente ai clienti toodetect e risposta toopotential minacce che si verificano fornendo gli avvisi di sicurezza sull'attività anomale. Agli utenti di esplorare gli eventi di hello sospette utilizzando [il controllo di Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) toodetermine se sono il risultato di un tentativo tooaccess, violazioni o sfruttare dati hello data warehouse.
Rilevamento minacce rende semplice tooaddress potenziali minacce toohello data warehouse senza hello necessità toobe un esperto della sicurezza o gestione un monitoraggio dei sistemi di sicurezza avanzate.

Ad esempio, la funzionalità di rilevamento delle minacce individua determinate attività anomale nel database che indicano potenziali tentativi di attacco SQL injection. Attacchi SQL injection è uno dei hello Web sicurezza problemi delle applicazioni su Internet, le applicazioni utilizzate tooattack basati sui dati hello. Gli utenti malintenzionati sfruttano applicazione vulnerabilità tooinject dannoso istruzioni SQL in campi di immissione di applicazione, per sugli o la modifica dei dati nel database di hello.

## <a name="set-up-threat-detection-for-your-database"></a>Configurare il rilevamento delle minacce per il database
1. Avvio hello portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com).
2. Passare a pannello di configurazione toohello di hello desiderato toomonitor SQL Data Warehouse. Nel pannello impostazioni hello, selezionare **controllo e rilevamento minacce**.
   
    ![Riquadro di spostamento][1]
3. In hello **controllo e rilevamento minacce** configurazione pannello turn **ON** controllo, che visualizza le impostazioni di rilevamento minacce hello.
   
    ![Riquadro di spostamento][2]
4. Impostare il rilevamento delle minacce su **SÌ** .
5. Configurare l'elenco di hello di messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di attività warehouse dati anomali.
6. Fare clic su **salvare** in hello **rilevamento controllo & minaccia** toosave pannello configurazione hello nuovi o aggiornati criteri di rilevamento di controllo e minacce.
   
    ![Riquadro di spostamento][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a>Esaminare le attività anomale di data warehouse quando viene rilevato un evento sospetto
1. Si riceverà una notifica tramite posta elettronica al rilevamento di attività di database anomale. <br/>
   messaggio di posta elettronica Hello verrà fornite informazioni sull'evento sospetti hello inclusi natura hello di attività anomale hello, nome del database, l'ora dell'evento hello nome e il server. Inoltre, verranno fornite informazioni sulle possibili cause e consigliabile tooinvestigate azioni e ridurre database toohello minaccia potenziale di hello.<br/>
   
    ![Riquadro di spostamento][4]
2. Nel messaggio di posta elettronica di hello, fare clic su hello **Log di controllo di SQL Azure** collegamento, che consente di avviare hello portale classico di Azure e visualizzare hello record di controllo pertinente alla ora hello di eventi sospetti hello.
   
    ![Riquadro di spostamento][5]
3. Fare clic su tooview record di controllo hello ulteriori informazioni sulle attività sospette database hello, ad esempio l'istruzione SQL, IP client e motivo di errore.
   
    ![Riquadro di spostamento][6]
4. Nel Pannello di controllo Registra hello, fare clic su **Apri in Excel** tooopen preconfigurata che excel tooimport modello e eseguire un'analisi più approfondita del log di controllo hello alla ora hello di eventi sospetti hello.<br/>
   **Nota:** In Excel 2010 o versioni successive Power Query e hello **combinazione rapida** impostazione è obbligatoria
   
    ![Riquadro di spostamento][7]
5. hello tooconfigure **combinazione rapida** impostazione - hello **POWER QUERY** scheda della barra multifunzione selezionare **opzioni** finestra di dialogo Opzioni toodisplay hello. Selezionare hello Privacy sezione e scegliere l'opzione secondo hello - 'Ignora i livelli di Privacy hello e potenziale miglioramento delle prestazioni':
   
    ![Riquadro di spostamento][8]
6. log di controllo SQL tooload, assicurarsi che i parametri di hello nella scheda Impostazioni hello siano impostati correttamente e quindi selezionare barra multifunzione 'Data' hello e fare clic sul pulsante 'Aggiorna tutto' hello.
   
    ![Riquadro di spostamento][9]
7. Hello risultati vengono visualizzati in hello **i log di controllo SQL** foglio che consente l'analisi più approfondita di toorun di attività anomale di hello che sono stati rilevati e ridurre l'impatto hello di eventi di protezione hello nell'applicazione.

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
