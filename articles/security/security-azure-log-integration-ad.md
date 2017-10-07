---
title: Integrazione di Log con i log di controllo di Azure Active Directory aaaAzure | Documenti Microsoft
description: Informazioni su come tooinstall hello servizio di integrazione di Log di Azure e integrare i registri dai log di controllo di Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Integrare i log di controllo di Azure Active Directory

Gli eventi di controllo di Azure Active Directory (Azure AD) aiutano i clienti a identificare le azioni con privilegi che si sono verificate in Azure Active Directory. È possibile visualizzare hello tipi di eventi che è possibile tenere traccia, è consigliabile consultare [eventi di report di controllo di Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).

> [!NOTE]
> Prima di eseguire i passaggi di hello in questo articolo, è necessario esaminare hello [iniziare](security-azure-log-integration-get-started.md) articolo e completare i passaggi hello.

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>Procedura toointegrate Azure Active directory log di controllo

1. Aprire il prompt dei comandi di hello ed eseguire questo comando:

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. Eseguire questo comando: 
 
   ``azlog createazureid``

   Questo comando richiede le credenziali di accesso di Azure. Hello comando crea quindi una Azure Active Directory principale del servizio nel tenant di Azure AD hello che ospitano hello le sottoscrizioni di Azure in cui hello utente connesso è un amministratore, coamministratore o un proprietario. comando Hello avrà esito negativo se l'utente connesso di hello è solo un utente guest nel tenant di Azure AD hello. TooAzure l'autenticazione viene eseguita mediante Azure AD. Creazione di un'entità servizio per l'integrazione di Log di Azure crea hello identità di Azure AD che ha accesso tooread dalle sottoscrizioni di Azure.

3. Comando che segue hello esecuzione tooprovide l'ID del tenant. È necessario membro toobe del comando di hello tenant admin ruolo toorun hello.

   ``Azlog.exe authorizedirectoryreader tenantId``

   Esempio:

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. Controllare hello seguente tooconfirm cartelle che hello Azure Active Directory i JSON file di registro viene creato in essi contenuti:

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

Hello video seguente illustra i passaggi di hello illustrati in questo articolo:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> Per istruzioni dettagliate su come rendere le informazioni di hello nei file JSON hello le informazioni di sicurezza e un sistema (SIEM) di gestione degli eventi, contattare il fornitore SIEM.

Assistenza della community è disponibile tramite hello [Forum MSDN di Azure Log integrazione](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Questo forum consente agli utenti in hello Azure Log integrazione community toosupport reciprocamente con domande, le risposte, suggerimenti e consigli. Inoltre, il team di integrazione di Azure Log hello questo forum consente di monitorare e aiuta ogni volta che è possibile.

Si può anche aprire un [richiesta di supporto](../azure-supportability/how-to-create-azure-support-request.md). Selezionare **Log integrazione** come servizio hello per il quale si richiede supporto.

## <a name="next-steps"></a>Passaggi successivi
toolearn più informazioni sull'integrazione di Log di Azure, vedere:

* [Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) (Integrazione log di Microsoft Azure): pagina di Area download con informazioni dettagliate, requisiti di sistema e istruzioni di installazione per l'integrazione dei log di Azure.
* [Introduzione tooAzure Log integrazione](security-azure-log-integration-overview.md): questo articolo illustra tooAzure integrazione di Log, le funzionalità chiave e il funzionamento.
* [Passaggi di configurazione di partner](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): questo post di blog viene illustrato come tooconfigure toowork di integrazione di Log di Azure con soluzioni Splunk, HP ArcSight e IBM QRadar di partner.
* [Domande frequenti sull'integrazione dei log di Azure](security-azure-log-integration-faq.md): questo articolo contiene le risponde alle domande sull'integrazione dei log di Azure.
* [Gli avvisi del Centro sicurezza di integrazione con l'integrazione di Azure Log](../security-center/security-center-integrating-alerts-with-log-integration.md): questo articolo illustra come centro di sicurezza toosync avvisi, insieme agli eventi di sicurezza di macchina virtuale raccolti da diagnostica di Azure e i log di controllo di Azure, con analitica il log o Soluzione SIEM.
* [Registri di verifica delle nuove funzionalità per la diagnostica di Azure e Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): questo post di blog introduce i log di controllo tooAzure e altre funzionalità che consentono di ottenere informazioni approfondite operazioni hello delle risorse di Azure.
