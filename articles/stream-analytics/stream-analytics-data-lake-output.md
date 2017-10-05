---
title: Output di Data Lake Store per Analisi di flusso | Documentazione Microsoft
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
ms.openlocfilehash: 3d867df3ef875d5cc41de418c3d1d269ff751fda
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="06c6c-103">Output di Archivio Data Lake per Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="06c6c-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="06c6c-104">I processi di Analisi di flusso supportano numerosi metodi di output, tra cui [Archivio Data Lake di Azure](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="06c6c-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="06c6c-105">Azure Data Lake Store è un repository su vasta scala a livello aziendale per carichi di lavoro di analisi di Big Data.</span><span class="sxs-lookup"><span data-stu-id="06c6c-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="06c6c-106">Archivio Data Lake consente di archiviare dati di qualsiasi dimensione, tipo e velocità di inserimento per le analisi esplorative e operative.</span><span class="sxs-lookup"><span data-stu-id="06c6c-106">Data Lake Store enables you to store data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="06c6c-107">Autorizzare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="06c6c-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="06c6c-108">Quando si seleziona Data Lake Store come output nel portale di Azure, verrà richiesto di autorizzare l'uso del Data Lake Store esistente o di richiedere l'accesso a Data Lake Store tramite il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="06c6c-108">When Data Lake Store is selected as an output in the Azure portal, you will be prompted to authorize use of your existing Data Lake Store or to request access to the Data Lake Store via the Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="06c6c-109">Se si ha già accesso a Data Lake Store, fare clic su "Autorizza ora". Per un breve tempo viene visualizzata una pagina con il messaggio "Reindirizzamento all'autorizzazione in corso".</span><span class="sxs-lookup"><span data-stu-id="06c6c-109">If you already have access to Data Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting to authorization”.</span></span> <span data-ttu-id="06c6c-110">La pagina si chiude automaticamente e verrà visualizzata la pagina che consente di configurare l'output di Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="06c6c-110">The page will automatically close and you will be presented with the page that would allow you to configure the Data Lake Store output.</span></span>

