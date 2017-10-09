---
title: Azure AD Connect Health per la sincronizzazione aaaUsing | Documenti Microsoft
description: "Questo è hello Azure AD Connect Health pagina verrà illustrate le modalità di sincronizzazione toomonitor Azure AD Connect."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>Monitorare la sincronizzazione di Azure AD Connect con Azure AD Connect Health
Hello seguente documentazione è specifico toomonitoring Azure AD Connect (sincronizzazione) con Azure AD Connect Health.  Per informazioni sul monitoraggio di AD FS con Azure AD Connect Health, vedere [Uso di Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md). Per informazioni sul monitoraggio di Servizi di dominio Active Directory con Azure AD Connect Health, vedere [Uso di Azure AD Connect Health con Servizi di dominio Active Directory](active-directory-aadconnect-health-adds.md).

![Azure AD Connect Health per la sincronizzazione](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Avvisi per Azure AD Connect Health per la sincronizzazione
Hello Azure AD Connect gli avvisi di integrità per la sezione di sincronizzazione fornisce che si hello elenco degli avvisi attivi. Ogni avviso include informazioni pertinenti, procedure di risoluzione e collegamenti toorelated documentazione. Selezionando un avviso attivo o risolto verrà visualizzato un nuovo pannello con informazioni aggiuntive, nonché i passaggi da eseguire avviso hello tooresolve e collegamenti tooadditional documentazione. Inoltre, è possibile visualizzare i dati cronologici avvisi risolti in hello precedente.

Selezionando un avviso che all'utente verrà fornito con informazioni aggiuntive, nonché i passaggi sono disponibili i collegamenti e avviso hello tooresolve tooadditional documentazione.

![Errore del servizio di sincronizzazione Azure AD Connect](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Valutazione limitata degli avvisi
Se Azure AD Connect non usa la configurazione predefinita di hello (ad esempio, se il filtro di attributi viene modificato da configurazione personalizzata tooa di hello configurazione predefinita), quindi l'agente hello Azure AD Connect Health non caricherà hello errore eventi correlati tooAzure AD Connect.

Questo limita la valutazione hello degli avvisi dal servizio hello. Si verrà visualizzato un messaggio che indica la condizione nel file hello portale di Azure con il servizio.

![Azure AD Connect Health per la sincronizzazione](./media/active-directory-aadconnect-health-sync/banner.png)

È possibile modificare questo facendo clic su "Impostazioni" e consentendo tooupload agente di Azure AD Connect Health tutti i log degli errori.

![Azure AD Connect Health per la sincronizzazione](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Informazioni dettagliate sulla sincronizzazione
Gli amministratori spesso desidera tooknow su hello tempo toosync modifiche tooAzure Active Directory e la quantità di hello di modifiche in corso. Questa funzionalità fornisce un modo semplice di toovisualize questo utilizzando hello sotto grafici:   

* Latenza delle operazioni di sincronizzazione
* Tendenza nelle modifiche agli oggetti

### <a name="sync-latency"></a>Latenza della sincronizzazione
Questa funzionalità fornisce una tendenza grafica della latenza operazioni hello sincronizzazione (importazione, esportazione e così via) per i connettori.  Fornisce una rapida e semplice toounderstand hello non solo latenza delle operazioni (maggiore se si dispone di un ampio set di modifiche che si verificano), ma anche eventuali anomalie toodetect un modo latenza hello che potrebbero richiedere un'ulteriore analisi.

![Latenza della sincronizzazione](./media/active-directory-aadconnect-health-sync/synclatency02.png)

Per impostazione predefinita, solo la latenza di hello dell'operazione di hello 'Export' per il connettore Azure AD hello viene visualizzata.  toosee altre operazioni sul connettore hello o tooview da altri connettori, fare clic sul grafico hello, selezionare Modifica grafico o fare clic sul pulsante "Modifica grafico latenza" hello e scegliere l'operazione specifica hello e connettori.

### <a name="sync-object-changes"></a>Sincronizzazione delle modifiche agli oggetti
Questa funzionalità fornisce una tendenza con interfaccia grafica di hello numerose modifiche che vengono valutati ed esportato tooAzure Active Directory.  Oggi, durante il tentativo di toogather le informazioni dal log di sincronizzazione hello sono difficile.  grafico Hello offre, non solo un modo più semplice di monitoraggio numero hello di modifiche che si sono verificati nell'ambiente in uso, ma anche una visualizzazione di errori di hello che si sono verificati.

![Latenza della sincronizzazione](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Report degli errori di sincronizzazione a livello di oggetto (anteprima)
Questa funzionalità offre un report sugli errori di sincronizzazione che possono verificarsi durante la sincronizzazione dei dati relativi alle identità tra Active Directory di Windows Server e Azure AD con Azure AD Connect.

* report Hello descrive errori registrati da client di sincronizzazione hello (Azure AD Connect versione 1.1.281.0 o versione successiva)
* Include gli errori di hello hello ultima sincronizzazione operazione nel motore di sincronizzazione hello. ("Esporta" in Azure Active Directory Connector hello.)
* Agente di Azure AD Connect Health per la sincronizzazione deve disporre di connettività in uscita toohello necessarie di punti di fine per i dati più recenti di hello report tooinclude hello.
* report Hello è **aggiornato ogni 30 minuti** utilizzando dati hello caricato dall'agente di Azure AD Connect Health per la sincronizzazione. Fornisce hello seguenti funzionalità principali

  * Categorizzazione degli errori
  * Elenco degli oggetti con errore per categoria
  * Tutti i dati di hello sugli errori di hello in un'unica posizione
  * Lato dal confronto di oggetti con errore a causa di conflitti tooa
  * Scaricare il report di errore hello come un CVS (presto disponibile)

### <a name="categorization-of-errors"></a>Categorizzazione degli errori
report Hello classifica hello esistente gli errori di sincronizzazione in hello seguenti categorie:

| Categoria | Descrizione |
| --- | --- |
| Attributo duplicato |Errori che si verificano quando Azure AD Connect prova a creare o aggiornare oggetti con valori duplicati per uno o più attributi di Azure AD che devono essere univoci in un tenant, come proxyAddresses o UserPrincipalName. |
| Dati non corrispondenti |Errori quando hello soft-corrispondenza ha esito negativo toomatch oggetti che generano errori di sincronizzazione. |
| Errore di convalida dei dati |Gli errori a causa di dati tooinvalid, ad esempio i caratteri non supportati in attributi importanti, ad esempio UserPrincipalName, formattare gli errori che non superano la convalida prima di essere scritte in Azure AD. |
| Attributo di grandi dimensioni |Gli errori quando uno o più attributi sono maggiori di hello consentito dimensioni, lunghezza o al conteggio. |
| Altre |Tutti gli altri errori che non rientrano nel hello sopra le categorie. Questa categoria verrà suddivisa in sottocategorie in base ai commenti e suggerimenti. |

![Riepilogo del report degli errori di sincronizzazione](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Categorie del report degli errori di sincronizzazione](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>Elenco degli oggetti con errore per categoria
Drill-down ogni categoria fornirà elenco hello di oggetti con errore hello in tale categoria.
![Elenco del report degli errori di sincronizzazione](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Dettagli errore
Dati è disponibile in hello visualizzazione per ogni errore dettagliata

* Gli identificatori per hello *oggetto Active Directory* coinvolti
* Gli identificatori per hello *oggetto AD Azure* coinvolti (se applicabile)
* Descrizione dell'errore e come toofix
* Articoli correlati

![Dettagli del report degli errori di sincronizzazione](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a>Scaricare il report di errore hello in formato CSV
Selezionando hello "" pulsante Esporta è possibile scaricare un file CSV con tutti i dettagli di hello tutti gli errori di hello.

## <a name="related-links"></a>Collegamenti correlati
* [Risoluzione degli errori durante la sincronizzazione](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [Resilienza degli attributi duplicati](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Installazione dell'agente di Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operazioni di Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso di Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso di Azure AD Connect Health con Servizi di dominio Active Directory](active-directory-aadconnect-health-adds.md)
* [Domande frequenti su Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Cronologia delle versioni di Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)