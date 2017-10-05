---
title: Rilevamento minacce - Database SQL di Azure | Documentazione Microsoft
description: "La funzionalità di rilevamento delle minacce individua le attività di database che indicano la presenza di potenziali minacce alla sicurezza nel database."
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
ms.openlocfilehash: bd3de9ed0131edc683763b0fe7f4a2ae74533944
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="25e0f-103">Rilevamento delle minacce nel database SQL</span><span class="sxs-lookup"><span data-stu-id="25e0f-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="25e0f-104">Rilevamento minacce di SQL rileva le attività anomale che indicano tentativi insoliti e potenzialmente dannosi di accesso o exploit dei database.</span><span class="sxs-lookup"><span data-stu-id="25e0f-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts to access or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="25e0f-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="25e0f-105">Overview</span></span>

<span data-ttu-id="25e0f-106">Rilevamento minacce di SQL offre un nuovo livello di protezione, che consente ai clienti di rilevare e rispondere alle minacce potenziali non appena si verificano, fornendo avvisi di sicurezza sulle attività anomale.</span><span class="sxs-lookup"><span data-stu-id="25e0f-106">SQL Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="25e0f-107">Gli utenti riceveranno un avviso in caso di attività di database sospetta, potenziali vulnerabilità e attacchi SQL injection, nonché in caso di modelli di accesso ai database anomali.</span><span class="sxs-lookup"><span data-stu-id="25e0f-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="25e0f-108">Gli avvisi di Rilevamento minacce di SQL forniscono i dettagli delle attività sospette e consigliano azioni per analizzare e ridurre la minaccia.</span><span class="sxs-lookup"><span data-stu-id="25e0f-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how to investigate and mitigate the threat.</span></span> <span data-ttu-id="25e0f-109">Gli utenti possono esaminare gli eventi sospetti tramite il [servizio di controllo del database SQL](sql-database-auditing.md) per determinare se sono il risultato di un tentativo di accesso, una violazione o un exploit dei dati del database.</span><span class="sxs-lookup"><span data-stu-id="25e0f-109">Users can explore the suspicious events using [SQL Database Auditing](sql-database-auditing.md) to determine if they result from an attempt to access, breach, or exploit data in the database.</span></span> <span data-ttu-id="25e0f-110">Il rilevamento delle minacce rende più semplice affrontare le minacce potenziali al database, senza dover essere esperti della sicurezza o gestire sistemi di controllo di sicurezza avanzati.</span><span class="sxs-lookup"><span data-stu-id="25e0f-110">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="25e0f-111">Ad esempio, l'attacco SQL injection è uno dei problemi di sicurezza comuni delle applicazioni Web su Internet, che viene usato per attaccare le applicazioni guidate dai dati.</span><span class="sxs-lookup"><span data-stu-id="25e0f-111">For example, SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="25e0f-112">Gli autori degli attacchi sfruttano le vulnerabilità delle applicazioni per introdurre istruzioni SQL dannose nei campi di immissione dell'applicazione, con lo scopo di violare o modificare i dati del database.</span><span class="sxs-lookup"><span data-stu-id="25e0f-112">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, breaching or modifying data in the database.</span></span>

