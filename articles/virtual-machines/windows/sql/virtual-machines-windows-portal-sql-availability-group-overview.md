---
title: "Panoramica di gruppi di disponibilità Server - macchine virtuali di Azure - aaaSQL | Documenti Microsoft"
description: "Questo articolo offre una panoramica sui gruppi di disponibilità di SQL Server in macchine virtuali di Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>Panoramica sui gruppi di disponibilità AlwaysOn di SQL Server in macchine virtuali di Azure #

Questo articolo offre una panoramica sui gruppi di disponibilità di SQL Server in macchine virtuali di Azure. 

Sempre in gruppi di disponibilità nelle macchine virtuali Azure sono simili tooAlways gruppi di disponibilità in locale. Per altre informazioni, vedere [Gruppi di disponibilità AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx). 

diagramma di Hello sono illustrate hello parti di un gruppo di disponibilità Server nelle macchine virtuali di Azure SQL completo.

![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

Hello differenza fondamentale per un gruppo di disponibilità in macchine virtuali di Azure è che hello macchine virtuali di Azure, richiedono un [bilanciamento del carico](../../../load-balancer/load-balancer-overview.md). servizio di bilanciamento del carico Hello contiene indirizzi IP hello per listener del gruppo di disponibilità hello. Se sono disponibili più gruppi di disponibilità, è necessario un listener per ogni gruppo. Un servizio di bilanciamento del carico può supportare più listener.

Quando si è pronti toobuild un aroup di disponibilità di SQL Server in macchine virtuali di Azure, vedere le esercitazioni toothese.

## <a name="automatically-create-an-availability-group-from-a-template"></a>Creare automaticamente un gruppo di disponibilità da un modello

[Configurare automaticamente il gruppo di disponibilità AlwaysOn in macchine virtuali di Azure con Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a>Creare manualmente un gruppo di disponibilità nel portale di Azure

È possibile inoltre creare macchine virtuali hello manualmente senza modello hello. Innanzitutto, completare i prerequisiti di hello, quindi creare il gruppo di disponibilità hello. Vedere hello seguenti argomenti: 

- [Completare i prerequisiti per la creazione di gruppi di disponibilità AlwaysOn in macchine virtuali di Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [Ripristino di emergenza e disponibilità tooimprove Crea gruppo di disponibilità AlwaysOn](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a>Passaggi successivi

[Configurare un gruppo di disponibilità SQL Server AlwaysOn in Macchine virtuali di Azure](virtual-machines-windows-portal-sql-availability-group-dr.md).
