---
title: Convalida in Centro sicurezza di Azure aaaAlerts | Documenti Microsoft
description: Questo documento consente di avvisi di sicurezza toovalidate hello in Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Convalida degli avvisi nel Centro sicurezza di Azure
Questo documento vengono illustrate come tooverify se il sistema è configurato correttamente per gli avvisi del Centro sicurezza di Azure.

## <a name="what-are-security-alerts"></a>Informazioni sugli avvisi di sicurezza
Centro sicurezza PC automaticamente raccoglie, analizza e consente di integrare dati di log da risorse di Azure, rete hello e soluzioni partner connessi, come soluzioni di protezione firewall ed endpoint, toodetect e avvisi è toothreats. Lettura [toosecurity risponda e gestire gli avvisi in Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) per ulteriori informazioni su avvisi di sicurezza e lettura [informazioni sugli avvisi di sicurezza nel Centro protezione Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn più hello diversi tipi di avvisi.

## <a name="alert-validation"></a>Convalida degli avvisi
Dopo che l'agente protezione Center è installato nel computer in uso, eseguire operazioni di hello seguenti dal computer hello in cui si desidera toobe hello attaccata di risorse di avviso hello:

1. Copiare un file eseguibile (per esempio calc.exe) toohello del PC o altra directory di praticità.
2. Rinominare il file troppo**ASC_AlertTest_662jfi039N.exe**.
3. Aprire il prompt dei comandi di hello ed eseguire il file con un argomento (un solo argomento fittizio nome), ad esempio: *ASC_AlertTest_662jfi039N.exe - foo*
4. Attendere 5 minuti too10 e aprire gli avvisi del Centro protezione. Sono disponibili un avviso toofollowing simili uno:

    ![Convalida degli avvisi](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

Quando si rivede questo avviso, assicurarsi che il campo di hello argomenti attivato il controllo viene visualizzato come true. Se viene visualizzato false, è necessario tooenable di argomenti della riga di comando di controllo. È possibile abilitare questa opzione utilizzando hello seguente riga di comando:

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>Vedere anche
In questo articolo ha introdotto toohello processo di convalida di avvisi. Ora che si ha familiarità con la convalida, provare a hello seguenti articoli:

* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Informazioni su come toomanage avvisi e gli eventi imprevisti toosecurity rispondono in Centro sicurezza PC.
* [Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md). Informazioni su come toomonitor hello integrità delle risorse di Azure.
* [Informazioni sugli avvisi di sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Informazioni sui tipi diversi di hello degli avvisi di sicurezza.
* [Guida alla risoluzione dei problemi del Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Informazioni su come tootroubleshoot comuni problemi nel Centro protezione. 
* [Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md). Trovare le domande frequenti sull'utilizzo del servizio hello.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/). Post di blog sulla sicurezza e sulla conformità di Azure.