<span data-ttu-id="25e0f-113">Rilevamento minacce di SQL integra gli avvisi con il [Centro sicurezza di Azure](https://azure.microsoft.com/en-us/services/security-center/). Ogni database SQL protetto verrà fatturato allo stesso prezzo del livello Standard del Centro sicurezza di Azure, al prezzo di $ 15 per nodo al mese, dove ogni server di database SQL protetto viene conteggiato come un nodo.</span><span class="sxs-lookup"><span data-stu-id="25e0f-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at the same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="25e0f-114">Fai una prova gratuita di 60 giorni.</span><span class="sxs-lookup"><span data-stu-id="25e0f-114">We invite you to try it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-the-azure-portal"></a><span data-ttu-id="25e0f-115">Configurare il rilevamento delle minacce per il database tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="25e0f-115">Set up threat detection for your database in the Azure portal</span></span>
1. <span data-ttu-id="25e0f-116">Avviare il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25e0f-116">Launch the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="25e0f-117">Passare al pannello di configurazione del database SQL che si vuole monitorare.</span><span class="sxs-lookup"><span data-stu-id="25e0f-117">Navigate to the configuration blade of the SQL Database you want to monitor.</span></span> <span data-ttu-id="25e0f-118">Nel pannello Impostazioni selezionare **Controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="25e0f-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="25e0f-119">![Riquadro di spostamento][1]</span><span class="sxs-lookup"><span data-stu-id="25e0f-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="25e0f-120">Nel pannello di configurazione **Controllo e rilevamento minacce** impostare il controllo su **SÌ**, il che consentirà di visualizzare le impostazioni di rilevamento minacce.</span><span class="sxs-lookup"><span data-stu-id="25e0f-120">In the **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display the threat detection settings.</span></span>
  
    ![Riquadro di spostamento][2]
4. <span data-ttu-id="25e0f-122">Impostare il rilevamento delle minacce su **SÌ** .</span><span class="sxs-lookup"><span data-stu-id="25e0f-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="25e0f-123">Configurare l'elenco di indirizzi di posta elettronica che riceveranno avvisi di sicurezza in caso di rilevamento di attività di database anomale.</span><span class="sxs-lookup"><span data-stu-id="25e0f-123">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="25e0f-124">Fare clic su **Salva** nel pannello di configurazione **Controllo e rilevamento minacce** per salvare il controllo nuovo o aggiornato e le impostazioni di rilevamento delle minacce.</span><span class="sxs-lookup"><span data-stu-id="25e0f-124">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection settings.</span></span>
       
    ![Riquadro di spostamento][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="25e0f-126">Configurare il rilevamento delle minacce tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="25e0f-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="25e0f-127">Per un esempio di script, vedere [Configurare il controllo del database SQL e il rilevamento delle minacce usando PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="25e0f-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="25e0f-128">Esaminare le attività di database anomale quando viene rilevato un evento sospetto</span><span class="sxs-lookup"><span data-stu-id="25e0f-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="25e0f-129">Si riceverà una notifica tramite posta elettronica al rilevamento di attività di database anomale.</span><span class="sxs-lookup"><span data-stu-id="25e0f-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="25e0f-130">Il messaggio di posta elettronica fornirà informazioni sull'evento di sicurezza sospetto, inclusi la natura delle attività anomale, il nome del database, il nome del server, il nome dell'applicazione e l'ora dell'evento.</span><span class="sxs-lookup"><span data-stu-id="25e0f-130">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name, application name, and the event time.</span></span> <span data-ttu-id="25e0f-131">Il messaggio di posta elettronica fornirà anche informazioni sulle possibili cause e le azioni consigliate per analizzare e ridurre il rischio di una potenziale minaccia al database.</span><span class="sxs-lookup"><span data-stu-id="25e0f-131">In addition, the email will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
     
    ![Riquadro di spostamento][4]
2. <span data-ttu-id="25e0f-133">L'avviso di posta elettronica include un collegamento diretto al log di controllo SQL.</span><span class="sxs-lookup"><span data-stu-id="25e0f-133">The email alert includes a direct link to the SQL Audit log.</span></span> <span data-ttu-id="25e0f-134">Facendo clic su questo collegamento viene avviato il portale di Azure e si aprono i record di controllo SQL riferiti alla stessa ora dell'evento sospetto.</span><span class="sxs-lookup"><span data-stu-id="25e0f-134">Clicking on this link launches the Azure portal and opens the SQL Audit records around the time of the suspicious event.</span></span> <span data-ttu-id="25e0f-135">Fare clic su un record di controllo per visualizzare altri dettagli sulle attività sospette del database, per trovare più facilmente le istruzioni SQL eseguite (chi ha eseguito l'accesso, cosa ha fatto e quando) e determinare se l'evento era legittimo o dannoso (ad esempio se sono state sfruttate vulnerabilità dell'applicazione all'SQL injection, un utente ha compromesso dati sensibili e così via).</span><span class="sxs-lookup"><span data-stu-id="25e0f-135">Click on an audit record to view more details on the suspicious database activities, making it easier to find the SQL statements that were executed (who accessed, what they did and when) and determine if the event was legitimate or malicious (e.g. application vulnerability to SQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="25e0f-136">
   ![Riquadro di spostamento][5]</span><span class="sxs-lookup"><span data-stu-id="25e0f-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-the-azure-portal"></a><span data-ttu-id="25e0f-137">Esplorare gli avvisi di rilevamento delle minacce per il database tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="25e0f-137">Explore threat detection alerts for your database in the Azure portal</span></span>

<span data-ttu-id="25e0f-138">Rilevamento minacce del database SQL integra i suoi avvisi con il [Centro sicurezza di Azure](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="25e0f-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="25e0f-139">Un riquadro sulla sicurezza live di SQL all'interno del pannello del database nel portale di Azure tiene traccia dello stato delle minacce attive.</span><span class="sxs-lookup"><span data-stu-id="25e0f-139">A live SQL security tile within the database blade in the Azure portal tracks the status of active threats.</span></span> 

   ![Riquadro di spostamento][6]
   
1. <span data-ttu-id="25e0f-141">Facendo clic sul riquadro della sicurezza di SQL si avvia il pannello degli avvisi del Centro sicurezza di Azure e viene fornita una panoramica delle minacce SQL attive rilevate nel database.</span><span class="sxs-lookup"><span data-stu-id="25e0f-141">Clicking on the SQL security tile launches the Azure Security Center alerts blade and provides an overview of active SQL threats detected on the database.</span></span> 

  ![Riquadro di spostamento][7]

2. <span data-ttu-id="25e0f-143">Facendo clic su uno specifico avviso vengono visualizzati altri dettagli e azioni per analizzare la minaccia e risolvere eventuali minacce future.</span><span class="sxs-lookup"><span data-stu-id="25e0f-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Riquadro di spostamento][8]


## <a name="next-steps"></a><span data-ttu-id="25e0f-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25e0f-145">Next steps</span></span>

* <span data-ttu-id="25e0f-146">Per altre informazioni su Rilevamento minacce, visitare il [blog di Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="25e0f-146">Learn more about Threat Detection, visit the [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="25e0f-147">Altre informazioni sul [controllo del database SQL di Azure](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="25e0f-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="25e0f-148">Altre informazioni sul [Centro sicurezza di Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="25e0f-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="25e0f-149">Per altre informazioni sui prezzi, vedere la [pagina Prezzi di Database SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="25e0f-149">For more details on pricing, please see the [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="25e0f-150">Per un esempio di script di PowerShell, vedere [Configurare il controllo del database SQL e il rilevamento delle minacce usando PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="25e0f-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


