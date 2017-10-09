---
title: aaaEnable agente della macchina virtuale in Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * abilitare VM agente * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a>Abilita l'agente di macchine virtuali nel Centro sicurezza di Azure
Hello agente della macchina virtuale deve essere installato nelle macchine virtuali (VM) in ordine troppo[Abilita raccolta dati](security-center-enable-data-collection.md).  Abilita il Centro sicurezza di Azure è toosee che richiedono che le macchine virtuali hello agente VM e consiglia di abilitare hello agente VM su tali macchine virtuali.

Hello agente VM viene installato per impostazione predefinita per le macchine virtuali distribuite da hello Azure Marketplace. articolo Hello [agente VM ed estensioni-parte 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) vengono fornite informazioni su come tooinstall hello agente della macchina virtuale.

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione. Questa non è una guida dettagliata.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **pannello indicazioni**selezionare **abilitare agente VM**.
   ![Abilita l'agente di macchine virtuali][1]
2. Verrà aperto il pannello hello **VM agente mancante o non risponde**. Questo pannello sono elencate le macchine virtuali hello che richiedono hello agente della macchina virtuale. Istruzioni hello sull'agente VM di hello pannello tooinstall hello.
   ![L'agente di macchine virtuali non è present][2]

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md)-informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md): informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md)-informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md)-informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md)-domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/)-ottenere informazioni e notizie sicurezza di Azure hello.

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
