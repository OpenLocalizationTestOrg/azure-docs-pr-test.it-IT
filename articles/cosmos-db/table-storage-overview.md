---
title: Panoramica di Archiviazione tabelle di Azure | Microsoft Docs
description: Archiviare dati non strutturati nel cloud con il servizio di archiviazione tabelle di Azure, ovvero un archivio dati NoSQL.
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/23/2017
ms.author: mimig
ms.openlocfilehash: 9099e90c402185b371495379db943d64fb82cdb8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-table-storage-overview"></a><span data-ttu-id="5f5cd-103">Panoramica di Archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="5f5cd-103">Azure Table storage overview</span></span>

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="5f5cd-104">L'archiviazione tabelle di Azure è un servizio che archivia dati NoSQL strutturati nel cloud, mettendo a disposizione un archivio di chiavi/attributi senza schema.</span><span class="sxs-lookup"><span data-stu-id="5f5cd-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="5f5cd-105">Poiché l'archiviazione tabelle è senza schema, è facile adattare i dati con il variare delle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f5cd-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="5f5cd-106">L'accesso ai dati dell'archiviazione tabelle è rapido ed economico per molti tipi di applicazioni e presenta costi generalmente più bassi rispetto alle soluzioni SQL tradizionali per volumi di dati simili.</span><span class="sxs-lookup"><span data-stu-id="5f5cd-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="5f5cd-107">È possibile usare l'archiviazione tabelle per archiviare set di dati flessibili, ad esempio i dati utente per le applicazioni Web, le rubriche, le informazioni sui dispositivi o altri tipi di metadati richiesti dal servizio.</span><span class="sxs-lookup"><span data-stu-id="5f5cd-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="5f5cd-108">In una tabella possono essere archiviate il numero desiderato di tabelle e un account di archiviazione può contenere un numero qualsiasi di tabelle, fino a che non viene raggiunto il limite di capacità dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5f5cd-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5f5cd-109">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5f5cd-109">Next steps</span></span>

* <span data-ttu-id="5f5cd-110">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma gratuita di Microsoft che consente di rappresentare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="5f5cd-110">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* [<span data-ttu-id="5f5cd-111">Introduzione all'archiviazione tabelle di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="5f5cd-111">Getting Started with Azure Table Storage in .NET</span></span>](table-storage-how-to-use-dotnet.md)

* <span data-ttu-id="5f5cd-112">Per informazioni dettagliate sulle API disponibili, vedere la documentazione di riferimento del servizio tabelle:</span><span class="sxs-lookup"><span data-stu-id="5f5cd-112">View the Table service reference documentation for complete details about available APIs:</span></span>

    * [<span data-ttu-id="5f5cd-113">Informazioni di riferimento sulla libreria client di archiviazione per .NET</span><span class="sxs-lookup"><span data-stu-id="5f5cd-113">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

    * [<span data-ttu-id="5f5cd-114">Informazioni di riferimento sulle API REST</span><span class="sxs-lookup"><span data-stu-id="5f5cd-114">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
