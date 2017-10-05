---
title: Introduzione al Rilevamento delle minacce in SQL Data Warehouse
description: "Attività iniziali per il rilevamento delle minacce"
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
ms.openlocfilehash: f4a2376fe4fb710d031c35ca7fdbf4c7bb0f3caa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="de91c-103">Introduzione al rilevamento delle minacce</span><span class="sxs-lookup"><span data-stu-id="de91c-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de91c-104">Controllo</span><span class="sxs-lookup"><span data-stu-id="de91c-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="de91c-105">Introduzione al rilevamento delle minacce</span><span class="sxs-lookup"><span data-stu-id="de91c-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="de91c-106">Overview</span><span class="sxs-lookup"><span data-stu-id="de91c-106">Overview</span></span>
<span data-ttu-id="de91c-107">La funzionalità di rilevamento delle minacce individua le attività di database che indicano la presenza di potenziali minacce alla sicurezza nel database.</span><span class="sxs-lookup"><span data-stu-id="de91c-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="de91c-108">Questa funzionalità è in anteprima ed è supportata per SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="de91c-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="de91c-109">Il rilevamento delle minacce offre un nuovo livello di protezione, che consente ai clienti di rilevare e rispondere alle minacce potenziali non appena si verificano, fornendo avvisi di sicurezza sulle attività anomale.</span><span class="sxs-lookup"><span data-stu-id="de91c-109">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="de91c-110">Gli utenti possono esaminare gli eventi sospetti usando il [servizio di controllo di Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) per determinare se sono il risultato di un tentativo di accesso, violazione o exploit dei dati nel data warehouse.</span><span class="sxs-lookup"><span data-stu-id="de91c-110">Users can explore the suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) to determine if they result from an attempt to access, breach or exploit data in the data warehouse.</span></span>
<span data-ttu-id="de91c-111">Il rilevamento delle minacce rende più semplice affrontare le minacce potenziali al data warehouse, senza dover essere esperti della sicurezza o gestire sistemi di controllo di sicurezza avanzati.</span><span class="sxs-lookup"><span data-stu-id="de91c-111">Threat Detection makes it simple to address potential threats to the data warehouse without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="de91c-112">Ad esempio, la funzionalità di rilevamento delle minacce individua determinate attività anomale nel database che indicano potenziali tentativi di attacco SQL injection.</span><span class="sxs-lookup"><span data-stu-id="de91c-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="de91c-113">L'attacco SQL injection è uno dei problemi di sicurezza comuni delle applicazioni Web su Internet, che viene usato per attaccare le applicazioni guidate dai dati.</span><span class="sxs-lookup"><span data-stu-id="de91c-113">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="de91c-114">Gli autori di attacchi sfruttano le vulnerabilità delle applicazioni per introdurre istruzioni SQL dannose nei campi di immissione dell'applicazione, per violare o modificare i dati nel database.</span><span class="sxs-lookup"><span data-stu-id="de91c-114">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="de91c-115">Configurare il rilevamento delle minacce per il database</span><span class="sxs-lookup"><span data-stu-id="de91c-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="de91c-116">Avviare il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de91c-116">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="de91c-117">Passare al pannello di configurazione dell’SQL Data Warehouse che si vuole monitorare.</span><span class="sxs-lookup"><span data-stu-id="de91c-117">Navigate to the configuration blade of the SQL Data Warehouse you want to monitor.</span></span> <span data-ttu-id="de91c-118">Nel pannello Impostazioni selezionare **Controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="de91c-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Riquadro di spostamento][1]
3. <span data-ttu-id="de91c-120">Nel pannello di configurazione **Controllo e rilevamento minacce** selezionare **ON** per attivare il controllo, che mostrerà le impostazioni di rilevamento delle minacce.</span><span class="sxs-lookup"><span data-stu-id="de91c-120">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the Threat detection settings.</span></span>
   
    ![Riquadro di spostamento][2]
