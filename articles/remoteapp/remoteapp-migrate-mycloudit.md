---
title: fatturazione hello aaaChange per Azure RemoteApp | Documenti Microsoft
description: Informazioni su come toostop fatturati per Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: fe3841a88978ec56829932621489e75d5dd7e673
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toomycloudit"></a>Eseguire la migrazione da tooMyCloudIT Azure RemoteApp 

**Si utilizza attualmente Microsoft Azure RemoteApp?** : MyCloudIT compilato un toomigrate strumento automatico della piattaforma di gestione di Azure RemoteApp (ARA) raccolte toohello MyCloudIT continuando toorun in Microsoft Azure.

**Sfruttare i vantaggi del portale di gestione risorse di Azure hello**: migrazione completata nella piattaforma MyCloudIT hello consente il nuovo portale di gestione risorse di Azure del tooAzure accesso immediato. Questo portale contiene tutte le funzionalità nuove hello e innovazioni offerti da Microsoft Azure, tra cui accesso tooVirtual macchina dimensioni tooensure la distribuzione viene compilata esigenze hello toosupport dell'azienda.

**Test nella soluzione hello tooensure paralleli per le proprie esigenze**: strumento di migrazione MyCloudIT hello incorporato tooinitiate processo di migrazione hello e test in parallelo mentre gli utenti ARA correnti continuano ARA toouse.  Gli utenti rimarranno in ARA fino al completamento della migrazione e dei test.  strumento di migrazione Hello viene compilato la raccolta toohandle hello tipico ARA.  Se si ritiene è uno scenario non standard, univoco, contattare Microsoft all'indirizzo [ sales@conexlink.com ](mailto:sales@conexlink.com) , pertanto è possibile fornire tooassist un piano personalizzato con la migrazione.

**La funzionalità desktop-as-a-Service**: tenere presente che MyCloudIT offre non solo si è abituati a funzionalità di hello RemoteApp, ma completa Desktop-As-A-Service offre funzionalità per hello stesso costo al mese senza che nessun utente minima requisiti.

## <a name="what-we-will-do-for-you"></a>Quali operazioni vengono eseguite

MyCloudIT automatizzare la migrazione di hello del modello di RemoteApp di Azure dal portale di Azure classico hello del portale di gestione risorse di Azure della sottoscrizione con lo strumento di migrazione automatica di toohello di sottoscrizione.  

> [!NOTE]
> Hello Azure RemoteApp che deve rimanere nel modello hello stessa regione di Azure come la distribuzione di Azure RemoteApp originale.  Se è necessario toochange aree di Azure o sottoscrizioni di Azure durante la migrazione di hello, contattare Microsoft per informazioni aggiuntive in [ sales@conexlink.com ](mailto:sales@conexlink.com).

Leggere di seguito per informazioni dettagliate su hello automatizzata il processo di migrazione con lo strumento di migrazione MyCloudIT hello:

1. strumento di migrazione Hello analizza proprie sottoscrizioni corrente per tutte le distribuzioni di sistema esistente.  
2. Selezionare un'ARA raccolta toomigrate alla volta.  Se si dispone di più raccolte, eseguire lo strumento più volte.
3. Pertanto è possibile recuperare i dati legacy o eseguire manualmente la nuova distribuzione di toohello che si dispone di hello opzione toocopy hello dischi profili utente (UPD) tooyour nuova distribuzione. Se si sceglie toocopy il che, verrà salvare che hello e includere un file di testo che viene eseguito il mapping degli utenti di hello UPD nome tooeach.  Hello che sarà copiato tooa condivisione sul server RDSMGMT hello `F:\Shares\LegacyUPD` e verranno esposti tramite condivisione hello `\\RDSmgmt\LegacyUPD`. 
4. La migrazione non comporterà tempi di inattività per la distribuzione ARA corrente.  Tuttavia, se toohello che vengono apportate modifiche (da ARA) dopo la copia di hello, queste modifiche non si rifletteranno in hello che archiviati nel portale di gestione risorse di Azure hello. 
5. Se si dispone di altre macchine virtuali come controller di dominio e i File server nella rete virtuale di Azure classico verrà stabilita peering tra la rete virtuale di Azure classico esistente reti virtuali e hello nuova rete virtuale creata per l'utente, in hello nuova risorsa di Azure Portale di gestione.
6. La soluzione automatizzata verrà solo stabilire peering tra la rete virtuale di Azure classico esistente reti virtuali e hello nuova rete virtuale se la distribuzione ARA esistente è una distribuzione ibrida; Pertanto, si esegue l'autenticazione con Windows Server Active Directory Controller di dominio in hello Classic rete virtuale esistente. Se non si stabilisce di peering per la raccolta di reti virtuali, ma è necessario peering reti virtuali, può contattare Microsoft come [ sales@conexlink.com ](mailto:sales@conexlink.com) e sarà lieta tooconfigure peering di rete virtuale senza alcun costo aggiuntivo.
7. La soluzione automatizzata garantisce viene aggiornata la configurazione DNS di Azure hello nuova rete virtuale impostazioni tooensure la nuova distribuzione consente di connettersi tooyour presenti Controller di dominio hello rete virtuale classica.
8. La soluzione automatizzata garantisce che non sono presenti conflitti di indirizzo IP come viene creata la nuova rete virtuale e stabilire hello peering di reti virtuali per le distribuzioni con un Windows Server Active Directory Server esistente.
9. Se si utilizza Azure AD solo per l'autenticazione, MyCloudIT verrà creare un nuovo dominio Windows Server Active Directory e utilizzare Azure AD Connect toosynchronize utenti tra l'istanza esistente di Azure AD hello e hello creato nuovo Windows Server di dominio Active Directory da MyCloudIT.
10. Se si utilizza un utente di dominio Active Directory di Windows Server tooauthenticate ARA, la soluzione automatizzata si connetterà il nuovo tooyour di distribuzione MyCloudIT esistente di Controller di dominio di Windows Server Active Directory tramite il peering reti virtuali.
11. Se si usa Azure Active Directory Domain Services per l'autenticazione, è possibile eseguire la migrazione ma è necessario contattarci per consentire la creazione di un piano di migrazione personalizzato.  Invia un messaggio di posta elettronica troppo[sales@conexlink.com](mailto:sales@conexlink.com). 
12. Una volta eseguita la migrazione toobe raccolta hello è confermata, ciò che l'esecuzione automatizzata soluzione viene eseguita la migrazione la raccolta ARA e nuova toohello (facoltativo) i dischi dei profili utente: la soluzione App Remote MyCloudIT basato su.
13. Una volta completata la distribuzione di hello, verranno pubblicate nuovamente hello stesse applicazioni che sono state pubblicate in ARA e dopo la distribuzione, si sarà in grado di toopublish altre applicazioni.

