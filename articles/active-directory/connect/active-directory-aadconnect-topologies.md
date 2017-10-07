---
title: 'Azure AD Connect: topologie supportate | Microsoft Docs'
description: Questo argomento illustra in modo dettagliato le topologie supportate e non supportate per Azure AD Connect
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Topologie per Azure AD Connect
Questo articolo descrive vari locale e le topologie di Azure Active Directory (Azure AD) di utilizzano la sincronizzazione di Azure AD Connect come soluzione di integrazione principali hello. Questo articolo include le configurazioni supportate e non supportate.

Di seguito è riportata la legenda hello per le immagini nell'articolo hello:

| Descrizione | Simbolo |
| --- | --- |
| Foresta locale di Active Directory |![Foresta locale di Active Directory](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| Active Directory locale con importazione con filtri |![Active Directory con importazione con filtri](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Server di sincronizzazione di Azure AD Connect |![Server di sincronizzazione di Azure AD Connect](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| Server di sincronizzazione di Azure AD Connect in "modalità di staging" |![Server di sincronizzazione di Azure AD Connect in "modalità di staging"](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| GALSync con Forefront Identity Manager (FIM) 2010 o Microsoft Identity Manager (MIM) 2016 |![GALSync con FIM 2010 o MIM 2016](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Dettagli relativi al server di sincronizzazione di Azure AD Connect |![Dettagli relativi al server di sincronizzazione di Azure AD Connect](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| Azure AD |![Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| Scenario non supportato |![Scenario non supportato](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>Foresta singola, tenant singolo di Azure AD
![Topologia per una foresta singola e un tenant singolo](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

topologia più comune di Hello è una singola locale foresta, con uno o più domini e un annuncio di Azure singolo tenant. Per l'autenticazione di Azure AD viene usata la sincronizzazione delle password. installazione rapida di Hello di Azure AD Connect supporta solo questa topologia.

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>Singola foresta, più tenant di Azure AD tooone server sincronizzazione
![Topologia con filtri non supportata per una foresta singola](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

Presenza di più server di sincronizzazione di Azure AD Connect tenant connesso toohello stesso Azure Active Directory non è supportato, ad eccezione di un [server di gestione temporanea](#staging-server). Non è supportato anche se questi server sono toosynchronize configurato con un set di oggetti si escludono a vicenda. Si potrebbe essere stato preso in considerazione questa topologia se non è possibile raggiungere tutti i domini nella foresta hello da un singolo server o se si desidera toodistribute carico tra più server.

## <a name="multiple-forests-single-azure-ad-tenant"></a>Più foreste, tenant singolo di Azure AD
![Topologia per più foreste e un tenant singolo](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

In molte organizzazioni sono presenti ambienti con più foreste Active Directory locali. La presenza di più foreste Active Directory locali può essere dovuta a vari motivi. Esempi tipici sono incluse le progettazioni con account-risorse foreste e hello il risultato di una fusione o acquisizione.

Quando sono presenti più foreste, devono essere tutte raggiungibili da un singolo server di sincronizzazione di Azure AD Connect. Non si dispone di dominio di tooa toojoin hello server. Se necessario tooreach tutte le foreste, è possibile collocare il server di hello in una rete perimetrale (anche noto come DMZ, DMZ e subnet schermata).

installazione guidata di Hello Azure AD Connect offre diverse opzioni tooconsolidate gli utenti sono rappresentati in più foreste. obiettivo di Hello è rappresentato solo una volta che un utente in Azure AD. Esistono alcune topologie comuni che è possibile configurare nel percorso di installazione personalizzata hello nell'installazione guidata di hello. In hello **identificazione univoca degli utenti** pagina, l'opzione corrispondente selezionare hello che rappresenta la topologia. consolidamento di Hello è configurato solo per gli utenti. Gruppi duplicati non sono consolidati con la configurazione predefinita di hello.

Le topologie comuni sono descritti nelle sezioni hello su [topologie separate](#multiple-forests-separate-topologies), [completo mesh](#multiple-forests-full-mesh-with-optional-galsync), e [hello topologia account-risorse](#multiple-forests-account-resource-forest).

configurazione predefinita di Hello in Azure AD Connect sync presuppone:

* Ogni utente dispone di un solo account abilitato e foresta hello in cui si trova l'account è utente di hello tooauthenticate utilizzato. Questo presupposto riguarda sia la sincronizzazione delle password che la federazione. userPrincipalName e sourceAnchor o immutableID provengono da questa foresta.
* Ogni utente ha solo una cassetta postale.
* foresta Hello che ospita la cassetta postale hello per un utente ha hello migliore qualità dei dati per gli attributi visibili in hello Exchange elenco (globale). Se è presente alcuna cassetta postale dell'utente di hello, qualsiasi foresta può essere utilizzato toocontribute questi valori dell'attributo.
* Se è disponibile una cassetta postale collegata, è presente anche un account in una foresta diversa usato per l'accesso.

Se l'ambiente non corrisponde a questi presupposti, hello eseguite le operazioni seguenti:

* Se si dispone di più di un account attivo o più di una cassetta postale, il motore di sincronizzazione hello sceglie una e Ignora hello altri.
* Una cassetta postale collegata con nessun altro account attivo non è esportato tooAzure Active Directory. account utente di Hello non è rappresentata come un membro in qualsiasi gruppo. Una cassetta postale collegata in DirSync viene sempre rappresentata come cassetta postale normale. Questa modifica è intenzionalmente un scenari più insiemi di strutture di supporto toobetter un comportamento diverso.

È possibile trovare altre informazioni, vedere [informazioni su configurazione predefinita di hello](active-directory-aadconnectsync-understanding-default-configuration.md).

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>Più foreste, più tenant di Azure AD tooone server sincronizzazione
![Topologia non supportata per più foreste e più server di sincronizzazione](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

Non è possibile avere più tooa server connesso sincronizzazione di Azure AD Connect single-tenant di Azure AD. eccezione Hello è hello utilizzo di un [server di gestione temporanea](#staging-server).

### <a name="multiple-forests-separate-topologies"></a>Più foreste, topologie separate
![Opzione per rappresentare gli utenti solo una volta in tutte le directory](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![Immagine di più foreste e topologie separate](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

In questo ambiente tutte le foreste locali vengono considerate entità separate. Nessun utente è presente in nessuna altra foresta. Ogni foresta dispone di un'organizzazione Exchange dedicata e non c'è nessun GALSync tra foreste hello. Questa topologia potrebbe essere una situazione di hello dopo una fusione/acquisizione o in un'organizzazione in cui ogni business unit opera in modo indipendente. Questi insiemi sono nella stessa organizzazione di Azure AD hello e vengono visualizzati con un elenco indirizzi globale unificato. In hello immagine precedente, ogni oggetto in ogni foresta è rappresentata una volta nel metaverse hello e aggregato nel tenant di Azure AD di destinazione hello.

### <a name="multiple-forests-match-users"></a>Più foreste: corrispondenze con utenti
Tooall comuni questi scenari è la distribuzione e gruppi di sicurezza possono contenere una combinazione di utenti, contatti e le entità di sicurezza esterne (FSP). FSP vengono utilizzati nei membri di servizi di dominio Active Directory (AD DS) toorepresent di altre foreste in un gruppo di sicurezza. FSP tutti sono oggetti reali toohello risolto in Azure AD.

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>Più foreste: a maglia completa con GALSync facoltativo
![Opzione per l'utilizzo di attributo mail hello per la corrispondenza quando le identità utente presenti in più directory](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![Topologia a maglia completa per più foreste](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

Una topologia a maglia completa consente agli utenti e risorse toobe che si trova in ogni foresta. In genere, sono presenti relazioni di trust bidirezionale tra foreste hello.

Se Exchange è presente in più di una foresta, potrebbe essere disponibile (facoltativamente) una soluzione GALSync locale. Ogni utente viene quindi rappresentato come un contatto in tutte le altre foreste. GALSync viene in genere implementato tramite FIM 2010 o MIM 2016. Azure AD Connect non può essere usato per la soluzione GALSync locale.

In questo scenario, gli oggetti identità vengono uniti tramite l'attributo mail hello. Un utente che ha una cassetta postale in un insieme di strutture è unita in join con i contatti hello in hello altre foreste.

### <a name="multiple-forests-account-resource-forest"></a>Più foreste, foresta di tipo account-risorse
![Opzione per l'utilizzo degli attributi ObjectSID e msExchMasterAccountSID hello per la corrispondenza quando le identità sono presenti in più directory](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![Topologia di foresta di tipo account-risorse per più foreste](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

In una topologia di foresta account-risorse sono presenti una o più foreste *account* con account utente attivi. Sono anche presenti una o più foreste *risorse* con account disabilitati.

In questo scenario una o più foreste risorse considerano attendibili tutte le foreste account. foresta delle risorse Hello include in genere uno schema di Active Directory esteso con Exchange e Lync. Tutti i servizi Exchange e Lync, con altri servizi condivisi, si trovano in questa foresta. Gli utenti dispongono di un account utente disabilitato nella foresta ed è collegata la cassetta postale hello toohello foresta degli account.

## <a name="office-365-and-topology-considerations"></a>Considerazioni su Office 365 e sulle topologie
Alcuni carichi di lavoro di Office 365 prevedono determinate restrizioni per le topologie supportate:

| Carico di lavoro | Restrizioni |
--------- | ---------
| Exchange Online | Se è presente più di un'organizzazione di Exchange locale (ovvero, Exchange è stato distribuito toomore rispetto a un insieme di strutture), è necessario utilizzare Exchange 2013 SP1 o versione successiva. Per altre informazioni, vedere [Distribuzioni ibride con più foreste di Active Directory](https://technet.microsoft.com/library/jj873754.aspx). |
| Skype for Business Online | Quando si utilizzano più insiemi di strutture locale, l'unica topologia di foresta account-risorse hello è supportata. Per altre informazioni, vedere [Requisiti ambientali di Skype for Business Server 2015](https://technet.microsoft.com/library/dn933910.aspx). |


## <a name="staging-server"></a>server di gestione temporanea
![Server di staging in una topologia](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

Azure AD Connect supporta l'installazione di un secondo server in *modalità di staging*. Un server in questa modalità legge i dati da tutte le directory connesse, ma non possono scrivere tooconnected directory. Utilizza il ciclo di sincronizzazione normale hello e pertanto dispone di una copia aggiornata dei dati di identità hello.

In caso di emergenza in cui il server primario di hello ha esito negativo, è possibile eseguire il failover toohello server di gestione temporanea. A tale scopo nella procedura guidata di Azure AD Connect hello. Il secondo server può trovarsi in un altro Data Center perché un'infrastruttura non è condiviso con il server primario hello. È necessario copiare manualmente qualsiasi modifica alla configurazione apportata sul server secondo toohello di hello server primario.

È possibile utilizzare un tootest server di gestione temporanea un effetto personalizzato nuova di hello e configurazione per i dati. È possibile visualizzare in anteprima le modifiche di hello e modificare la configurazione hello. Quando si è soddisfatti nuova configurazione hello, è possibile rendere hello server attivo hello di server di gestione temporanea e impostare la modalità precedente active server toostaging hello.

È anche possibile utilizzare questo server di sincronizzazione di active hello tooreplace (metodo). Preparare hello nuovo server e impostarlo toostaging modalità. Assicurarsi che sia in buono stato, disabilita (rendere attivo), la modalità di gestione temporanea e arrestare hello server attualmente attivo.

È possibile toohave più di un server di gestione temporanea quando si desidera toohave più copie di backup in diversi Data Center.

## <a name="multiple-azure-ad-tenants"></a>Più tenant di Azure AD
È consigliabile che in Azure AD sia presente un tenant singolo per un'organizzazione.
Prima di pianificare toouse più tenant di Azure Active Directory, vedere l'articolo hello [gestire unità amministrative in Azure AD](../active-directory-administrative-units-management.md). che illustra gli scenari comuni in cui è possibile usare un singolo tenant.

![Topologia per più foreste e più tenant](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Esiste una relazione 1:1 tra un server di sincronizzazione di Azure AD Connect e un tenant di Azure AD. Per ogni tenant di Azure AD è necessaria un'installazione del server del servizio di sincronizzazione Azure AD Connect. istanze di tenant di Azure AD Hello vengono isolate in base alla progettazione. Ovvero gli utenti in un unico tenant non è possibile visualizzare gli utenti in hello altri tenant. Se la separazione è necessaria, questa è una configurazione supportata. In caso contrario, è consigliabile utilizzare hello singolo modello di tenant di Azure AD.

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>Ogni oggetto una sola volta in un tenant di Azure AD
![Topologia con filtri per una foresta singola](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

In questa topologia, un server di sincronizzazione di Azure AD Connect è tenant tooeach connesso AD Azure. server di sincronizzazione di Azure AD Connect Hello deve essere configurato per il filtro in modo che ognuno disponga di un set di oggetti toooperate si escludono a vicenda. È possibile, ad esempio, definire ambito ogni dominio particolare tooa del server o unità organizzativa.

Un dominio DNS può essere registrato unicamente in un tenant singolo di Azure AD. Hello UPN degli utenti hello nell'istanza di Active Directory locale hello è inoltre necessario utilizzare spazi dei nomi distinti. Ad esempio, in hello precedente immagine, tre suffissi UPN separati vengono registrati nell'istanza di Active Directory locale hello: wingtiptoys.com contoso.com e fabrikam.com. gli utenti di Hello in ogni dominio di Active Directory locale usare uno spazio dei nomi diversi.

Non sussiste alcun GALSync tra istanze di tenant di Azure AD hello. Hello Rubrica in Exchange Online e Skype per presentazioni Business solo gli utenti di hello stesso tenant.

Questa topologia presenta i seguenti hello in caso contrario restrizioni sugli scenari supportati:

* Solo uno dei tenant hello Azure AD è possibile abilitare un ibrida di Exchange con l'istanza di Active Directory locale hello.
* I dispositivi Windows 10 possono essere associati a un solo tenant di Azure AD.
* Hello singola opzione sign-on (SSO) per l'autenticazione pass-through e sincronizzazione password è utilizzabile con un solo tenant di Azure AD.

requisito di Hello per un set di oggetti si escludono a vicenda si applica anche toowriteback. Alcune funzionalità di writeback non sono supportate con questa topologia, perché presuppongono una singola configurazione locale. Queste funzionalità includono:

* Writeback dei gruppi con la configurazione predefinita.
* Writeback dispositivi.

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>Ogni oggetto più volte in un tenant di Azure AD
![Topologia non supportata per una foresta singola e più tenant](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![Topologia non supportata per una foresta singola e più connettori](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

Queste attività non sono supportate:

* Sincronizzazione hello stesso tenant di Azure AD toomultiple utente.
* Modifica della configurazione per fare in modo che gli utenti di un tenant di Azure AD vengano visualizzati come contatti in un altro tenant di Azure AD.
* Modificare i tenant di Azure AD Connect sincronizzazione tooconnect toomultiple Azure AD.

### <a name="galsync-by-using-writeback"></a>GALSync tramite l'uso di writeback
![Topologia non supportata per più foreste e più directory, con GALSync incentrato su Azure AD](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![Topologia non supportata per più foreste e più directory, con GALSync incentrato su Active Directory locale](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

I tenant di Azure AD sono isolati per impostazione predefinita. Queste attività non sono supportate:

* Modificare la configurazione di hello Azure AD Connect dati di sincronizzazione tooread da un altro tenant di Azure AD.
* Esportare gli utenti come istanza di Active Directory locale tooanother contatti con sincronizzazione di Azure AD Connect.

### <a name="galsync-with-on-premises-sync-server"></a>GALSync con server di sincronizzazione locale
![GALSync in una topologia per più foreste e più directory](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

È possibile utilizzare 2010 FIM o MIM 2016 toosync utenti locali (tramite GALSync) tra due organizzazioni di Exchange. gli utenti di Hello in un'organizzazione vengono visualizzati come utenti o contatti esterni in hello un'altra organizzazione. Sarà quindi possibile sincronizzare le due istanze locali diverse di Active Directory con i rispettivi tenant di Azure AD.

## <a name="next-steps"></a>Passaggi successivi
toolearn tooinstall Azure AD Connect per questi scenari, vedere [installazione personalizzata di Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.

Altre informazioni sull'[integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
