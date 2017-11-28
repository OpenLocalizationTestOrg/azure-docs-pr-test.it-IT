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
# <a name="sql-database-threat-detection"></a><span data-ttu-id="d8ffb-103">Rilevamento delle minacce nel database SQL</span><span class="sxs-lookup"><span data-stu-id="d8ffb-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="d8ffb-104">Rilevamento minacce SQL rileva attività anomale che indica di tentativi insoliti e potenzialmente dannoso tooaccess o exploit database.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="d8ffb-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d8ffb-105">Overview</span></span>

<span data-ttu-id="d8ffb-106">Rilevamento minacce SQL fornisce un nuovo livello di sicurezza, che consente ai clienti toodetect e risposta toopotential minacce che si verificano fornendo gli avvisi di sicurezza sull'attività anomale.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-106">SQL Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="d8ffb-107">Gli utenti riceveranno un avviso in caso di attività di database sospetta, potenziali vulnerabilità e attacchi SQL injection, nonché in caso di modelli di accesso ai database anomali.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="d8ffb-108">Avvisi di rilevamento minacce SQL forniscono i dettagli dell'attività sospette e consigliabile azione sulla tooinvestigate e ridurre il rischio di hello.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how tooinvestigate and mitigate hello threat.</span></span> <span data-ttu-id="d8ffb-109">Agli utenti di esplorare gli eventi di hello sospette utilizzando [SQL Database Auditing](sql-database-auditing.md) toodetermine se sono il risultato di un tentativo tooaccess, violazioni o sfruttare i dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-109">Users can explore hello suspicious events using [SQL Database Auditing](sql-database-auditing.md) toodetermine if they result from an attempt tooaccess, breach, or exploit data in hello database.</span></span> <span data-ttu-id="d8ffb-110">Rilevamento minacce rende semplice tooaddress potenziali minacce toohello database di senza necessità di hello toobe un esperto della sicurezza o gestire i sistemi di monitoraggio di sicurezza avanzata.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-110">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="d8ffb-111">Ad esempio attacchi SQL injection è uno dei hello Web sicurezza problemi delle applicazioni su Internet, le applicazioni utilizzate tooattack basati sui dati hello.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-111">For example, SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="d8ffb-112">Gli utenti malintenzionati sfruttano applicazione vulnerabilità tooinject dannoso istruzioni SQL in campi di ingresso dell'applicazione, sono state violate oppure la modifica dei dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-112">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, breaching or modifying data in hello database.</span></span>