<span data-ttu-id="06c6c-111">Se non si è iscritti a Data Lake Store, è possibile selezionare il collegamento "Iscriversi adesso" per avviare la richiesta, oppure seguire le [istruzioni introduttive](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="06c6c-111">If you have not signed up for Data Lake Store, you can follow the “Sign up now” link to initiate the request, or follow the [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-the-data-lake-store-output-properties"></a><span data-ttu-id="06c6c-112">Configurare le proprietà dell'output di Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="06c6c-112">Configure the Data Lake Store output properties</span></span>
<span data-ttu-id="06c6c-113">Dopo aver autenticato l'account, è possibile configurare le proprietà per l'output di Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="06c6c-113">Once you have the Data Lake Store account authenticated, you can configure the properties for your Data Lake Store output.</span></span> <span data-ttu-id="06c6c-114">La tabella seguente elenca i nomi di proprietà e le relative descrizioni per configurare l'output di Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="06c6c-114">The table below is the list of property names and their description to configure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="06c6c-115"><B>NOME PROPRIETÀ</B></span><span class="sxs-lookup"><span data-stu-id="06c6c-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="06c6c-116"><B>DESCRIZIONE</B></span><span class="sxs-lookup"><span data-stu-id="06c6c-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="06c6c-117">Alias di output</span><span class="sxs-lookup"><span data-stu-id="06c6c-117">Output Alias</span></span></td>
<td><span data-ttu-id="06c6c-118">È un nome descrittivo usato nelle query per indirizzare l'output delle query ad Archivio Data Lake in uso.</span><span class="sxs-lookup"><span data-stu-id="06c6c-118">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="06c6c-119">Account di Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="06c6c-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="06c6c-120">Nome dell'account di archiviazione a cui si sta inviando l'output.</span><span class="sxs-lookup"><span data-stu-id="06c6c-120">The name of the storage account where you are sending your output.</span></span> <span data-ttu-id="06c6c-121">Verrà visualizzato un elenco di account Data Lake Store a cui l'utente connesso può accedere.</span><span class="sxs-lookup"><span data-stu-id="06c6c-121">You will be presented with a list of Data Lake Store accounts  the logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="06c6c-122">Schema prefisso percorso [<I>facoltativo</I>]</span><span class="sxs-lookup"><span data-stu-id="06c6c-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="06c6c-123">Percorso del file usato per scrivere i file nell'account di Archivio Data Lake specificato.</span><span class="sxs-lookup"><span data-stu-id="06c6c-123">The file path used to write your files within the specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="06c6c-124">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="06c6c-124">{date}, {time}</span></span><BR><span data-ttu-id="06c6c-125">Esempio 1: folder1/logs/{date}/{time}</span><span class="sxs-lookup"><span data-stu-id="06c6c-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="06c6c-126">Esempio 2: folder1/logs/{date}</span><span class="sxs-lookup"><span data-stu-id="06c6c-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="06c6c-127">Formato data [<I>facoltativo</I>]</span><span class="sxs-lookup"><span data-stu-id="06c6c-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="06c6c-128">Se nel percorso di prefisso viene usato il token di data, è possibile selezionare il formato della data in cui sono organizzati i file.</span><span class="sxs-lookup"><span data-stu-id="06c6c-128">If the date token is used in the prefix path, you can select the date format in which your files are organized.</span></span> <span data-ttu-id="06c6c-129">Esempio: AAAA/MM/GG</span><span class="sxs-lookup"><span data-stu-id="06c6c-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="06c6c-130">Formato ora [<I>facoltativo</I>]</span><span class="sxs-lookup"><span data-stu-id="06c6c-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="06c6c-131">Se nel percorso di prefisso viene usato il token dell'ora, specificare il formato dell'ora in cui sono organizzati i file.</span><span class="sxs-lookup"><span data-stu-id="06c6c-131">If the time token is used in the prefix path, specify the time format in which your files are organized.</span></span> <span data-ttu-id="06c6c-132">Al momento, l'unico valore supportato è HH.</span><span class="sxs-lookup"><span data-stu-id="06c6c-132">Currently the only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="06c6c-133">Formato di serializzazione eventi</span><span class="sxs-lookup"><span data-stu-id="06c6c-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="06c6c-134">Formato di serializzazione per i dati di output.</span><span class="sxs-lookup"><span data-stu-id="06c6c-134">Serialization format for output data.</span></span> <span data-ttu-id="06c6c-135">Sono supportati i formati JSON, CSV e Avro.</span><span class="sxs-lookup"><span data-stu-id="06c6c-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="06c6c-136">Codifica</span><span class="sxs-lookup"><span data-stu-id="06c6c-136">Encoding</span></span></td>
<td><span data-ttu-id="06c6c-137">Se il formato è CSV o JSON, è necessario specificare un formato di codifica.</span><span class="sxs-lookup"><span data-stu-id="06c6c-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="06c6c-138">Al momento UTF-8 è l'unico formato di codifica supportato.</span><span class="sxs-lookup"><span data-stu-id="06c6c-138">UTF-8 is the only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="06c6c-139">Delimitatore</span><span class="sxs-lookup"><span data-stu-id="06c6c-139">Delimiter</span></span></td>
<td><span data-ttu-id="06c6c-140">Applicabile solo per la serializzazione CSV.</span><span class="sxs-lookup"><span data-stu-id="06c6c-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="06c6c-141">Analisi di flusso supporta una serie di delimitatori comuni per la serializzazione dei dati CSV.</span><span class="sxs-lookup"><span data-stu-id="06c6c-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="06c6c-142">I valori supportati sono virgola, punto e virgola, spazio, tabulazione e barra verticale.</span><span class="sxs-lookup"><span data-stu-id="06c6c-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="06c6c-143">Format</span><span class="sxs-lookup"><span data-stu-id="06c6c-143">Format</span></span></td>
<td><span data-ttu-id="06c6c-144">Applicabile solo per la serializzazione JSON.</span><span class="sxs-lookup"><span data-stu-id="06c6c-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="06c6c-145">Separato da righe specifica che l'output verrà formattato separando ciascun oggetto JSON con una nuova riga.</span><span class="sxs-lookup"><span data-stu-id="06c6c-145">Line separated specifies that the output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="06c6c-146">Array specifica che l'output verrà formattato come array di oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="06c6c-146">Array specifies that the output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="06c6c-147">Rinnovare l'autorizzazione per Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="06c6c-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="06c6c-148">Attualmente esiste una limitazione secondo cui il token di autenticazione deve essere aggiornato manualmente ogni 90 giorni per tutti i processi con output di Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="06c6c-148">Currently, there is a limitation where the authentication token needs to be manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="06c6c-149">È necessario anche autenticare nuovamente l'account di Archivio Data Lake se la password è stata modificata dopo la creazione del processo o dopo l'ultima autenticazione.</span><span class="sxs-lookup"><span data-stu-id="06c6c-149">You will also need to re-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="06c6c-150">Un sintomo di questo problema è la mancanza di output del processo e un errore nei log delle operazioni che indicano la necessità di una nuova autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="06c6c-150">A symptom of this issue is no job output and an error in the Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="06c6c-151">Per risolvere questo problema, arrestare il processo in esecuzione e passare all'output di Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="06c6c-151">To resolve this issue, stop your running job and go to your Data Lake Store output.</span></span> <span data-ttu-id="06c6c-152">Fare clic sul collegamento "Rinnova autorizzazione" e per un istante viene visualizzata una pagina che indica "Reindirizzamento all'autorizzazione..."</span><span class="sxs-lookup"><span data-stu-id="06c6c-152">Click the “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span></span> <span data-ttu-id="06c6c-153">La pagina verrà chiusa automaticamente e, in caso di esito positivo, verrà indicato "Autorizzazione rinnovata".</span><span class="sxs-lookup"><span data-stu-id="06c6c-153">The page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="06c6c-154">È quindi necessario fare clic su "Salva" nella parte inferiore della pagina e, per continuare, riavviare il processo dall'ora dell'ultimo arresto per evitare la perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="06c6c-154">You then need to click “Save” at the bottom of the page, and can proceed by restarting your job from the Last Stopped Time to avoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

