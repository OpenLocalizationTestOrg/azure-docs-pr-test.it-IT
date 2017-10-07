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
# <a name="stream-analytics-data-lake-store-output"></a>Output di Archivio Data Lake per Analisi di flusso
I processi di Analisi di flusso supportano numerosi metodi di output, tra cui [Archivio Data Lake di Azure](https://azure.microsoft.com/services/data-lake-store/). Azure Data Lake Store è un repository su vasta scala a livello aziendale per carichi di lavoro di analisi di Big Data. Archivio Data Lake consente toostore dati di qualsiasi dimensione, tipo e l'inserimento di velocità per analitica operative ed esplorative.

## <a name="authorize-a-data-lake-store-account"></a>Autorizzare un account Archivio Data Lake
1. Quando archivio Data Lake è selezionato come output nel portale di Azure hello, sarà necessario utilizzare tooauthorize delle toorequest esistente archivio Data Lake accedere archivio Data Lake di toohello tramite hello portale classico.
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. Se si dispone già di accesso tooData Lake archivio, fare clic su "autorizza" e per un breve periodo di una pagina viene visualizzata che indica "Reindirizzamento tooauthorization". pagina Hello verrà chiusa automaticamente e verrà visualizzato con una pagina hello che permetterebbe tooconfigure hello archivio Data Lake output.

Se non sei iscritto per archivio Data Lake, è possibile seguire hello "Iscrizione" tooinitiate hello richiesta di collegamento o seguire hello [istruzioni avviata](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="configure-hello-data-lake-store-output-properties"></a>Configurare le proprietà di output di hello archivio Data Lake
Dopo aver creato account archivio Data Lake hello autenticato, è possibile configurare le proprietà di hello per l'archivio Data Lake di output. tabella Hello riportata di seguito è riportato hello elenco di nomi di proprietà e i relativi tooconfigure descrizione che l'archivio Data Lake di output.

<table>
<tbody>
<tr>
<td><B>NOME PROPRIETÀ</B></td>
<td><B>DESCRIZIONE</B></td>
</tr>
<tr>
<td>Alias di output</td>
<td>Si tratta di un nome descrittivo utilizzato nella query toodirect hello query output toothis archivio Data Lake.</td>
</tr>
<tr>
<td>Account di Archivio Data Lake</td>
<td>nome Hello hello dell'account di archiviazione in cui si invia l'output. Verrà visualizzato un elenco di account archivio Data Lake hello utente connesso deve accedere.</td>
</tr>
<tr>
<td>Schema prefisso percorso [<I>facoltativo</I>]</td>
<td>Hello toowrite percorso file del file all'interno di hello specificati Account archivio Data Lake. <BR>{date}, {time}<BR>Esempio 1: folder1/logs/{date}/{time}<BR>Esempio 2: folder1/logs/{date}</td>
</tr>
<tr>
<td>Formato data [<I>facoltativo</I>]</td>
<td>Se il token di data hello viene utilizzato nel percorso di prefisso hello, è possibile selezionare il formato di data hello in cui sono organizzati i file. Esempio: AAAA/MM/GG</td>
</tr>
<tr>
<td>Formato ora [<I>facoltativo</I>]</td>
<td>Se il token di tempo hello viene utilizzato nel percorso di prefisso hello, specificare il formato di ora hello in cui i file sono organizzati. Il valore di hello solo supportato attualmente è HH.</td>
</tr>
<tr>
<td>Formato di serializzazione eventi</td>
<td>Formato di serializzazione per i dati di output. Sono supportati i formati JSON, CSV e Avro.</td>
</tr>
<tr>
<td>Codifica</td>
<td>Se il formato è CSV o JSON, è necessario specificare un formato di codifica. UTF-8 è hello formato di codifica è supportata solo in questo momento.</td>
</tr>
<tr>
<td>Delimitatore</td>
<td>Applicabile solo per la serializzazione CSV. Analisi di flusso supporta una serie di delimitatori comuni per la serializzazione dei dati CSV. I valori supportati sono virgola, punto e virgola, spazio, tabulazione e barra verticale.</td>
</tr>
<tr>
<td>Format</td>
<td>Applicabile solo per la serializzazione JSON. Separato da righe specifica che verrà formattato output di hello con ogni oggetto JSON sia separato da una nuova riga. Matrice specifica che verrà formattato come una matrice di oggetti JSON output di hello.</td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a>Rinnovare l'autorizzazione per Archivio Data Lake
Attualmente, è presente una limitazione in cui il token di autenticazione hello deve toobe aggiornate manualmente ogni 90 giorni per tutti i processi con l'output di archivio Data Lake. È inoltre necessario toore-autenticazione account archivio Data Lake se è stata modificata la password poiché il processo di creazione o dell'ultima autenticazione. Un sintomo del problema è un errore nel log delle operazioni hello segnalerà necessità per l'autorizzazione e nessun output del processo.

tooresolve questo problema, arrestare il processo in esecuzione e passare l'archivio tooyour Data Lake di output. Fare clic sul collegamento "Rinnovo authorization" hello e per un breve periodo di una pagina viene visualizzata che indica "Reindirizzamento tooauthorization".... pagina Hello verrà chiusa automaticamente e se ha esito positivo, verrà indicato "Autorizzazione è stata rinnovata". Quindi necessario tooclick "Salva" nella parte inferiore di hello della pagina hello e può continuare, riavviare il processo dalla perdita di dati di ora ultimo arresto tooavoid hello.

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

