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
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="c6dea-103">Introduzione al rilevamento delle minacce</span><span class="sxs-lookup"><span data-stu-id="c6dea-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6dea-104">Controllo</span><span class="sxs-lookup"><span data-stu-id="c6dea-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="c6dea-105">Introduzione al rilevamento delle minacce</span><span class="sxs-lookup"><span data-stu-id="c6dea-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c6dea-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c6dea-106">Overview</span></span>
<span data-ttu-id="c6dea-107">Rilevamento minacce consente attività di database anomale che possono indicare potenziali database toohello rischi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="c6dea-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="c6dea-108">Questa funzionalità è in anteprima ed è supportata per SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6dea-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="c6dea-109">Rilevamento minacce fornisce un nuovo livello di sicurezza, che consente ai clienti toodetect e risposta toopotential minacce che si verificano fornendo gli avvisi di sicurezza sull'attività anomale.</span><span class="sxs-lookup"><span data-stu-id="c6dea-109">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="c6dea-110">Agli utenti di esplorare gli eventi di hello sospette utilizzando [il controllo di Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) toodetermine se sono il risultato di un tentativo tooaccess, violazioni o sfruttare dati hello data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6dea-110">Users can explore hello suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine if they result from an attempt tooaccess, breach or exploit data in hello data warehouse.</span></span>
<span data-ttu-id="c6dea-111">Rilevamento minacce rende semplice tooaddress potenziali minacce toohello data warehouse senza hello necessità toobe un esperto della sicurezza o gestione un monitoraggio dei sistemi di sicurezza avanzate.</span><span class="sxs-lookup"><span data-stu-id="c6dea-111">Threat Detection makes it simple tooaddress potential threats toohello data warehouse without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="c6dea-112">Ad esempio, la funzionalità di rilevamento delle minacce individua determinate attività anomale nel database che indicano potenziali tentativi di attacco SQL injection.</span><span class="sxs-lookup"><span data-stu-id="c6dea-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="c6dea-113">Attacchi SQL injection è uno dei hello Web sicurezza problemi delle applicazioni su Internet, le applicazioni utilizzate tooattack basati sui dati hello.</span><span class="sxs-lookup"><span data-stu-id="c6dea-113">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="c6dea-114">Gli utenti malintenzionati sfruttano applicazione vulnerabilità tooinject dannoso istruzioni SQL in campi di immissione di applicazione, per sugli o la modifica dei dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="c6dea-114">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="c6dea-115">Configurare il rilevamento delle minacce per il database</span><span class="sxs-lookup"><span data-stu-id="c6dea-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="c6dea-116">Avvio hello portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6dea-116">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c6dea-117">Passare a pannello di configurazione toohello di hello desiderato toomonitor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6dea-117">Navigate toohello configuration blade of hello SQL Data Warehouse you want toomonitor.</span></span> <span data-ttu-id="c6dea-118">Nel pannello impostazioni hello, selezionare **controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="c6dea-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Riquadro di spostamento][1]
3. <span data-ttu-id="c6dea-120">In hello **controllo e rilevamento minacce** configurazione pannello turn **ON** controllo, che visualizza le impostazioni di rilevamento minacce hello.</span><span class="sxs-lookup"><span data-stu-id="c6dea-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello Threat detection settings.</span></span>
   
    ![Riquadro di spostamento][2]
