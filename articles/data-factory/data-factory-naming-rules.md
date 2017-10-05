---
title: "Regole per la denominazione delle entità di Azure Data Factory | Microsoft Docs"
description: "Descrive le regole di denominazione per le entità di Data factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d447bbceb4ab344e011311eaf143b20f0a0400d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="da7f5-103">Azure Data Factory - Regole di denominazione</span><span class="sxs-lookup"><span data-stu-id="da7f5-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="da7f5-104">La tabella seguente specifica le regole di denominazione per gli elementi di Data factory.</span><span class="sxs-lookup"><span data-stu-id="da7f5-104">The following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="da7f5-105">Nome</span><span class="sxs-lookup"><span data-stu-id="da7f5-105">Name</span></span> | <span data-ttu-id="da7f5-106">Univocità del nome</span><span class="sxs-lookup"><span data-stu-id="da7f5-106">Name Uniqueness</span></span> | <span data-ttu-id="da7f5-107">Controlli di convalida</span><span class="sxs-lookup"><span data-stu-id="da7f5-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="da7f5-108">Data factory</span><span class="sxs-lookup"><span data-stu-id="da7f5-108">Data Factory</span></span> |<span data-ttu-id="da7f5-109">Univoco in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="da7f5-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="da7f5-110">Per i nomi non viene fatta distinzione tra maiuscole e minuscole: `MyDF` e `mydf`, ad esempio, fanno riferimento alla stessa data factory.</span><span class="sxs-lookup"><span data-stu-id="da7f5-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer to the same data factory.</span></span> |<ul><li><span data-ttu-id="da7f5-111">Ogni data factory è collegata a una sola sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="da7f5-111">Each data factory is tied to exactly one Azure subscription.</span></span></li><li><span data-ttu-id="da7f5-112">I nomi degli oggetti devono iniziare con una lettera o un numero e possono contenere solo lettere, numeri e il carattere trattino (-).</span><span class="sxs-lookup"><span data-stu-id="da7f5-112">Object names must start with a letter or a number, and can contain only letters, numbers, and the dash (-) character.</span></span></li><li><span data-ttu-id="da7f5-113">Ogni carattere trattino (-) deve essere immediatamente preceduto e seguito da una lettera o un numero.</span><span class="sxs-lookup"><span data-stu-id="da7f5-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="da7f5-114">Nei nomi di contenitori non sono consentiti trattini consecutivi.</span><span class="sxs-lookup"><span data-stu-id="da7f5-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="da7f5-115">Il nome può contenere da 3 a 63 caratteri.</span><span class="sxs-lookup"><span data-stu-id="da7f5-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="da7f5-116">Servizi collegati/Tabelle/Pipeline</span><span class="sxs-lookup"><span data-stu-id="da7f5-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="da7f5-117">Univoco in una data factory.</span><span class="sxs-lookup"><span data-stu-id="da7f5-117">Unique with in a data factory.</span></span> <span data-ttu-id="da7f5-118">Per i nomi viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="da7f5-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="da7f5-119">Numero massimo di caratteri nel nome di una tabella: 260.</span><span class="sxs-lookup"><span data-stu-id="da7f5-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="da7f5-120">I nomi degli oggetti devono iniziare con una lettera, un numero o un carattere di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="da7f5-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="da7f5-121">Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\".</span><span class="sxs-lookup"><span data-stu-id="da7f5-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="da7f5-122">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="da7f5-122">Resource Group</span></span> |<span data-ttu-id="da7f5-123">Univoco in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="da7f5-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="da7f5-124">Per i nomi viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="da7f5-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="da7f5-125">Numero massimo di caratteri: 1000.</span><span class="sxs-lookup"><span data-stu-id="da7f5-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="da7f5-126">Il nome può contenere lettere, cifre e i caratteri seguenti: "-", "_", "," e "."</span><span class="sxs-lookup"><span data-stu-id="da7f5-126">Name can contain letters, digits, and the following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

