---
title: "aaaLearn su hello più recenti versioni del sistema operativo Guest di Azure | Documenti Microsoft"
description: "Novità di versione più recente Hello e compatibilità SDK per sistema operativo Guest di servizi Cloud di Azure."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 6306cafe-1153-44c7-8554-623b03d59a34
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 8/24/2017
ms.author: raiye
ms.openlocfilehash: 7274f5a68a32ce91bdede77e1443cdb8053c07ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-releases-and-sdk-compatibility-matrix"></a>Rilasci del sistema operativo guest Azure e matrice di compatibilità dell'SDK
Vengono fornite informazioni aggiornate sulle versioni più recenti del sistema operativo Guest Azure per i servizi Cloud hello. Queste informazioni sono utili per pianificare il percorso di aggiornamento prima che un sistema operativo guest venga disabilitato. Se si configura i ruoli toouse *automatica* degli aggiornamenti del sistema operativo Guest come descritto [impostazioni di aggiornamento del sistema operativo Guest Azure][Azure Guest OS Update Settings], non è indispensabile leggere questa pagina.

> [!IMPORTANT]
> Questa pagina si applica tooCloud servizi ruoli web e di lavoro, che sono eseguiti su un sistema operativo Guest. Caso **non applica** tooIaaS macchine virtuali.
>
>


> [!NOTE]
> Hello Feed RSS di recente è stata deprecata. Tornare a visitare questa pagina per gli aggiornamenti su un nuovo feed presto disponibile.
>
>

