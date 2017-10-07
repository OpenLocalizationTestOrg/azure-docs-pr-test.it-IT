---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - determinare i requisiti di sincronizzazione della directory | Documenti Microsoft"
description: Identificare i requisiti necessari per la sincronizzazione di tutti gli utenti di hello tra = in locale e nel cloud per enterprise hello.
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a>Determinare i requisiti di sincronizzazione delle directory
La sincronizzazione è fornire agli utenti un'identità nel cloud hello basata sull'identità locale. Che useranno sincronizzata conto per l'autenticazione o l'autenticazione federata, o meno agli utenti di hello è comunque necessario toohave un'identità nel cloud hello.  Questa identità sarà necessario toobe mantenute e aggiornate periodicamente.  gli aggiornamenti di Hello possono assumere forme diverse, dal titolo modifiche toopassword cambia.  

Avviare la valutazione hello organizzazioni identità utente e soluzione requisiti locale. Questa valutazione è requisiti tecnici di hello toodefine importanti per la modalità di creazione e gestite nel cloud hello identità utente.  Per la maggior parte delle organizzazioni, Active Directory locale e verranno sincronizzati da, tuttavia in alcuni casi non sarà case hello directory locale hello che per gli utenti.  

Verificare che hello tooanswer seguenti domande:

* Sono presenti una o più foreste di Active Directory?
  
  * Con quante directory di Azure Active Directory viene eseguita la sincronizzazione?
    
    1. Sono attivi dei filtri?
    2. Sono stati pianificati più server Azure AD Connect?
* È presente uno strumento di sincronizzazione locale?
  
  * In caso affermativo, gli utenti dispongono di una directory virtuale/integrazione delle identità?
* Si dispone di qualsiasi altra directory locale che si desidera toosynchronize (ad esempio Directory LDAP, database delle risorse Umane e così via)?
  * Verranno toobe esegue qualsiasi GALSync?
  * Che cos'è lo stato corrente hello dell'UPN dell'organizzazione? 
  * È presente una directory diversa per l'autenticazione degli utenti?
  * Si usa Microsoft Exchange in azienda?
    * Si prevede di eseguire una distribuzione ibrida di Exchange?

Dopo aver creato un'idea sui requisiti di sincronizzazione, è necessario toodetermine dello strumento è una toomeet corretta hello questi requisiti.  Microsoft offre diversi integrazione directory tooaccomplish di strumenti e la sincronizzazione.  Vedere hello [tabella di confronto di strumenti di gestione identità ibride directory integration](active-directory-hybrid-identity-design-considerations-tools-comparison.md) per ulteriori informazioni. 

Dopo aver creato i requisiti di sincronizzazione e strumento hello effettuare tale operazione per l'azienda, è necessario tooevaluate hello delle applicazioni che utilizzano questi servizi di directory. Questa valutazione è importante toodefine hello requisiti tecnici toointegrate questi cloud toohello applicazioni. Verificare che hello tooanswer seguenti domande:

* Queste applicazioni sarà spostato toohello cloud e utilizzare directory hello?
* Sono presenti attributi speciali che devono sincronizzare toobe toohello cloud queste applicazioni possono utilizzarli correttamente?
* Queste applicazioni è necessario toobe riscritto tootake sfruttare autenticazione cloud?
* Queste applicazioni continuerà toolive locale mentre gli utenti accedere utilizzando l'identità cloud hello?

È inoltre necessario toodetermine hello sicurezza requisiti e vincoli di sincronizzazione della directory. Questa valutazione è importante tooget un elenco di requisiti hello che sarà necessaria nell'ordine toocreate e gestire le identità dell'utente nel cloud hello. Verificare che hello tooanswer seguenti domande:

* In cui verranno collocati i server di sincronizzazione hello?
* Verrà aggiunto al dominio?
* Server hello si troverà in una rete con restrizioni dietro un firewall, ad esempio una rete Perimetrale?
  * Sarà la sincronizzazione toosupport tooopen in grado di hello necessario firewall porte?
* Si dispone di un piano di ripristino di emergenza per il server di sincronizzazione hello?
* Si dispone di un account con autorizzazioni appropriate di hello per tutte le foreste che si desidera toosynch con?
  * Se l'azienda non conosce risposte hello per questa domanda, nella sezione hello "Autorizzazioni per la sincronizzazione password" nell'articolo hello [hello installazione servizio di sincronizzazione di Azure Active Directory](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) e determinare se esiste già un account con queste autorizzazioni o se è necessario toocreate uno.
* Se dispone di sincronizzazione di più foreste è foresta tooeach tooget in grado di hello sincronizzazione server?

> [!NOTE]
> Annotare i tootake che ogni risposta e comprendere motivazioni hello delle risposte hello. [Determinare i requisiti di risposta agli eventi imprevisti](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) esaminerà le opzioni di hello disponibili. Una volta fornite le risposte a queste domande, sarà possibile selezionare l'opzione più adatta in base alle esigenze aziendali.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
[Determinare i requisiti dell'autenticazione a più fattori](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)