4. <span data-ttu-id="c6dea-122">Impostare il rilevamento delle minacce su **SÌ** .</span><span class="sxs-lookup"><span data-stu-id="c6dea-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="c6dea-123">Configurare l'elenco di hello di messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di attività warehouse dati anomali.</span><span class="sxs-lookup"><span data-stu-id="c6dea-123">Configure hello list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="c6dea-124">Fare clic su **salvare** in hello **rilevamento controllo & minaccia** toosave pannello configurazione hello nuovi o aggiornati criteri di rilevamento di controllo e minacce.</span><span class="sxs-lookup"><span data-stu-id="c6dea-124">Click **Save** in hello **Auditing & Threat detection** configuration blade toosave hello new or updated auditing and threat detection policy.</span></span>
   
    ![Riquadro di spostamento][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="c6dea-126">Esaminare le attività anomale di data warehouse quando viene rilevato un evento sospetto</span><span class="sxs-lookup"><span data-stu-id="c6dea-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="c6dea-127">Si riceverà una notifica tramite posta elettronica al rilevamento di attività di database anomale.</span><span class="sxs-lookup"><span data-stu-id="c6dea-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="c6dea-128">messaggio di posta elettronica Hello verrà fornite informazioni sull'evento sospetti hello inclusi natura hello di attività anomale hello, nome del database, l'ora dell'evento hello nome e il server.</span><span class="sxs-lookup"><span data-stu-id="c6dea-128">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="c6dea-129">Inoltre, verranno fornite informazioni sulle possibili cause e consigliabile tooinvestigate azioni e ridurre database toohello minaccia potenziale di hello.</span><span class="sxs-lookup"><span data-stu-id="c6dea-129">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
   
    ![Riquadro di spostamento][4]
2. <span data-ttu-id="c6dea-131">Nel messaggio di posta elettronica di hello, fare clic su hello **Log di controllo di SQL Azure** collegamento, che consente di avviare hello portale classico di Azure e visualizzare hello record di controllo pertinente alla ora hello di eventi sospetti hello.</span><span class="sxs-lookup"><span data-stu-id="c6dea-131">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure Classic Portal and show hello relevant Auditing records around hello time of hello suspicious event.</span></span>
   
    ![Riquadro di spostamento][5]
3. <span data-ttu-id="c6dea-133">Fare clic su tooview record di controllo hello ulteriori informazioni sulle attività sospette database hello, ad esempio l'istruzione SQL, IP client e motivo di errore.</span><span class="sxs-lookup"><span data-stu-id="c6dea-133">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Riquadro di spostamento][6]
4. <span data-ttu-id="c6dea-135">Nel Pannello di controllo Registra hello, fare clic su **Apri in Excel** tooopen preconfigurata che excel tooimport modello e eseguire un'analisi più approfondita del log di controllo hello alla ora hello di eventi sospetti hello.</span><span class="sxs-lookup"><span data-stu-id="c6dea-135">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span><br/><span data-ttu-id="c6dea-136">
   **Nota:** In Excel 2010 o versioni successive Power Query e hello **combinazione rapida** impostazione è obbligatoria</span><span class="sxs-lookup"><span data-stu-id="c6dea-136">
**Note:** In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required</span></span>
   
    ![Riquadro di spostamento][7]
5. <span data-ttu-id="c6dea-138">hello tooconfigure **combinazione rapida** impostazione - hello **POWER QUERY** scheda della barra multifunzione selezionare **opzioni** finestra di dialogo Opzioni toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="c6dea-138">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="c6dea-139">Selezionare hello Privacy sezione e scegliere l'opzione secondo hello - 'Ignora i livelli di Privacy hello e potenziale miglioramento delle prestazioni':</span><span class="sxs-lookup"><span data-stu-id="c6dea-139">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>
   
    ![Riquadro di spostamento][8]
6. <span data-ttu-id="c6dea-141">log di controllo SQL tooload, assicurarsi che i parametri di hello nella scheda Impostazioni hello siano impostati correttamente e quindi selezionare barra multifunzione 'Data' hello e fare clic sul pulsante 'Aggiorna tutto' hello.</span><span class="sxs-lookup"><span data-stu-id="c6dea-141">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>
   
    ![Riquadro di spostamento][9]
7. <span data-ttu-id="c6dea-143">Hello risultati vengono visualizzati in hello **i log di controllo SQL** foglio che consente l'analisi più approfondita di toorun di attività anomale di hello che sono stati rilevati e ridurre l'impatto hello di eventi di protezione hello nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c6dea-143">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>

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
