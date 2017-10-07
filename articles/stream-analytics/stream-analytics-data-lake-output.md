---
title: aaaStream Analitica Data Lake archivio Output | Documenti Microsoft
description: Configurazione dell'autenticazione e dell'autorizzazione di un Archivio Data Lake di Azure in un processo di analisi di flusso
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="f3c40-103">Output di Archivio Data Lake per Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="f3c40-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="f3c40-104">I processi di Analisi di flusso supportano numerosi metodi di output, tra cui [Archivio Data Lake di Azure](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="f3c40-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="f3c40-105">Azure Data Lake Store è un repository su vasta scala a livello aziendale per carichi di lavoro di analisi di Big Data.</span><span class="sxs-lookup"><span data-stu-id="f3c40-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="f3c40-106">Archivio Data Lake consente toostore dati di qualsiasi dimensione, tipo e l'inserimento di velocità per analitica operative ed esplorative.</span><span class="sxs-lookup"><span data-stu-id="f3c40-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="f3c40-107">Autorizzare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="f3c40-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="f3c40-108">Quando archivio Data Lake è selezionato come output nel portale di Azure hello, sarà necessario utilizzare tooauthorize delle toorequest esistente archivio Data Lake accedere archivio Data Lake di toohello tramite hello portale classico.</span><span class="sxs-lookup"><span data-stu-id="f3c40-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="f3c40-109">Se si dispone già di accesso tooData Lake archivio, fare clic su "autorizza" e per un breve periodo di una pagina viene visualizzata che indica "Reindirizzamento tooauthorization".</span><span class="sxs-lookup"><span data-stu-id="f3c40-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="f3c40-110">pagina Hello verrà chiusa automaticamente e verrà visualizzato con una pagina hello che permetterebbe tooconfigure hello archivio Data Lake output.</span><span class="sxs-lookup"><span data-stu-id="f3c40-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="f3c40-111">Se non sei iscritto per archivio Data Lake, è possibile seguire hello "Iscrizione" tooinitiate hello richiesta di collegamento o seguire hello [istruzioni avviata](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f3c40-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="f3c40-112">Configurare le proprietà di output di hello archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="f3c40-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="f3c40-113">Dopo aver creato account archivio Data Lake hello autenticato, è possibile configurare le proprietà di hello per l'archivio Data Lake di output.</span><span class="sxs-lookup"><span data-stu-id="f3c40-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="f3c40-114">tabella Hello riportata di seguito è riportato hello elenco di nomi di proprietà e i relativi tooconfigure descrizione che l'archivio Data Lake di output.</span><span class="sxs-lookup"><span data-stu-id="f3c40-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="f3c40-115"><B>NOME PROPRIETÀ</B></span><span class="sxs-lookup"><span data-stu-id="f3c40-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="f3c40-116"><B>DESCRIZIONE</B></span><span class="sxs-lookup"><span data-stu-id="f3c40-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f3c40-117">Alias di output</span><span class="sxs-lookup"><span data-stu-id="f3c40-117">Output Alias</span></span></td>
<td><span data-ttu-id="f3c40-118">Si tratta di un nome descrittivo utilizzato nella query toodirect hello query output toothis archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f3c40-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f3c40-119">Account di Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="f3c40-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="f3c40-120">nome Hello hello dell'account di archiviazione in cui si invia l'output.</span><span class="sxs-lookup"><span data-stu-id="f3c40-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="f3c40-121">Verrà visualizzato un elenco di account archivio Data Lake hello utente connesso deve accedere.</span><span class="sxs-lookup"><span data-stu-id="f3c40-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f3c40-122">Schema prefisso percorso [<I>facoltativo</I>]</span><span class="sxs-lookup"><span data-stu-id="f3c40-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="f3c40-123">Hello toowrite percorso file del file all'interno di hello specificati Account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f3c40-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="f3c40-124">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="f3c40-124">{date}, {time}</span></span><BR><span data-ttu-id="f3c40-125">Esempio 1: folder1/logs/{date}/{time}</span><span class="sxs-lookup"><span data-stu-id="f3c40-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="f3c40-126">Esempio 2: folder1/logs/{date}</span><span class="sxs-lookup"><span data-stu-id="f3c40-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f3c40-127">Formato data [<I>facoltativo</I>]</span><span class="sxs-lookup"><span data-stu-id="f3c40-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="f3c40-128">Se il token di data hello viene utilizzato nel percorso di prefisso hello, è possibile selezionare il formato di data hello in cui sono organizzati i file.</span><span class="sxs-lookup"><span data-stu-id="f3c40-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="f3c40-129">Esempio: AAAA/MM/GG</span><span class="sxs-lookup"><span data-stu-id="f3c40-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f3c40-130">Formato ora [<I>facoltativo</I>]</span><span class="sxs-lookup"><span data-stu-id="f3c40-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="f3c40-131">Se il token di tempo hello viene utilizzato nel percorso di prefisso hello, specificare il formato di ora hello in cui i file sono organizzati.</span><span class="sxs-lookup"><span data-stu-id="f3c40-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="f3c40-132">Il valore di hello solo supportato attualmente è HH.</span><span class="sxs-lookup"><span data-stu-id="f3c40-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f3c40-133">Formato di serializzazione eventi</span><span class="sxs-lookup"><span data-stu-id="f3c40-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="f3c40-134">Formato di serializzazione per i dati di output.</span><span class="sxs-lookup"><span data-stu-id="f3c40-134">Serialization format for output data.</span></span> <span data-ttu-id="f3c40-135">Sono supportati i formati JSON, CSV e Avro.</span><span class="sxs-lookup"><span data-stu-id="f3c40-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f3c40-136">Codifica</span><span class="sxs-lookup"><span data-stu-id="f3c40-136">Encoding</span></span></td>
<td><span data-ttu-id="f3c40-137">Se il formato è CSV o JSON, è necessario specificare un formato di codifica.</span><span class="sxs-lookup"><span data-stu-id="f3c40-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="f3c40-138">UTF-8 è hello formato di codifica è supportata solo in questo momento.</span><span class="sxs-lookup"><span data-stu-id="f3c40-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f3c40-139">Delimitatore</span><span class="sxs-lookup"><span data-stu-id="f3c40-139">Delimiter</span></span></td>
<td><span data-ttu-id="f3c40-140">Applicabile solo per la serializzazione CSV.</span><span class="sxs-lookup"><span data-stu-id="f3c40-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="f3c40-141">Analisi di flusso supporta una serie di delimitatori comuni per la serializzazione dei dati CSV.</span><span class="sxs-lookup"><span data-stu-id="f3c40-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="f3c40-142">I valori supportati sono virgola, punto e virgola, spazio, tabulazione e barra verticale.</span><span class="sxs-lookup"><span data-stu-id="f3c40-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f3c40-143">Format</span><span class="sxs-lookup"><span data-stu-id="f3c40-143">Format</span></span></td>
<td><span data-ttu-id="f3c40-144">Applicabile solo per la serializzazione JSON.</span><span class="sxs-lookup"><span data-stu-id="f3c40-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="f3c40-145">Separato da righe specifica che verrà formattato output di hello con ogni oggetto JSON sia separato da una nuova riga.</span><span class="sxs-lookup"><span data-stu-id="f3c40-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="f3c40-146">Matrice specifica che verrà formattato come una matrice di oggetti JSON output di hello.</span><span class="sxs-lookup"><span data-stu-id="f3c40-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="f3c40-147">Rinnovare l'autorizzazione per Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="f3c40-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="f3c40-148">Attualmente, è presente una limitazione in cui il token di autenticazione hello deve toobe aggiornate manualmente ogni 90 giorni per tutti i processi con l'output di archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f3c40-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="f3c40-149">È inoltre necessario toore-autenticazione account archivio Data Lake se è stata modificata la password poiché il processo di creazione o dell'ultima autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f3c40-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="f3c40-150">Un sintomo del problema è un errore nel log delle operazioni hello segnalerà necessità per l'autorizzazione e nessun output del processo.</span><span class="sxs-lookup"><span data-stu-id="f3c40-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="f3c40-151">tooresolve questo problema, arrestare il processo in esecuzione e passare l'archivio tooyour Data Lake di output.</span><span class="sxs-lookup"><span data-stu-id="f3c40-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="f3c40-152">Fare clic sul collegamento "Rinnovo authorization" hello e per un breve periodo di una pagina viene visualizzata che indica "Reindirizzamento tooauthorization"....</span><span class="sxs-lookup"><span data-stu-id="f3c40-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="f3c40-153">pagina Hello verrà chiusa automaticamente e se ha esito positivo, verrà indicato "Autorizzazione è stata rinnovata".</span><span class="sxs-lookup"><span data-stu-id="f3c40-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="f3c40-154">Quindi necessario tooclick "Salva" nella parte inferiore di hello della pagina hello e può continuare, riavviare il processo dalla perdita di dati di ora ultimo arresto tooavoid hello.</span><span class="sxs-lookup"><span data-stu-id="f3c40-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

