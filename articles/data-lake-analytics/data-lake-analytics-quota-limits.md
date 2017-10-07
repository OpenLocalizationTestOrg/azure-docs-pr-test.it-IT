---
title: i limiti di Quota Data Lake Analitica aaaAzure | Documenti Microsoft
description: Informazioni su come tooadjust e aumento della quota limita negli account di Azure Data Lake Analitica (ADLA).
services: data-lake-analytics
keywords: Azure Data Lake Analytics.
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a>Limiti di quota di Azure Data Lake Analytics

Informazioni su come tooadjust e aumento della quota limita negli account di Azure Data Lake Analitica (ADLA). La conoscenza di questi limiti può aiutare a comprendere il comportamento del processo U-SQL. Tutti i limiti di quota sono trasferibili, pertanto è possibile aumentare i limiti massimi di hello raggiungendo toous.

## <a name="azure-subscriptions-limits"></a>Limiti delle sottoscrizioni Azure

**Numero massimo di account di ADLA per sottoscrizione:**  5

 Si tratta hello il numero massimo di account ADLA che è possibile creare per ogni sottoscrizione. Se si tenta di account ADLA toocreate un sesto, si verificherà un errore "È stato raggiunto numero massimo di hello di account Data Lake Analitica consentiti (5) nell'area sotto il nome di sottoscrizione". In questo caso, eliminare qualsiasi account ADLA inutilizzati o raggiungere toous da [aprendo un ticket di supporto](#increase-maximum-quota-limits).

## <a name="adla-account-limits"></a>Limiti degli account di ADLA

**Numero massimo di unità di analisi per account:** 250

Si tratta di numero massimo di hello di AUs che possono essere eseguiti contemporaneamente nel tuo account. Se il totale delle unità di analisi dei processi in esecuzione supera questo limite, i processi più recenti vengono accodati automaticamente. ad esempio:

* Se si dispone di un solo processo in esecuzione con 250 Australia, quando si invia un secondo processo rimarrà in attesa nella coda del processo hello finché hello primo processo viene completato.
* Se si dispone di cinque processi in esecuzione e ognuno utilizza 50 Australia, quando si invia un processo sesto necessarie 20 AUs è in attesa nella coda del processo hello fino a quando non sono presenti 20 AUs disponibili.

**Numero massimo di processi simultanei di U-SQL per ogni account:** 20

Si tratta hello numero massimo di processi che possono essere eseguiti contemporaneamente nel tuo account. Al di sopra di questo valore, i processi più recenti vengono accodati automaticamente.

## <a name="adjust-adla-quota-limits-per-account"></a>Modificare i limiti di quota di Azure Data Lake Analytics per ogni account

1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Scegliere un account ADLA esistente.
3. Fare clic su **Proprietà**.
4. Regolare **parallelismo** e **processi simultanei** toosuit le proprie esigenze.

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a>Aumentare i limiti massimi di quota

1. Aprire una richiesta di supporto nel portale di Azure.

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. Selezionare il tipo di problema hello **Quota**.
3. Selezionare la propria **sottoscrizione** (assicurarsi che non sia una sottoscrizione di "prova").
4. Selezionare il tipo di quota **Data Lake Analytics**.

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. Nel pannello problema hello, spiegare il limite di aumento richiesto con **dettagli** di motivo per cui è necessario questa capacità aggiuntiva.

    ![Pannello del portale di Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. Verificare le informazioni di contatto e creare la richiesta di supporto hello.

Microsoft esamina la richiesta e tenta di tooaccommodate le esigenze aziendali appena possibile.

## <a name="next-steps"></a>Passaggi successivi

* [Panoramica di Analisi Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Gestire Azure Data Lake Analytics tramite Azure PowerShell](data-lake-analytics-manage-use-powershell.md)
* [Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
