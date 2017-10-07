---
title: problemi relativi alle licenze aaaResolve per un gruppo in Azure Active Directory | Documenti Microsoft
description: Come tooidentify e risolvere i problemi di assegnazione licenze quando si usa Azure Active Directory in base al gruppo di licenze
services: active-directory
keywords: Licenze di Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Identificare e risolvere i problemi relativi alle licenze per un gruppo in Azure Active Directory

In base al gruppo di licenze in Azure Active Directory (Azure AD) è stato introdotto il concetto di hello degli utenti in uno stato di errore di licenza. In questo articolo è illustrare i motivi di hello perché gli utenti potrebbero in questo stato.

Quando si assegna le licenze direttamente tooindividual utenti, senza utilizzare licenze basate su gruppo, l'operazione di assegnazione hello potrebbe non riuscire. Ad esempio, quando si esegue il cmdlet PowerShell di hello `Set-MsolUserLicense` su un utente, i cmdlet di hello può non riuscire per diversi motivi per cui sono correlati toobusiness logica. Ad esempio, potrebbe esserci un numero insufficiente di licenze o di un conflitto tra due piani di servizio non può essere assegnato a hello stesso tempo. Hello problema viene comunicato tooyou di eseguire il backup.

Quando si utilizza in base al gruppo di licenza, hello stessi errori possono verificarsi, ma vengono eseguite in background hello quando hello servizio Azure AD è l'assegnazione delle licenze. Per questo motivo, gli errori di hello non possono essere comunicata tooyou immediatamente. In alternativa, è registrati nell'oggetto utente hello e quindi segnalati tramite portale amministrativo hello. Si noti che l'utente originale toolicense preventivo hello hello non viene mai perso, ma venga registrata in uno stato di errore per analisi future e la risoluzione.

## <a name="how-toofind-license-assignment-errors"></a>Come gli errori di assegnazione delle licenze toofind

1. utenti toofind nello stato un errore in un gruppo specifico, pannello hello open per il gruppo di hello. In **Licenze** verrà visualizzata una notifica se sono presenti utenti con stato di errore.

