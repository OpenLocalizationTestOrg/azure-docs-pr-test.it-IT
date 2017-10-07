---
title: integrazione di Log con il Centro sicurezza PC aaaAzure | Documenti Microsoft
description: Informazioni su come tooget sicurezza di Azure center gli avvisi di utilizzo con l'integrazione di Log
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
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>Come tooget avvisi del Centro sicurezza PC nell'integrazione di log di Azure
Questo articolo fornisce hello passaggi necessari tooenable hello Azure Log Integrazione servizio toopull informazioni sugli avvisi di sicurezza generati dal Centro sicurezza di Azure. È necessario che sia completata passaggi hello hello [iniziare](security-azure-log-integration-get-started.md) articolo prima di eseguire i passaggi di hello in questo articolo.

## <a name="detailed-steps"></a>Procedura dettagliata
Hello segue creerà hello necessari entità servizio di Azure Active Directory e autorizzazioni di lettura assegnare hello servizio principio toohello sottoscrizione:
1. Aprire il prompt dei comandi di hello e passare troppo**c:\Program Files\Microsoft Azure Log integrazione**
2. Eseguire il comando hello``azlog createazureid``

    Questo comando richiede le credenziali di accesso di Azure. comando Hello crea quindi un [entità servizio di Azure Active Directory](../active-directory/develop/active-directory-application-objects.md) in hello tenant di Azure AD che ospitano hello le sottoscrizioni di Azure in cui hello utente connesso è un amministratore, coamministratore o un proprietario. comando Hello avrà esito negativo se hello utente connesso è solo un utente Guest hello Tenant di Azure AD. TooAzure l'autenticazione viene eseguita tramite Azure Active Directory (AD). Creazione di un'entità servizio per l'integrazione Azlog crea hello identità di Azure AD che avrà accesso tooread dalle sottoscrizioni di Azure.

2. Successivamente verrà eseguito un comando che assegna l'accesso in lettura per un'entità servizio toohello sottoscrizione hello creata nel passaggio 2. Se non si specifica un ID sottoscrizione, il comando hello tenterà tooassign hello servizio principale lettore ruolo tooall sottoscrizioni toowhich si dispone di accesso. </br></br>
``azlog authorize <SubscriptionID>`` </br> ad esempio </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    Si potrebbero visualizzare avvisi se si esegue hello autorizzare comando immediatamente dopo il comando di createazureid hello. Si verifica della latenza tra la creazione di account di Azure AD hello e quando account hello disponibili per l'utilizzo. Se attendere circa 60 secondi dopo l'esecuzione comando toorun hello di hello createazureid autorizzare comando, quindi questi avvisi non verrà visualizzato.

4. Verificare quali sono le seguenti cartelle tooconfirm che i file di registro JSON hello hello:
 * **c:\Users\azlog\AzureResourceManagerJson**
 * **c:\Users\azlog\AzureResourceManagerJsonLD** </br></br>
5. Controllare hello tooconfirm cartelle presenti in essi contenuti gli avvisi del centro di sicurezza seguenti:</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD** </br></br>

Se si verificano problemi durante l'installazione di hello e configurazione, aprire un [richiesta di supporto](/azure-supportability/how-to-create-azure-support-request.md)selezionare **Log integrazione** come servizio hello per il quale si richiede supporto.

## <a name="next-steps"></a>Passaggi successivi
toolearn più informazioni sull'integrazione di Log di Azure, vedere hello seguenti documenti:

* [Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) (Integrazione log di Microsoft Azure) - Area download per informazioni dettagliate, requisiti di sistema e istruzioni di installazione per l'integrazione dei log di Azure.
* [Integrazione di log di introduzione tooAzure](security-azure-log-integration-overview.md) : questo documento introduce tooAzure integrazione di log, le funzionalità chiave e il funzionamento.
* [Passaggi di configurazione di partner](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – questo post di blog viene illustrato come tooconfigure Azure log toowork integrazione con soluzioni di partner Splunk e ArcSight HP, IBM QRadar.
* [Domande frequenti sull'integrazione dei log di Azure](security-azure-log-integration-faq.md) - Queste domande frequenti riguardano l'integrazione dei log di Azure.
* [L'integrazione di Centro sicurezza PC avvisi con Azure log integrazione](../security-center/security-center-integrating-alerts-with-log-integration.md) : questo documento viene illustrato come centro di sicurezza toosync avvisi, insieme agli eventi di sicurezza di macchina virtuale raccolti da diagnostica di Azure e i log di controllo di Azure con analitica il log o Soluzione SIEM.
* [Nuove funzionalità di diagnostica di Azure e i log di controllo di Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) : questo post di blog introduce i log di controllo tooAzure e altre funzionalità che consentono di ottenere informazioni approfondite operazioni hello delle risorse di Azure.
