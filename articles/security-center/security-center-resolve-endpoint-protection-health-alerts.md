---
title: "avvisi di integrità aaaResolve endpoint protection in Centro sicurezza di Azure | Documenti Microsoft"
description: "Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * risolvere Endpoint Protection integrità avvisi * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Risolvere gli avvisi sull'integrità della protezione degli endpoint nel Centro sicurezza di Azure
Il Centro sicurezza di Azure consiglia di risolvere gli avvisi sull'integrità della protezione degli endpoint rilevati.  Centro sicurezza PC consente toosee quali macchine virtuali (VM) sono errori di endpoint protection e il numero di errori.

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione. Questa non è una guida dettagliata.
> 
> 

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **pannello indicazioni**selezionare **gli avvisi di integrità di Endpoint Protection risolvere**.
   ![Risolvere gli avvisi sull'integrità della protezione degli endpoint][1]
2. Verrà aperto il pannello hello **errore di Endpoint Protection** in cui sono elencate le macchine virtuali con gli errori e il numero di hello di errori per ogni macchina virtuale. Selezionare una macchina virtuale dall'elenco di hello.
   ![Endpoint protection failure][2]
3. Oggetto **elenco errori** pannello apre per hello selezionato VM, che visualizza un elenco di errori. Selezionare un errore hello elenco toolearn altre. Verrà aperto un pannello con informazioni sull'errore hello selezionato.
   ![Elenco degli errori][3]
   ![Evento di errore][4]

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
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