4. <span data-ttu-id="de91c-122">Impostare il rilevamento delle minacce su **SÌ** .</span><span class="sxs-lookup"><span data-stu-id="de91c-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="de91c-123">Configurare l'elenco di indirizzi di posta elettronica che riceveranno avvisi di sicurezza in caso di rilevamento di attività anomale di data warehouse.</span><span class="sxs-lookup"><span data-stu-id="de91c-123">Configure the list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="de91c-124">Fare clic su **Salva** nel pannello di configurazione **Controllo e rilevamento minacce** per salvare i criteri di controllo e rilevamento delle minacce nuovi o aggiornati.</span><span class="sxs-lookup"><span data-stu-id="de91c-124">Click **Save** in the **Auditing & Threat detection** configuration blade to save the new or updated auditing and threat detection policy.</span></span>
   
    ![Riquadro di spostamento][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="de91c-126">Esaminare le attività anomale di data warehouse quando viene rilevato un evento sospetto</span><span class="sxs-lookup"><span data-stu-id="de91c-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="de91c-127">Si riceverà una notifica tramite posta elettronica al rilevamento di attività di database anomale.</span><span class="sxs-lookup"><span data-stu-id="de91c-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="de91c-128">Il messaggio di posta elettronica fornirà informazioni sull'evento di sicurezza sospetto, inclusi la natura delle attività anomale, il nome del database, il nome del server e l'ora dell'evento.</span><span class="sxs-lookup"><span data-stu-id="de91c-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="de91c-129">Verranno anche fornite informazioni sulle possibili cause e le azioni consigliate per analizzare e ridurre il rischio di una potenziale minaccia al database.</span><span class="sxs-lookup"><span data-stu-id="de91c-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
   
    ![Riquadro di spostamento][4]
2. <span data-ttu-id="de91c-131">Nel messaggio di posta elettronica fare clic sul collegamento relativo al **log di controllo SQL di Azure** che avvierà il portale di Azure classico visualizzando i record di controllo pertinenti intorno all'ora dell'evento sospetto.</span><span class="sxs-lookup"><span data-stu-id="de91c-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure Classic Portal and show the relevant Auditing records around the time of the suspicious event.</span></span>
   
    ![Riquadro di spostamento][5]
3. <span data-ttu-id="de91c-133">Fare clic sui record di controllo per visualizzare altri dettagli sulle attività di database sospette, come l'istruzione SQL, il motivo dell'errore e l'indirizzo IP del client.</span><span class="sxs-lookup"><span data-stu-id="de91c-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Riquadro di spostamento][6]
4. <span data-ttu-id="de91c-135">Nel pannello Auditing Records (Controllo record) fare clic su  **Apri in Excel** per aprire un modello Excel preconfigurato per importare ed eseguire un'analisi più approfondita del log di controllo sull'orario in cui si è verificato l'evento sospetto.</span><span class="sxs-lookup"><span data-stu-id="de91c-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span><br/><span data-ttu-id="de91c-136">
   **Nota**: in Excel 2010 o versione successiva sono richiesti Power Query e l'impostazione **Combinazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="de91c-136">
**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required</span></span>
   
    ![Riquadro di spostamento][7]
5. <span data-ttu-id="de91c-138">Per configurare l'impostazione **Combinazione rapida**, nella scheda della barra multifunzione **POWER QUERY** selezionare **Opzioni** per visualizzare la finestra di dialogo Opzioni.</span><span class="sxs-lookup"><span data-stu-id="de91c-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="de91c-139">Selezionare la sezione Privacy e scegliere la seconda opzione - "Ignora i livelli di privacy per un potenziale miglioramento delle prestazioni":</span><span class="sxs-lookup"><span data-stu-id="de91c-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>
   
    ![Riquadro di spostamento][8]
6. <span data-ttu-id="de91c-141">Per caricare i log di controllo SQL, assicurarsi che i parametri nella scheda Impostazioni siano configurati correttamente e quindi selezionare "Dati" sulla barra multifunzione e fare clic sul pulsante "Aggiorna tutto".</span><span class="sxs-lookup"><span data-stu-id="de91c-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>
   
    ![Riquadro di spostamento][9]
7. <span data-ttu-id="de91c-143">I risultati vengono visualizzati nel foglio dei **log di controllo SQL** che consente di eseguire un'analisi più approfondita delle attività anomale rilevate e di ridurre l'impatto dell'evento di sicurezza nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="de91c-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>

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