![Gruppo, notifica di errore](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Fare clic su hello notifica tooopen un elenco di tutti gli utenti interessati. È possibile fare clic su ogni utente singolarmente toosee ulteriori informazioni, vedere.

![Gruppo, elenco degli utenti in stato di errore](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. toofind tutti i gruppi che contengono almeno un errore, in hello **Azure Active Directory** pannello selezionare **licenze** e quindi **Panoramica**. Se alcuni gruppi richiedono attenzione, viene visualizzata una casella di informazioni.

![Panoramica, informazioni sui gruppi in stato di errore](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Fare clic su hello casella toosee un elenco di tutti i gruppi con errori. È possibile fare clic su ogni gruppo per visualizzare altri dettagli.

![Panoramica, elenco di gruppi con errori](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


Di seguito è riportata una descrizione di ogni potenziale tooresolve modo di problema e hello è.

## <a name="not-enough-licenses"></a>Le licenze non sono sufficienti

**Problema:** non è sufficiente licenze disponibili per uno dei prodotti hello specificato nel gruppo di hello. È necessario tooeither acquistare più licenze per prodotto hello o liberare le licenze inutilizzate da altri utenti o gruppi.

toosee quante licenze sono disponibili, andare troppo**Azure Active Directory** > **licenze** > **tutti i prodotti**.

toosee quali utenti e gruppi utilizzano licenze, fare clic su un prodotto. In **Utenti con licenza** verranno visualizzati tutti gli utenti a cui sono state assegnate licenze direttamente o tramite uno o più gruppi. In **Gruppi con licenza** verranno visualizzati tutti i gruppi a cui è assegnato tale prodotto.

**PowerShell:** i cmdlet di PowerShell segnalano questo errore come _CountViolation_.

## <a name="conflicting-service-plans"></a>Piani di servizio in conflitto

**Problema:** uno dei prodotti hello specificato nel gruppo hello contiene un piano di servizio è in conflitto con un altro piano di servizio che è già assegnato toohello utente tramite un prodotto diverso. Alcuni piani di servizio configurati in modo che non possono essere assegnate toohello dello stesso utente di un altro piano di servizio correlate.

Prendere in considerazione hello di esempio seguente. Un utente dispone di una licenza per Office 365 Enterprise **E1** assegnato direttamente, con tutti i piani di hello abilitati. utente Hello è stato aggiunto a un gruppo di tooa con Office 365 Enterprise hello **E3** tooit prodotto assegnato. Questo prodotto contiene piani di servizio che non si sovrappongono con i piani di hello inclusi in E1, per consentire l'assegnazione delle licenze gruppo hello avrà esito negativo con errore "I piani di servizio in conflitto" hello. In questo esempio, i piani di servizio in conflitto hello sono:

-   SharePoint Online (piano 2) in conflitto con SharePoint Online (piano 1).
-   Exchange Online (piano 2) in conflitto con Exchange Online (piano 1).

toosolve questo conflitto, è necessario toodisable tali due piani in hello E1 licenza che utente toohello direttamente assegnato. In alternativa, è necessario l'assegnazione delle licenze toomodify hello intero gruppo e disabilitare i piani di hello nella licenza E3 hello. In alternativa, è possibile decidere tooremove hello E1 licenza utente hello se è ridondante nel contesto di hello della licenza di hello E3.

decidere come prodotto in conflitto tooresolve licenze sempre Hello appartiene toohello amministratore. Azure AD non risolve automaticamente i conflitti di licenza.

**PowerShell:** i cmdlet di PowerShell segnalano questo errore come _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>Altri prodotti dipendono da questa licenza

**Problema:** uno dei prodotti hello specificato nel gruppo hello contiene un piano di servizio che deve essere abilitato per un altro piano di servizio, in un altro prodotto, alla funzione. Questo errore si verifica quando si tenta di Azure AD tooremove hello sottostante il piano di servizio. Ad esempio, ciò può verificarsi in seguito a utente hello verrà rimosso dal gruppo hello.

toosolve questo problema, è necessario che tale piano obbligatorio hello è ancora assegnato toousers tramite un altro metodo, o che i servizi dipendenti hello sono disabilitati per tali utenti toomake. Successivamente, è possibile rimuovere correttamente licenza gruppo hello per gli utenti.

**PowerShell:** i cmdlet di PowerShell segnalano questo errore come _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>La località di utilizzo non è consentita

**Problema:** alcuni servizi Microsoft non sono disponibili in tutte le località a causa di leggi e regolamenti locali. Prima di poter assegnare un utente tooa di licenza, si dispone di proprietà di "Località di utilizzo" hello toospecify per utente hello. È possibile farlo in hello **utente** > **profilo** > **impostazioni** sezione hello portale di Azure.

Quando Azure AD tenta tooassign un utente tooa licenza di gruppo non è supportato il cui percorso di utilizzo, avrà esito negativo e registra l'errore utente hello.

toosolve questo problema, rimuovere utenti da percorsi che dal gruppo hello concesso in licenza. In alternativa, se valori posizione di utilizzo correnti hello non rappresentano percorso effettivo dell'utente hello, è possibile modificarle in modo che hello assegnazione delle licenze correttamente successivo (se il nuovo percorso di hello è supportato).

**PowerShell:** i cmdlet di PowerShell segnalano questo errore come _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Quando Azure AD le assegna licenze di gruppo, tutti gli utenti senza specificata una località di utilizzo ereditano percorso hello della directory di hello. È consigliabile che gli amministratori di impostare utilizzo corretto di hello valori del percorso sugli utenti prima di utilizzare in base al gruppo di gestione delle licenze toocomply con normative e leggi locali.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>Cosa accade quando un gruppo include più di una licenza del prodotto

È possibile assegnare più di un gruppo di tooa di licenza del prodotto. Enterprise Mobility + Security tooa gruppo tooeasily abilitare inclusi i servizi per gli utenti, ad esempio, è possibile assegnare a Office 365 Enterprise E3.

Azure AD tenta tooassign tutte le licenze che sono specificate nel gruppo tooeach utente di hello. Se Azure AD non è possibile assegnare uno dei prodotti hello a causa di problemi di logica di business (ad esempio, se non ci siano disponibili licenze sufficienti per tutti, o se sono presenti conflitti con altri servizi che sono abilitati sull'utente hello), non assegna altre licenze nel gruppo hello hello entrambi.

Sarà hello toosee in grado di utenti che non è stato possibile tooget assegnato non è riusciti e controllare quali prodotti sono stati interessati dal problema.

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a>Assegnazione delle licenze non riesce senza avvisare per un utente a causa di indirizzi proxy tooduplicate in Exchange Online

Se si usa Exchange Online, alcuni utenti nel tenant possono essere configurate in modo non corretto con hello stesso valore dell'indirizzo proxy. Quando in base al gruppo di licenze tenta tooassign toosuch una licenza utente, avrà esito negativo e non verrà registrato un errore (a differenza di hello altri casi di errore descritti in precedenza) - si tratta di una limitazione nella versione di anteprima hello di questa funzionalità e verrà tooaddress prima  *Disponibilità generale*.

> [!TIP]
> Se si nota che alcuni utenti non hanno ricevuto una licenza e non ci sono errori registrati per tali utenti, per prima cosa controllare se hanno indirizzi proxy duplicati.
> Questa operazione può essere eseguita tramite l'esecuzione di hello seguente cmdlet di PowerShell con Exchange Online:
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [In questo articolo](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) contiene ulteriori dettagli su questo problema, incluse le informazioni su [come tooExchange tooconnect Online usando PowerShell remoto](https://technet.microsoft.com/library/jj984289.aspx).

Dopo aver problemi degli indirizzi proxy sono stati risolti per gli utenti interessato hello, rendere che tooforce licenza, l'elaborazione in hello gruppo toomake che ora è possibile applicare nuovamente le licenze.

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a>Come fare per imporre l'elaborazione degli errori tooresolve un gruppo di licenze?

A seconda procedura che è stato necessario tooresolve errori, potrebbe essere necessario toomanually l'elaborazione di trigger di uno stato di utente hello tooupdate gruppo.

Ad esempio, se liberato alcune licenze rimuovendo le assegnazioni delle licenze direttamente dagli utenti, è necessario tootrigger l'elaborazione di gruppi che in precedenza non è stato possibile licenza toofully tutti i membri utente. Aprire toodo che, trovare pannello gruppo hello **licenze**e seleziona hello **rielaborare** pulsante nella barra degli strumenti hello.

## <a name="next-steps"></a>Passaggi successivi

toolearn più informazioni sugli altri scenari per la gestione delle licenze tramite i gruppi, vedere l'esempio hello:

* [L'assegnazione gruppo di licenze tooa in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Che cosa sono le licenze basate sui gruppi in Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Come singoli toomigrate concesso in licenza agli utenti in base toogroup licenze in Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Scenari aggiuntivi relativi alle licenze basate sui gruppi in Azure Active Directory](active-directory-licensing-group-advanced.md)
