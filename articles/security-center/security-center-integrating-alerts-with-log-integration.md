---
title: integrazione di log aaaIntegrating gli avvisi di Centro sicurezza di Azure con Azure | Documenti Microsoft
description: Questo articolo consente di iniziare a usare gli avvisi del Centro sicurezza con l'integrazione dei log di Azure.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>Integrazione degli avvisi del Centro sicurezza di Azure con l'integrazione dei log di Azure
Molte operazioni di sicurezza e i team di risposta agli eventi imprevisti si basano su una soluzione di informazioni di sicurezza e gestione di eventi (SIEM) come punto di partenza per la valutazione e analisi degli avvisi di sicurezza hello. Con l'integrazione dei log di Azure è possibile integrare gli avvisi del Centro sicurezza di Azure con la soluzione SIEM in uso.

L'integrazione dei log di Azure supporta attualmente HP ArcSight, Splunk e IBM QRadar.

## <a name="what-logs-can-i-integrate"></a>Quali log è possibile integrare?
Azure produce registrazioni complete per ogni servizio. I log sono classificati nel modo seguente:

* **I registri di controllo/gestione** fornire visibilità hello operazioni di gestione risorse di Azure CREATE, UPDATE e DELETE. Questi eventi di controllo piano vengono rilevati nel log attività Azure hello
* **I registri del pannello dati** fornire visibilità eventi hello generato quando si utilizza una risorsa di Azure. Un esempio è registro eventi di Windows hello, in cui è possibile ottenere informazioni sugli eventi di sicurezza dal canale di sicurezza del Visualizzatore eventi hello. Gli eventi del piano dati (che vengono generati da una macchina virtuale o un servizio di Azure) vengono replicati dal log di diagnostica di Azure.

Integrazione di log di Azure supporta attualmente l'integrazione di hello di:

* Log delle macchine virtuali di Azure
* Log di controllo di Azure
* Avvisi del Centro sicurezza di Azure

## <a name="install-azure-log-integration"></a>Installare l'integrazione dei log di Azure
Scaricare l' [integrazione dei log di Azure](https://www.microsoft.com/download/details.aspx?id=53324).

il servizio di integrazione di log di Azure Hello raccoglie dati di telemetria dalla macchina di hello in cui è installato.  I dati di telemetria raccolti sono:

* Eccezioni che si verificano durante l'esecuzione dell'integrazione dei log di Azure
* Metriche relative al numero di hello di query e gli eventi elaborati
* Statistiche sulle opzioni della riga di comando Azlog.exe che vengono usate

> [!NOTE]
> Per disabilitare la raccolta dei dati di telemetria è possibile deselezionare questa opzione.
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>Integrare i log di controllo di Azure e gli avvisi del Centro sicurezza di Azure
1. Prompt dei comandi aprire hello e **cd** in **c:\Program Files\Microsoft Azure Log integrazione**.
2. Eseguire hello **azlog createazureid** comando toocreate un [entità servizio di Azure Active Directory](../active-directory/active-directory-application-objects.md) in Azure Active Directory (AD) hello tenant che ospitano hello le sottoscrizioni di Azure.

    Verrà richiesto l'account di accesso di Azure.

   > [!NOTE]
   > È necessario essere sottoscrizione hello proprietario o un coamministratore della sottoscrizione hello.
   >
   >

    TooAzure l'autenticazione viene eseguita mediante Azure AD.  Creazione di un'entità servizio per l'integrazione di log di Azure crea identità di Azure AD hello che viene fornito accesso tooread dalle sottoscrizioni di Azure.
3. Eseguire hello **azlog autorizzare <SubscriptionID>**  comando tooassign dell'accesso in lettura per un'entità servizio toohello sottoscrizione hello creata nel passaggio 2. Se non si specifica un **SubscriptionID**, entità servizio hello è assegnato hello lettore ruolo tooall sottoscrizioni toowhich si ha accesso.

   > [!NOTE]
   > Si potrebbero visualizzare avvisi se si esegue hello **autorizzare** comando immediatamente dopo hello **createazureid** comando. Si verifica della latenza tra la creazione di account di Azure AD hello e quando account hello disponibili per l'utilizzo. Attendere circa 10 secondi dopo l'esecuzione di hello **createazureid** comando toorun hello **autorizzare** comando, quindi questi avvisi non verrà visualizzato.
   >
   >
4. Verificare quali sono le seguenti cartelle tooconfirm che i file di registro JSON hello hello:

   * **c:\Users\azlog\AzureResourceManagerJson**
   * **c:\Users\azlog\AzureResourceManagerJsonLD**
5. Controllare hello tooconfirm cartelle presenti in essi contenuti gli avvisi del centro di sicurezza seguenti:

   * **c:\Users\azlog\ AzureSecurityCenterJson**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD**
6. Configurare hello SIEM file server di inoltro connettore toohello cartella. procedura Hello sarà diverso in base hello SIEM in uso.

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sui log attività di Azure e le definizioni di proprietà, vedere:

* [Operazioni di controllo con Gestione risorse](../azure-resource-manager/resource-group-audit.md)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) , ottenere informazioni e notizie sicurezza di Azure hello.
