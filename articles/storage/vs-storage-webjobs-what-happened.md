---
title: aaaWhat si sono verificati progetto processo Web toomy (Visual Studio di archiviazione di Azure, servizio connesso)? | Microsoft Docs
description: "Viene descritto cosa è successo in un progetto processo Web di Azure dopo che l'account di archiviazione tooa utilizzando Visual Studio la connessione di servizi connessi"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 7735f49b1e7ec8dda30d1262d7ce65454604b610
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webjob-project-visual-studio-azure-storage-connected-service"></a>Il progetto processo Web verificato anomalo toomy (Visual Studio di archiviazione di Azure, servizio connesso)?
## <a name="references-added"></a>Aggiunta di riferimenti
pacchetto NuGet di archiviazione di Azure Hello è stato aggiunto tooor aggiornata nel progetto di Visual Studio.  
Questo pacchetto aggiunge hello segue i riferimenti .NET:

* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.WindowsAzure.ConfigurationManager**
* **Microsoft.WindowsAzure.Storage**
* **Newtonsoft.Json**
* **System.Data**
* **System.Spatial**

## <a name="connection-string-for-azure-storage-added"></a>Aggiunta di stringa di connessione per l'Archiviazione di Azure
Nel file app. config di hello del progetto, hello **AzureWebJobsStorage** e **AzureWebJobsDashboard** voci sono state aggiornate con stringa di connessione e la chiave dell'account di archiviazione hello selezionato.

Per altre informazioni, vedere [Risorse di documentazione di Processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).

