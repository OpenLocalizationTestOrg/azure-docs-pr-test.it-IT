---
title: le distribuzioni PaaS aaaSecuring | Documenti Microsoft
description: " Comprendere i vantaggi di sicurezza hello di PaaS e altri modelli di servizio cloud e apprendere le procedure consigliate per proteggere la distribuzione PaaS di Azure. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: techlake
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: b94fe03b6f3a43d82e1e6e834f10a423e4c1db95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-deployments"></a>Protezione delle distribuzioni PaaS

In questo articolo vengono fornite informazioni che consentono di:

- Comprendere i vantaggi di sicurezza hello di hosting di applicazioni nel cloud hello
- Valutare i vantaggi di sicurezza hello della piattaforma come servizio (PaaS) e altri modelli di servizio cloud
- Modificare lo stato attivo per la protezione da un approccio di sicurezza tooan incentrati sulla rete perimetrale incentrata sull'identità
- Implementare le procedure consigliate per la sicurezza del modello PaaS

## <a name="cloud-security-advantages"></a>Vantaggi della sicurezza cloud
Nel cloud hello esistono toobeing vantaggi di sicurezza. In un ambiente locale, le organizzazioni che hanno risorse limitate tooinvest disponibili nella sicurezza, che consente di creare un ambiente in cui gli utenti malintenzionati in grado di tooexploit vulnerabilità in tutti i livelli e responsabilità non soddisfatta.

