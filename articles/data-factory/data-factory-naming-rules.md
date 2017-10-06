---
title: "aaaRules per la denominazione delle entità di Azure Data Factory | Documenti Microsoft"
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
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="a4391-103">Azure Data Factory - Regole di denominazione</span><span class="sxs-lookup"><span data-stu-id="a4391-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="a4391-104">Hello nella tabella seguente fornisce le regole di denominazione per gli elementi Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a4391-104">hello following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="a4391-105">Nome</span><span class="sxs-lookup"><span data-stu-id="a4391-105">Name</span></span> | <span data-ttu-id="a4391-106">Univocità del nome</span><span class="sxs-lookup"><span data-stu-id="a4391-106">Name Uniqueness</span></span> | <span data-ttu-id="a4391-107">Controlli di convalida</span><span class="sxs-lookup"><span data-stu-id="a4391-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a4391-108">Data factory</span><span class="sxs-lookup"><span data-stu-id="a4391-108">Data Factory</span></span> |<span data-ttu-id="a4391-109">Univoco in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a4391-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="a4391-110">I nomi sono tra maiuscole e minuscole, vale a dire `MyDF` e `mydf` riferimento toohello stessa data factory.</span><span class="sxs-lookup"><span data-stu-id="a4391-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer toohello same data factory.</span></span> |<ul><li><span data-ttu-id="a4391-111">Ogni data factory è abbinato tooexactly una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4391-111">Each data factory is tied tooexactly one Azure subscription.</span></span></li><li><span data-ttu-id="a4391-112">I nomi degli oggetti deve iniziare con una lettera o un numero e può contenere solo lettere, numeri e hello trattino (-).</span><span class="sxs-lookup"><span data-stu-id="a4391-112">Object names must start with a letter or a number, and can contain only letters, numbers, and hello dash (-) character.</span></span></li><li><span data-ttu-id="a4391-113">Ogni carattere trattino (-) deve essere immediatamente preceduto e seguito da una lettera o un numero.</span><span class="sxs-lookup"><span data-stu-id="a4391-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="a4391-114">Nei nomi di contenitori non sono consentiti trattini consecutivi.</span><span class="sxs-lookup"><span data-stu-id="a4391-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="a4391-115">Il nome può contenere da 3 a 63 caratteri.</span><span class="sxs-lookup"><span data-stu-id="a4391-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="a4391-116">Servizi collegati/Tabelle/Pipeline</span><span class="sxs-lookup"><span data-stu-id="a4391-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="a4391-117">Univoco in una data factory.</span><span class="sxs-lookup"><span data-stu-id="a4391-117">Unique with in a data factory.</span></span> <span data-ttu-id="a4391-118">Per i nomi viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="a4391-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="a4391-119">Numero massimo di caratteri nel nome di una tabella: 260.</span><span class="sxs-lookup"><span data-stu-id="a4391-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="a4391-120">I nomi degli oggetti devono iniziare con una lettera, un numero o un carattere di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="a4391-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="a4391-121">Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\".</span><span class="sxs-lookup"><span data-stu-id="a4391-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="a4391-122">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a4391-122">Resource Group</span></span> |<span data-ttu-id="a4391-123">Univoco in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a4391-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="a4391-124">Per i nomi viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="a4391-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="a4391-125">Numero massimo di caratteri: 1000.</span><span class="sxs-lookup"><span data-stu-id="a4391-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="a4391-126">Nome può contenere lettere, cifre e hello seguenti caratteri: "-", "_",","e"."</span><span class="sxs-lookup"><span data-stu-id="a4391-126">Name can contain letters, digits, and hello following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