Certi di quali hello del sistema operativo Guest è o come hello il lavoro di versioni del sistema operativo Guest? Leggere [questa](#how-it-works) sezione.

## <a name="news-updates"></a>Novità e aggiornamenti

###### <a name="august-24-2017"></a>**24 agosto 2017**
È stato rilasciato il sistema operativo guest di agosto.

###### <a name="august-3-2017"></a>**3 agosto 2017**
È stato rilasciato il sistema operativo guest di luglio.

###### <a name="july-19-2017"></a>**19 luglio 2017**
L'implementazione del sistema operativo guest di luglio è iniziata il 19 luglio e il rilascio è previsto per l'8 agosto.

###### <a name="july-7-2017"></a>**7 luglio 2017**
È stato rilasciato il sistema operativo guest di giugno.

###### <a name="june-16-2017"></a>**16 giugno 2017**
L'implementazione del sistema operativo guest di giugno è iniziata il 16 giugno e il rilascio è previsto per l'11 luglio.

###### <a name="june-5-2017"></a>**5 giugno 2017**
È stato rilasciato il sistema operativo guest di maggio.

###### <a name="may-17-2017"></a>**17 maggio 2017**
Scadenza tooa bug di sicurezza, abbiamo stiamo disabilitazione hello seguito dicembre 2016 e gennaio January 2017 rilasci del sistema operativo che non dispongono di hello [correggere] dal portale hello: WA-GUEST-OS-5.4_201612-01, WA-GUEST-OS-4.39_201612-01, WA-GUEST-OS-3.46_ 201612-01, WA-GUEST-OS-2.59_201701-01

###### <a name="may-12-2017"></a>**12 maggio 2017**
L'implementazione del sistema operativo guest di maggio è iniziata il 12 maggio e il rilascio è previsto per l'13 giugno.

###### <a name="april-18-2017"></a>**18 aprile 2017**
L'implementazione del sistema operativo guest di aprile è iniziata il 18 aprile e il rilascio è previsto per il 9 maggio.

###### <a name="april-10-2017"></a>**10 aprile 2017**
L'implementazione del sistema operativo guest di marzo è iniziata il 14 marzo 2017 ed è stata rilasciata il 10 aprile 2017.

###### <a name="january-10-2017"></a>**10 gennaio 2017**
Hello gennaio del sistema operativo Guest contiene patch che influiscono solo sulla famiglia del sistema operativo 2 (Windows 2008 R2 Server). Microsoft ha rilasciato pertanto solo l'immagine del sistema operativo famiglia 2 hello (WA-GUEST-OS-2.59_201701-01) per questo mese. Per tutte le altre famiglie del sistema operativo, hello dicembre del sistema operativo (201612 - 01) rimane hello più recente.


## <a name="releases"></a>Rilasci
## <a name="family-5-releases"></a>Versioni della famiglia 5
**Windows Server, 2016**

Versione .NET Framework installata: 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2

> [!NOTE]
> Le date con un * sono toochange soggetto.
>
> Hello Password RDP per 5 famiglia del sistema operativo deve essere almeno 10 caratteri.
>

| Stringa di configurazione | Data di rilascio | Data di disabilitazione | Data di scadenza |
| --- | --- | --- | --- |
| WA-GUEST-OS-5.10_201708-01 |24 agosto 2017 |Dopo la versione 5.12 |Da definire |
| WA-GUEST-OS-5.9_201707-01 |3 agosto 2017 |Post 5.11 |Da definire |
| WA-GUEST-OS-5.8_201706-01 |7 luglio 2017 |Post 5.10 |Da definire |
|~~WA-GUEST-OS-5.7_201705-01~~ |5 giugno 2017 |24 agosto 2017 |Da definire |
|~~WA-GUEST-OS-5.6_201704-01~~ |9 maggio 2017 |3 agosto 2017 |Da definire |
|~~WA-GUEST-OS-5.5_201703-01~~ |10 aprile 2017 |7 luglio 2017 |Da definire |
|~~WA-GUEST-OS-5.4_201612-01~~ |10 gennaio 2017 |5 giugno 2017|Da definire |
|~~WA-GUEST-OS-5.3_201611-01~~ |14 dicembre 2016 |9 maggio 2017 |Da definire |
|~~WA-GUEST-OS-5.2_201610-02~~ |1 novembre 2016 |10 aprile 2017 |Da definire |

## <a name="family-4-releases"></a>Versioni della famiglia 4
**Windows Server 2012 R2**

Supporta .NET 4.0, 4.5, 4.5.1 e 4.5.2

> [!NOTE]
> Le date con un * sono soggetto toochange
>
>

| Stringa di configurazione | Data di rilascio | Data di disabilitazione | Data di scadenza |
| --- | --- | --- | --- |
| WA-GUEST-OS-4.45_201708-01 |24 agosto 2017 |Dopo la versione 4.47 |Da definire |
| WA-GUEST-OS-4.44_201707-01 |3 agosto 2017 |Post 4.46 |Da definire |
| WA-GUEST-OS-4.43_201706-01 |7 luglio 2017 |Post 4.45 |Da definire |
|~~WA-GUEST-OS-4.42_201705-01~~ |5 giugno 2017 |24 agosto 2017 |Da definire |
|~~WA-GUEST-OS-4.41_201704-01~~ |9 maggio 2017 |3 agosto 2017 |Da definire |
|~~WA-GUEST-OS-4.40_201703-01~~ |10 aprile 2017 |7 luglio 2017 |Da definire |
|~~WA-GUEST-OS-4.39_201612-01~~ |10 gennaio 2017 |5 giugno 2017 |Da definire |
|~~WA-GUEST-OS-4.38_201611-01~~ |14 dicembre 2016 |9 maggio 2017 |Da definire |
|~~WA-GUEST-OS-4.37_201610-02~~ |16 novembre 2016 |10 aprile 2017 |Da definire |
|~~WA-GUEST-OS-4.36_201609-01~~ |13 ottobre 2016 |14 gennaio 2017 |Da definire |
|~~WA-GUEST-OS-4.35_201608-01~~ |13 settembre 2016 |16 dicembre 2016 |Da definire |
|~~WA-GUEST-OS-4.34_201607-01~~ |8 agosto 2016 |13 novembre 2016 |Da definire |


## <a name="family-3-releases"></a>Versioni della famiglia 3
**Windows Server 2012**

Supporta .NET 4.0, 4.5, 4.5.1 e 4.5.2

> [!NOTE]
> Le date con un * sono soggetto toochange
>
>

| Stringa di configurazione | Data di rilascio | Data di disabilitazione | Data di scadenza |
| --- | --- | --- | --- |
| WA-GUEST-OS-3.52_201708-01 |24 agosto 2017 |Dopo la versione 3.54 |Da definire |
| WA-GUEST-OS-3.51_201707-01 |3 agosto 2017 |Post 3.53 |Da definire |
| WA-GUEST-OS-3.50_201706-01 |7 luglio 2017 |Post 3.52 |Da definire |
|~~WA-GUEST-OS-3.49_201705-01~~ |5 giugno 2017 |24 agosto 2017 |Da definire |
|~~WA-GUEST-OS-3.48_201704-01~~ |9 maggio 2017 |3 agosto 2017 |Da definire |
|~~WA-GUEST-OS-3.47_201703-01~~ |10 aprile 2017 |7 luglio 2017 |Da definire |
|~~WA-GUEST-OS-3.46_201612-01~~ |10 gennaio 2017 |5 giugno 2017 |Da definire |
|~~WA-GUEST-OS-3.45_201611-01~~ |14 dicembre 2016 |9 maggio 2017 |Da definire |
|~~WA-GUEST-OS-3.44_201610-02~~ |16 novembre 2016 |1 maggio 2017 |Da definire |
|~~WA-GUEST-OS-3.43_201609-01~~ |13 ottobre 2016 |14 gennaio 2017 |Da definire |
|~~WA-GUEST-OS-3.42_201608-01~~ |13 settembre 2016 |16 dicembre 2016 |Da definire |
|~~WA-GUEST-OS-3.41_201607-01~~ |8 agosto 2016 |13 novembre 2016 |Da definire |


## <a name="family-2-releases"></a>Versioni della famiglia 2
**Windows Server 2008 R2 SP1**

Supporta .NET 3.5, 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Le date con un * sono soggetto toochange
>
>

| Stringa di configurazione | Data di rilascio | Data di disabilitazione | Data di scadenza |
| --- | --- | --- | --- |
| WA-GUEST-OS-2.65_201708-01 |24 agosto 2017 |Dopo la versione 2.67 |Da definire |
| WA-GUEST-OS-2.64_201707-01 |3 agosto 2017 |Post 2.66 |Da definire |
| WA-GUEST-OS-2.63_201706-01 |7 luglio 2017 |Post 2.65 |Da definire |
|~~WA-GUEST-OS-2.62_201705-01~~ |5 giugno 2017 |24 agosto 2017 |Da definire |
|~~WA-GUEST-OS-2.61_201704-01~~ |9 maggio 2017 |3 agosto 2017 |Da definire |
|~~WA-GUEST-OS-2.60_201703-01~~ |10 aprile 2017 |7 luglio 2017 |Da definire |
|~~WA-GUEST-OS-2.59_201701-01~~ |10 gennaio 2017 |5 giugno 2017 |Da definire |
|~~WA-GUEST-OS-2.58_201612-01~~ |10 gennaio 2017 |9 maggio 2017|Da definire |
|~~WA-GUEST-OS-2.57_201611-01~~ |14 dicembre 2016 |10 aprile 2017 |Da definire |
|~~WA-GUEST-OS-2.56_201610-02~~ |16 novembre 2016 |10 febbraio 2017 |Da definire |
|~~WA-GUEST-OS-2.55_201609-01~~ |13 ottobre 2016 |14 gennaio 2017 |Da definire |
|~~WA-GUEST-OS-2.54_201608-01~~ |13 settembre 2016 |16 dicembre 2016 |Da definire |
|~~WA-GUEST-OS-2.53_201607-01~~ |8 agosto 2016 |13 novembre 2016 |Da definire |



## <a name="msrc-patch-updates"></a>Patch di aggiornamento MSRC
Hello elenco delle patch incluse in ogni versione del sistema operativo Guest mensile è disponibile [qui][patches].

## <a name="sdk-support"></a>Supporto SDK
Anche se hello [criteri di ritiro per hello Azure SDK] [ retire policy sdk] indica che solo le versioni sopra 2.2 sono supportati e specifiche famiglie di sistemi operativi Guest consentano si toouse le versioni precedenti. È consigliabile utilizzare sempre hello più recente supportata SDK.

| Famiglia del sistema operativo guest | Versioni dell’SDK compatibili |
| --- | --- |
| 5 |Versione 2.9.5.1+ |
| 4 |Versione 2.1+ |
| 3 |Versione 1.8+ |
| 2 |Versione 1.3+ |
| 1 |Versione 1.0+ |

## <a name="guest-os-release-information"></a>Informazioni sui rilasci del sistema operativo guest
Esistono tre date importanti rilascia tooGuest del sistema operativo: **versione** data, **disabilitato** data, e **scadenza** Data. Un sistema operativo Guest è considerato disponibile quando è in hello portale e può essere selezionato come destinazione di hello del sistema operativo Guest. Quando un sistema operativo Guest raggiunge hello **disabilitato** data, viene rimosso da Azure. Tuttavia, qualsiasi servizio cloud destinato a tale sistema operativo guest funzionerà normalmente.

finestra Hello tra hello **disabilitato** data e hello **scadenza** Data fornisce una transizione di tooeasily buffer da un tooone di sistemi operativi Guest più recente. Se si utilizza *automatica* come il sistema operativo Guest, AlwaysOn sarà la versione più recente di hello e non è necessario tooworry su di esso in scadenza.

Quando hello **scadenza** data viene superato, qualsiasi servizio Cloud verrà arrestato continua a usare il sistema operativo Guest, eliminato o forzato tooupgrade. È possibile leggere informazioni sui criteri di ritiro hello [qui][retirepolicy].

## <a name="guest-os-family-version-explanation"></a>Spiegazione delle famiglie e delle versioni del sistema operativo guest
famiglie di sistemi operativi Guest Hello sono basate sulle versioni rilasciate di Microsoft Windows Server. Hello del sistema operativo Guest è hello sottostante sistema operativo che viene eseguito servizi Cloud di Azure in. A ogni sistema operativo guest sono associati una famiglia, una versione e un numero di rilascio.

* **Guest OS family**  
  Una versione del sistema operativo Windows Server sulla quale è basato un sistema operativo guest. Ad esempio, la *famiglia 3* è basata su Windows Server 2012.
* **Versione del sistema operativo guest**  
  Immagine tooa specifico famiglia di sistemi operativi Guest più rilevanti [Microsoft Security Response Center (MSRC)] [ msrc] patch disponibili nella versione del sistema operativo Guest nuovo di hello data hello viene generato. È possibile che non siano incluse tutte le patch.

    I numeri iniziano da 0 e vengono incrementati di 1 a ogni aggiunta di un nuovo set di aggiornamenti. Gli zeri finali vengono visualizzati solo se sono importanti; ad esempio, la versione 2.10 è una versione diversa e successiva rispetto alla versione 2.1.
* **Rilascio del sistema operativo guest**  
  Un nuovo rilascio di una versione del sistema operativo guest. Il nuovo rilascio viene introdotto se durante la fase di test Microsoft rileva problemi che richiedono l'esecuzione di modifiche. Hello ultimo rilascio sostituisce sempre quelli precedenti versioni, pubblico o non. Hello portale di Azure consente solo agli utenti versione più recente di hello toopick per una determinata versione. Distribuzioni in esecuzione su una versione precedente non sono in genere imposto l'aggiornamento a seconda della gravità hello bug hello.

Nell'esempio hello seguente, 2 è una famiglia di hello, 12 è una versione di hello e "rel2" è la versione di hello.

**Rilascio del sistema operativo guest** - 2.12 rel2

**Stringa di configurazione per questo rilascio** - WA-GUEST-OS-2.12_201208-02

la stringa di configurazione per un sistema operativo Guest Hello ha le stesse informazioni incorporate, insieme a una data che mostra le patch MSRC che sono state considerate per tale versione. In questo esempio, patch di MSRC prodotte per Windows Server 2008 R2 di tooand ad agosto 2012 sono state considerate per l'inclusione. Solo le patch si applicano specificatamente toothat versione di Windows Server sono incluse. Ad esempio, se una patch MSRC si applica tooMicrosoft Office, non sarà inclusa poiché il prodotto non è parte dell'immagine di base del Server di Windows hello.

## <a name="guest-os-system-update-process"></a>Processo di aggiornamento del sistema operativo guest
In questa pagina vengono fornite informazioni sui prossimi rilasci del sistema operativo guest. I clienti hanno indicato che desiderano tooknow quando viene rilasciata una versione poiché i ruoli del servizio cloud verranno riavviato se sono impostati aggiornamento troppo "automatico". Versioni del sistema operativo guest in genere si verificano almeno cinque (5) giorni dalla hello dell'aggiornamento di MSRC versione che si verifica in hello secondo martedì di ogni mese. Le nuove versioni includono tutte hello patch importanti di MSRC per ogni famiglia del sistema operativo Guest.

Gli aggiornamenti di Microsoft Azure vengono rilasciati costantemente. Hello del sistema operativo Guest è solo uno di tali aggiornamenti nella pipeline hello. Una versione può essere influenzata da molti fattori troppo numerosi toolist qui. Inoltre, Azure viene eseguito su centinaia di migliaia di computer. Ciò significa che è Impossibile toogive esatta data e un'ora quando si riavvierà dei ruoli. Si sta lavorando a un piano toolimit o scadenzare temporalmente i riavvii.

Quando una nuova versione di hello che del sistema operativo Guest viene pubblicato, può richiedere tempo toofully propagazione in Azure. Poiché i servizi aggiornato toohello nuovo sistema operativo Guest, sono domini di aggiornamento rispettando la distinzione tra riavviato. Gli aggiornamenti dei servizi set toouse "Automatico" verranno visualizzato un rilascio prima. Dopo l'aggiornamento di hello, si noterà nuova versione del sistema operativo Guest di hello elencata per il servizio in hello portale di Azure. Durante questo periodo possono essere introdotti dei nuovi rilasci. Alcune versioni possono essere distribuiti in più periodi di tempo e riavvii di aggiornamenti automatici non possono verificarsi per molte settimane dopo la data di rilascio ufficiale hello. Quando un sistema operativo Guest è disponibile, è possibile quindi in modo esplicito scegliere tale versione dal portale hello o nel file di configurazione.

Per moltissime informazioni importanti sui riavvii e sui puntatori toomore informazioni sui dettagli tecnici degli aggiornamenti di Guest e del sistema operativo Host, vedere il blog MSDN hello post intitolato [gli aggiornamenti di istanza del ruolo viene riavviato dovuti tooOS] [ restarts].

Se si aggiorna manualmente il sistema operativo Guest, vedere hello [criteri di ritiro del sistema operativo Guest] [ retirepolicy] per ulteriori informazioni.

## <a name="guest-os-supportability-and-retirement-policy"></a>Criteri relativi al supporto e al ritiro del sistema operativo guest
Hello criteri di supporto e sul ritiro del sistema operativo Guest viene spiegata [qui][retirepolicy].

[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure Guest OS Update Settings]: cloud-services-how-to-configure.md
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[Microsoft Security Advisory 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md
[correggere]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