<span data-ttu-id="d8ffb-113">Rilevamento minacce SQL integra gli avvisi con [Centro sicurezza di Azure](https://azure.microsoft.com/en-us/services/security-center/), e verrà addebitato ogni server SQL Database protetto in hello stesso prezzo come livello Standard di Centro protezione di Azure, in $15/nodo/mese, dove ogni protetto SQL Server di database viene conteggiato come un nodo.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at hello same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="d8ffb-114">Invitare tootry impostarlo per 60 giorni per liberare.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-114">We invite you tootry it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="d8ffb-115">Impostare la funzionalità di rilevamento minacce del database nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="d8ffb-115">Set up threat detection for your database in hello Azure portal</span></span>
1. <span data-ttu-id="d8ffb-116">Avviare hello Azure portale in [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d8ffb-116">Launch hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d8ffb-117">Passare a pannello di configurazione toohello di Database SQL da toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-117">Navigate toohello configuration blade of hello SQL Database you want toomonitor.</span></span> <span data-ttu-id="d8ffb-118">Nel pannello impostazioni hello, selezionare **controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="d8ffb-119">![Riquadro di spostamento][1]</span><span class="sxs-lookup"><span data-stu-id="d8ffb-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="d8ffb-120">In hello **controllo e rilevamento minacce** configurazione pannello turn **ON** controllo, che consentirà di visualizzare le impostazioni di rilevamento minacce hello.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display hello threat detection settings.</span></span>
  
    ![Riquadro di spostamento][2]
4. <span data-ttu-id="d8ffb-122">Impostare il rilevamento delle minacce su **SÌ** .</span><span class="sxs-lookup"><span data-stu-id="d8ffb-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="d8ffb-123">Configurare l'elenco di hello di messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di attività del database anomale.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-123">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="d8ffb-124">Fare clic su **salvare** in hello **rilevamento controllo & minaccia** toosave pannello hello nuove o aggiornate minaccia e controllo delle impostazioni di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-124">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection settings.</span></span>
       
    ![Riquadro di spostamento][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="d8ffb-126">Configurare il rilevamento delle minacce tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8ffb-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="d8ffb-127">Per un esempio di script, vedere [Configurare il controllo del database SQL e il rilevamento delle minacce usando PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d8ffb-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="d8ffb-128">Esaminare le attività di database anomale quando viene rilevato un evento sospetto</span><span class="sxs-lookup"><span data-stu-id="d8ffb-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="d8ffb-129">Si riceverà una notifica tramite posta elettronica al rilevamento di attività di database anomale.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="d8ffb-130">messaggio di posta elettronica Hello verrà fornite informazioni sull'evento sospetti hello inclusi natura hello di attività anomale hello, nome del database, nome del server, nome dell'applicazione e ora dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-130">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name, application name, and hello event time.</span></span> <span data-ttu-id="d8ffb-131">Inoltre, hello e posta elettronica verrà fornite informazioni sulle possibili cause e consigliabile azioni tooinvestigate attenuare database toohello minaccia potenziale di hello.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-131">In addition, hello email will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
     
    ![Riquadro di spostamento][4]
2. <span data-ttu-id="d8ffb-133">avviso di posta elettronica Hello include un log di controllo SQL toohello collegamento diretto.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-133">hello email alert includes a direct link toohello SQL Audit log.</span></span> <span data-ttu-id="d8ffb-134">Facendo clic su questo hello avvia collegamento Azure portal e apre hello SQL i record di controllo alla ora hello di eventi sospetti hello.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-134">Clicking on this link launches hello Azure portal and opens hello SQL Audit records around hello time of hello suspicious event.</span></span> <span data-ttu-id="d8ffb-135">Fare clic su ulteriori informazioni sulle attività sospette database hello, rendendo più semplice toofind hello SQL le istruzioni eseguite in un tooview record di controllo (ha avuto accesso, le quali è stata e quando) e determinare se l'evento hello è legittimo o malintenzionati (ad esempio, applicazione è stato sfruttato injection tooSQL vulnerabilità, un utente violato i dati sensibili e così via).</span><span class="sxs-lookup"><span data-stu-id="d8ffb-135">Click on an audit record tooview more details on hello suspicious database activities, making it easier toofind hello SQL statements that were executed (who accessed, what they did and when) and determine if hello event was legitimate or malicious (e.g. application vulnerability tooSQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="d8ffb-136">
   ![Riquadro di spostamento][5]</span><span class="sxs-lookup"><span data-stu-id="d8ffb-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="d8ffb-137">Esplorare gli avvisi di rilevamento minacce del database nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="d8ffb-137">Explore threat detection alerts for your database in hello Azure portal</span></span>

<span data-ttu-id="d8ffb-138">Rilevamento minacce del database SQL integra i suoi avvisi con il [Centro sicurezza di Azure](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="d8ffb-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="d8ffb-139">SQL sicurezza animato nel pannello database hello nello stato di hello hello Azure tiene traccia del portale di minacce attive.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-139">A live SQL security tile within hello database blade in hello Azure portal tracks hello status of active threats.</span></span> 

   ![Riquadro di spostamento][6]
   
1. <span data-ttu-id="d8ffb-141">Fare clic sul riquadro di sicurezza SQL hello avvia pannello avvisi di hello Centro sicurezza di Azure e viene fornita una panoramica di minacce SQL attive nel database di hello rilevate.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-141">Clicking on hello SQL security tile launches hello Azure Security Center alerts blade and provides an overview of active SQL threats detected on hello database.</span></span> 

  ![Riquadro di spostamento][7]

2. <span data-ttu-id="d8ffb-143">Facendo clic su uno specifico avviso vengono visualizzati altri dettagli e azioni per analizzare la minaccia e risolvere eventuali minacce future.</span><span class="sxs-lookup"><span data-stu-id="d8ffb-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Riquadro di spostamento][8]


## <a name="next-steps"></a><span data-ttu-id="d8ffb-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8ffb-145">Next steps</span></span>

* <span data-ttu-id="d8ffb-146">Altre informazioni sulle funzionalità di rilevamento minacce, visitare hello [blog di Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="d8ffb-146">Learn more about Threat Detection, visit hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="d8ffb-147">Altre informazioni sul [controllo del database SQL di Azure](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="d8ffb-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="d8ffb-148">Altre informazioni sul [Centro sicurezza di Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="d8ffb-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="d8ffb-149">Per ulteriori informazioni sui prezzi, vedere hello [pagina prezzi di Database SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="d8ffb-149">For more details on pricing, please see hello [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="d8ffb-150">Per un esempio di script di PowerShell, vedere [Configurare il controllo del database SQL e il rilevamento delle minacce usando PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d8ffb-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