![Vantaggi di sicurezza dell'era cloud][1]

Le organizzazioni è tooimprove in grado del rilevamento delle minacce e tempi di risposta tramite un provider funzionalità di sicurezza basato su cloud e intelligence cloud.  Spostando i provider di cloud toohello responsabilità, le organizzazioni possono raggiungere più code coverage di sicurezza, che li abilita tooreallocate risorse di sicurezza e le priorità business tooother del budget.

## <a name="division-of-responsibility"></a>Suddivisione della responsabilità
È importante toounderstand divisione di hello di responsabilità con Microsoft. In locale, si è proprietari dello stack intero hello ma durante lo spostamento cloud toohello alcune responsabilità trasferimento tooMicrosoft. Hello responsabilità matrice seguente mostra aree hello dello stack hello in una distribuzione IaaS, PaaS e SaaS che si è responsabili e Microsoft è responsabile.

![Aree di responsabilità][2]

Per tutti i tipi di distribuzione cloud, l'utente è proprietario di dati e identità. Si sono responsabili per proteggere la sicurezza hello dei dati e alle risorse locali, identità e hello componenti cloud, che è possibile controllare (che varia in base al tipo di servizio).

Funzionalità che vengono sempre mantenuti dall'utente, indipendentemente dal tipo di distribuzione, di hello sono:

- Dati
- Endpoint
- Account
- gestione degli accessi

## <a name="security-advantages-of-a-paas-cloud-service-model"></a>Vantaggi di sicurezza di un modello di servizio cloud PaaS
Utilizzando hello stessa matrice responsabilità, si esaminerà i vantaggi di sicurezza hello di una distribuzione PaaS di Azure o in locale.

![Vantaggi di sicurezza del modello PaaS][3]

A partire dalla parte inferiore di hello dello stack di hello, infrastruttura fisica hello, Microsoft riduce i rischi comuni e responsabilità. Poiché Microsoft cloud hello viene continuamente monitorata da Microsoft, è tooattack disco rigido. Può non essere opportuno per hello di toopursue un utente malintenzionato cloud Microsoft come destinazione. A meno che l'utente malintenzionato di hello ha una grande quantità di denaro e risorse, l'autore dell'attacco hello è probabilmente toomove nella destinazione tooanother.  

Centro hello dello stack di hello, non vi è alcuna differenza tra una distribuzione PaaS e locale. A livello di applicazione hello e livello di gestione di account e accedere hello, si presenta rischi simili. Nella sezione passaggi successivi hello di questo articolo, verrà illustrato consigliate toobest per eliminare o ridurre al minimo i rischi.

Nella parte superiore di hello di stack hello, governance dei dati e rights management, sono in uno dei rischi che possono essere limitati gestione delle chiavi. descritta nelle procedure consigliate. Durante la gestione delle chiavi è una responsabilità aggiuntiva, sono disponibili aree in una distribuzione PaaS che non è più necessario toomanage in modo è possibile spostare la gestione delle risorse tookey.

Hello piattaforma Azure offre anche protezione DDoS avanzata tramite varie tecnologie di rete. Tuttavia, tutti i tipi di protezione da attacchi DDoS basati su rete hanno vari limiti per quanto riguarda collegamenti e data center. toohelp evitare l'impatto di hello di grandi dimensioni attacchi DDoS, è possibile sfruttare funzionalità cloud di base di Azure consente tooquickly e automaticamente toodefend attacchi DDoS di scalabilità. Questi aspetti verranno approfonditi più dettagli su come è possibile farlo in hello consigliata gli articoli di procedure consigliate.

## <a name="modernizing-hello-defenders-mindset"></a>Modello mentale del modernizzazione hello defender
Le distribuzioni sono un cambiamento del toosecurity approccio generale con PaaS. Si passa da tutti gli elementi che richiedono toocontrol manualmente responsabilità toosharing con Microsoft.

Un'altra differenza significativa tra PaaS e le distribuzioni locali tradizionali, è una nuova visualizzazione di ciò che definisce il perimetro di sicurezza primario hello. In passato, perimetro di sicurezza locale primario hello stato della rete e più locali sicurezza progettazioni utilizzare hello rete come il punto pivot protezione primaria. Per le distribuzioni PaaS, consigliabile considerare perimetro di sicurezza primario di identità toobe hello.

## <a name="identity-as-hello-primary-security-perimeter"></a>Identità come il perimetro di sicurezza primario hello
Uno dei cinque caratteristiche essenziali hello del cloud computing è ampio accesso alla rete, che rende incentrato su rete pensiero meno pertinenti. obiettivo di Hello gran parte del cloud computing è utenti tooallow tooaccess risorse indipendentemente dalla posizione. Per la maggior parte degli utenti, la loro posizione succede toobe in qualche punto hello Internet.

Hello figura riportata di seguito viene illustrato come il perimetro di sicurezza hello è stato migliorato da una rete perimetrale tooan identità perimetrale. Sicurezza diventa meno sulla protezione della rete e altre informazioni su proteggendo i dati, nonché la gestione della sicurezza hello di App e gli utenti. la differenza principale Hello è quella aziendale tooyour importante del toopush sicurezza più vicino toowhat.

![L'identità come nuovo perimetro di sicurezza][4]

Inizialmente, i servizi PaaS di Azure come i ruoli Web e SQL di Azure non offrivano difese con perimetri di rete tradizionali. È stata indicata che scopo dell'elemento hello toobe esposti toohello Internet (ruolo web) e che l'autenticazione garantisce perimetrale di nuovo hello (ad esempio BLOB o SQL Azure).

Procedure consigliate di sicurezza più recenti si presuppongono che avversario hello ha violato perimetro della rete hello. Pertanto, procedure consigliate di difesa moderne sono stati spostati tooidentity. Le organizzazioni devono stabilire un perimetro di sicurezza basato sull'identità con procedure consigliate di autenticazione e autorizzazione estremamente robuste.

## <a name="recommendations-for-managing-hello-identity-perimeter"></a>Suggerimenti per la gestione perimetrale identità hello

Principi e modelli per perimetro della rete hello stati disponibili per molti anni. Al contrario, settore hello è relativamente minore esperienza con identità come il perimetro di sicurezza primario hello. Ciò premesso, abbiamo accumulati sufficiente tooprovide esperienza alcuni consigli generali che si sono rivelati nel campo hello e applicare tooalmost tutti i servizi PaaS.

esempio Hello riepiloga un toomanaging di approccio generale migliore di procedure consigliate del perimetro di identità.

- **Non perdere le chiavi o le credenziali** la protezione di chiavi e le credenziali è essenziale toosecure le distribuzioni PaaS. Perdere chiavi e credenziali è un problema comune. Una buona soluzione è toouse una soluzione centralizzata in cui le chiavi e i segreti possono essere archiviati in moduli di protezione hardware (HSM). Azure fornisce un modulo HSM nel cloud hello con [insieme credenziali chiavi Azure](../key-vault/key-vault-whatis.md).
- **Non è opportuno inserire le credenziali e altri segreti nel codice sorgente o GitHub** hello solo peggiorando cosa di perdere le chiavi e le credenziali è un'entità non autorizzata ottenere accedere toothem. Gli utenti malintenzionati sono tootake in grado di sfruttare i segreti archiviati nel repository di codice, ad esempio GitHub e chiavi di toofind di tecnologie bot. Si consiglia pertanto di non inserire chiavi e segreti in questi archivi di codice sorgente pubblici.
- **Proteggere le interfacce di gestione delle macchine virtuali nei servizi PaaS e IaaS ibridi** I servizi IaaS e PaaS vengono eseguiti in macchine virtuali. In base al tipo di hello del servizio, sono disponibili diverse interfacce di gestione che consentono di tooremote gestire queste macchine virtuali direttamente. È possibile usare protocolli di gestione remota, ad esempio [Secure Shell Protocol (SSH)](https://en.wikipedia.org/wiki/Secure_Shell), [Remote Desktop Protocol (RDP)](https://support.microsoft.com/kb/186607) e [Remote PowerShell](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting). In generale, è consigliabile non abilitare l'accesso remoto diretto tooVMs da hello Internet. Se disponibile, è consigliabile usare approcci alternativi, ad esempio tramite una rete virtuale privata di Azure. Se non sono disponibili soluzioni alternative, assicurarsi di usare passphrase complesse e, se disponibile, l'autenticazione a due fattori (ad esempio [Multi-Factor Authentication di Azure](../multi-factor-authentication/multi-factor-authentication.md)).
- **Usare piattaforme di autenticazione e autorizzazione robuste**

  - Usare le identità federate in Azure AD invece degli archivi utente personalizzati. Quando si usa identità federate, sfruttare i vantaggi di un approccio basato su piattaforma e delegare la gestione di hello partner tooyour identità autorizzati. Un approccio di identità federativa è particolarmente importante negli scenari quando i dipendenti vengono terminati e le informazioni necessarie toobe applicata tramite più identità e autorizzazione sistemi.
  - Usare i meccanismi di autenticazione e autorizzazione forniti dalla piattaforma invece di un codice personalizzato motivo di Hello è che lo sviluppo di codice di autenticazione personalizzata può essere soggetta a errori. La maggior parte degli sviluppatori non sono esperti di sicurezza e improbabile toobe comunicata sfumature hello e hello ultimi sviluppi autenticazione e autorizzazione. Il codice commerciale, ad esempio quello di Microsoft, è spesso soggetto a rigorose analisi di sicurezza.
  - Usare l'autenticazione a più fattori. Multi-factor authentication è hello corrente standard per l'autenticazione e autorizzazione in quanto evita hello sicurezza deboli tipi di nome utente e password di autenticazione. Interfacce di gestione di Azure (portale/remoto PowerShell) di accesso tooboth hello e toocustomer servizi devono essere progettate e configurato toouse [Azure multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md).
  - Usare protocolli di autenticazione standard come OAuth2 e Kerberos. Questi protocolli sono stati ampiamente analizzati e sono probabilmente implementati come parte delle librerie della piattaforma per autenticazione e autorizzazione.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo sono stati illustrati i vantaggi di sicurezza di una distribuzione PaaS di Azure. Il passaggio successivo è costituito dall'approfondimento delle procedure consigliate per proteggere le soluzioni PaaS Web e mobili. Si inizierà dai servizi app di Azure, dal database SQL di Azure e da SQL Data Warehouse di Azure. Quando gli articoli di procedure consigliate per altri servizi di Azure sono disponibili, i collegamenti verranno forniti in hello seguente elenco:

- [servizio app di Azure](security-paas-applications-using-app-services.md)
- [Database SQL di Azure e SQL Data Warehouse di Azure](security-paas-applications-using-sql.md)
- Archiviazione di Azure
- Cache REDIS di Azure
- Bus di servizio di Azure
- Web application firewall

<!--Image references-->
[1]: ./media/security-paas-deployments/advantages-of-cloud.png
[2]: ./media/security-paas-deployments/responsibility-zones.png
[3]: ./media/security-paas-deployments/advantages-of-paas.png
[4]: ./media/security-paas-deployments/identity-perimeter.png