## <a name="post-migration-benefits"></a>Vantaggi dopo la migrazione

1. È fornire la console di gestione hello consente toomanage hello intero ciclo di vita della distribuzione di App Remote.
2. Si sarà in grado di toomanage macchine del virtuale dal portale.  Avviare, arrestare e ridimensionare le singole macchine virtuali, se necessario.
3. console di gestione di Hello offre capacità toocreate hello e gestire gli utenti / gruppi dal portale di gestione.
4. console di gestione di Hello fornisce hello possibilità toosynchronize agli utenti Office 365 toocreate un'esperienza di accesso stesso.
5. console di gestione Hello offre hello possibilità toocreate aggiuntive App remota e Desktop raccolte senza costi utente duplicati o i requisiti minimi dell'utente. 
6. console di gestione di Hello consente hello toopublish di nuove applicazioni App Remote.
7. console di gestione di Hello offre hello possibilità tooschedule hello avvio e arresto della distribuzione di App Remote se è necessario solo la soluzione orari specifici.
8. console di gestione di Hello offre hello possibilità tooautomate hello installazione e configurazione dell'agente di Backup di Azure hello che fornisce una cronologia di conservazione di documento per i dati sui clienti.
9. console di gestione di Hello offre accesso tooperformance metriche della distribuzione.  In questo modo si hello possibilità tooidentify eventuali potenziali colli di bottiglia delle prestazioni senza installare strumenti di gestione aggiuntivi relativi alle prestazioni.
10. Se si dispone di più host della sessione, si tooenable in grado di auto scaling pertanto sola sessione hello host che devono toobe in esecuzione sono in esecuzione.
11. MyCloudIT fornisce server gateway di accesso toohello RDWeb tramite un nome di dominio MyCloudIT.  È possibile utilizzare hello possibilità toore mappa hello URL tooa personalizzato URL per la personalizzazione degli utenti finali.

## <a name="prerequisites-for-migration"></a>Prerequisiti per la migrazione

1. È necessario avere accesso toohello sottoscrizione di Azure che ospita la soluzione corrente di Azure RemoteApp.
2. È necessario concedere autorizzazioni nostro portale entro toomigrate la sottoscrizione del modello e toocreate / modificare la nuova distribuzione MyCloudIT.
3. Si noti che a causa di limitazione tooa Azure RemoteApp, ogni raccolta può solo essere migrato tre volte.  Se è necessario un insieme di toomigrate più di tre volte, è possibile generare un tooincrease tooAzure ticket il conteggio di esportazione o Contattaci e che fornirà assistenza in numero di hello ARA richieste tooincrease hello esportazione.

## <a name="mycloudit-billing"></a>Fatturazione di MyCloudIT

Vedere [MyCloudIT prezzi per le soluzioni di RemoteApp](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) per informazioni su come toopredict e gestire i costi generali di Azure.

Se si dispone ancora di domande, contattare Microsoft all'indirizzo [ sales@conexlink.com ](mailto:sales@conexlink.com) o guardare video dimostrativo completo hello [utilità di migrazione ad Azure RemoteApp - MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s). 

