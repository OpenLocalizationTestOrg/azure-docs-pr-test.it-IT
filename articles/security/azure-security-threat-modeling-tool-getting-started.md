---
title: aaaGetting Started - modellazione strumento Microsoft Threat - Azure | Documenti Microsoft
description: "Si tratta di una panoramica più approfondita evidenziazione hello strumento di modellazione delle minacce in azione."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 75ef139071e8abd0e743aa17b443a6e353f29372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-threat-modeling-tool"></a>Introduzione a hello strumento di modellazione delle minacce

Hello Cloud e strumenti di sicurezza dell'organizzazione rilasciato hello anteprima dello strumento di modellazione minaccia di quest'anno come gratuito  **[fare clic per scaricare](https://aka.ms/tmtpreview)**. modifica di Hello il meccanismo di recapito consente toopush hello più recenti miglioramenti e correzioni di bug toocustomers ogni volta che aprono strumento hello, rendendo più semplice toomaintain e utilizzare.
In questo articolo illustra il processo di hello di introduzione a approccio di modellazione delle minacce hello Microsoft SDL e Mostra come modelli di rischio elevato toodevelop toouse hello strumento come backbone del processo di protezione.

Questo articolo si basa sulle conoscenze di approccio di modellazione delle minacce SDL hello. Per una rapida panoramica, vedere troppo**[Threat Modeling Web Applications](https://msdn.microsoft.com/library/ms978516.aspx)**  e la versione archiviata di  **[scoprire di difetti di sicurezza utilizzando hello approccio STRIDE](https://docs.google.com/viewer?a=v&pid=sites&srcid=ZGVmYXVsdGRvbWFpbnxzZWN1cmVwcm9ncmFtbWluZ3xneDo0MTY1MmM0ZDI0ZjQ4ZDMy)**  MSDN articolo pubblicato nel 2006.

riepilogare tooquickly, approccio hello prevede la creazione di un diagramma, identificazione di minacce, ridurre tali rischi e convalida ogni riduzione. Di seguito è riportato un diagramma che illustra questo processo:

![Processo SDL](./media/azure-security-threat-modeling-tool/sdlapproach.png)

## <a name="starting-hello-threat-modeling-process"></a>Inizio hello processo di modellazione

Quando si avvia hello strumento di modellazione delle minacce, si noterà che alcuni fattori, come illustrato nell'immagine hello:

![Pagina iniziale vuota](./media/azure-security-threat-modeling-tool/tmtstart.png)

### <a name="threat-model-section"></a>Sezione del modello di minaccia

| Componente                                   | Dettagli                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pulsante Commenti, Suggerimenti e Problemi** | Accetta hello  **[Forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sdlprocess)**  su tutti gli aspetti SDL. Fornisce un tooread opportunità tramite altri svolte dagli utenti, insieme ai consigli e soluzioni alternative. Se ancora non si trova ciò che sta cercando, inviare tramite posta elettronica tmtextsupport@microsoft.com per il nostro toohelp team di supporto è                                                                                                                            |
| **Creare un modello**                          | Apre un canvas vuoto per si toodraw del diagramma. Verificare che tooselect quale modello toouse desiderato per il modello                                                                                                                                                                                                                                                                                                                                                                       |
| **Modello di base per la modellazione**                 | È necessario selezionare quali toouse modello prima di creare un modello. Il nostro modello principale è hello Azure modello modello, che contiene gli stencil specifici di Azure, minacce e le misure di attenuazione. Per i modelli generici, selezionare hello SDL TM Knowledge Base dal menu a discesa hello. Toocreate un modello personalizzato o di inviare una nuova istanza per tutti gli utenti? Estrarre il nostro  **[modello Repository](https://github.com/Microsoft/threat-modeling-templates)**  toolearn GitHub Page più                              |
| **Aprire un modello**                            | <p>Vengono aperti modelli di minacce salvati in precedenza. funzionalità di Hello modelli aperti di recente è molto utile se occorre tooopen i file più recente. Quando si passa il mouse sulla selezione di hello, sono disponibili 2 modi tooopen modelli:</p><p><ul><li>Apertura dal computer in uso: un modo classico per aprire un file utilizzando l'archiviazione locale</li><li>Apri da OneDrive-i team possono usare le cartelle in OneDrive toosave e condividere tutti i modelli di rischio in collaborazione e aumentare la produttività toohelp unica posizione</li></ul></p> |
| **Guida introduttiva**                   | Verrà visualizzata la hello  **[strumento di modellazione di Microsoft Threat](./azure-security-threat-modeling-tool.md)**  pagina principale                                                                                                                                                                                                                                                                                                                                                                                            |

### <a name="template-section"></a>Sezione del modello di partenza

| Componente               | Dettagli                                                                                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Crea nuovo modello** | Apre un modello vuoto per si toobuild in. A meno che non si dispone di una Knowledge Base estesa nella creazione di modelli da zero, è consigliabile toobuild dalle funzioni esistenti |
| **Apri modello**       | Apre esistente modelli per le modifiche toomake troppo                                                                                                             |

il team di strumento di modellazione delle minacce Hello è costantemente esperienze e funzionalità dello strumento tooimprove. Alcune lievi modifiche potrebbero essere eseguito nel corso di hello di hello anno, ma tutte le principali modifiche apportate richiedono di riscrivere più volte nella Guida di hello. Fare riferimento tooit spesso tooensure si ottiene ultimi annunci hello.

## <a name="building-a-model"></a>Creazione di un modello

In questa sezione si seguiranno:

- Cristina (uno sviluppatore)
- Ricardo (un program manager) e
- Ashish (un tester)

Dovranno processo hello di sviluppo il primo modello di minaccia.

> Ricardo: Salve Cristina, io ho lavorato a diagramma del modello di minaccia hello e desidera toomake che abbiamo dettagli hello destra. Puoi darmi una mano a controllare?
> Cristina: Certo. Vediamo.
> Ricardo apre strumento hello e condivide la schermata con Cristina.

![Modello di minaccia di base](./media/azure-security-threat-modeling-tool/basictmt.png)

> Cristina: OK, sembra semplice, ma puoi spiegarmelo?
> Ricardo: Certo! Ecco suddivisione hello:
> - L'utente è disegnato come un'entità esterna: un quadrato
> - Si sta inviando i server Web di comandi tooour: cerchio hello
> - server Web Hello è consultato un database (due linee parallele)

Ciò che Ricardo ha appena mostrato a Cristina è un DFD, abbreviazione di **[diagramma di flusso dei dati](https://en.wikipedia.org/wiki/Data_flow_diagram)**. Strumento di modellazione delle minacce Hello consente i confini del trust toospecify gli utenti, indicati da linee tratteggiate rosse hello, tooshow in cui sono entità diverse nel controllo. Ad esempio, gli amministratori IT richiedono un sistema di Active Directory per l'autenticazione, quindi hello Active Directory è di fuori del controllo.

> Cristina: Ricerca toome destra. Informazioni sulle minacce hello?
> Ricardo: Ti mostro.

## <a name="analyzing-threats"></a>Analisi delle minacce

Quando si fa clic su visualizzazione analisi hello da hello icona selezione dei menu (file con lente di ingrandimento), che viene eseguito l'elenco di tooa di minacce generato hello strumento di modellazione del rischio trovato basata sul modello predefinito di hello, che utilizza l'approccio SDL hello definito  **[ STRIDE (Spoofing, manomissioni, divulgare informazioni, Denial of Service ed elevazione dei privilegi)](https://en.wikipedia.org/wiki/STRIDE_(security))**. l'idea Hello è che i software viene fornito in una serie stimabile di minacce, che possono essere recuperate tramite queste 6 categorie.

Questo approccio è simile a proteggere la casa garantendo ogni porta e la finestra dispone di un meccanismo di blocco prima di aggiungere un sistema di allarme o la ricerca dopo ladro hello.

![Minacce di base](./media/azure-security-threat-modeling-tool/basicthreats.png)

Ricardo inizia selezionando hello primo elemento elenco hello. Di seguito è illustrato ciò che accade:

In primo luogo, è stata migliorata l'interazione di hello tra due stencil hello

![Interazione](./media/azure-security-threat-modeling-tool/interaction.png)

In secondo luogo, ulteriori informazioni sulla minaccia hello viene visualizzata nella finestra di proprietà minaccia hello

![Informazioni di interazione](./media/azure-security-threat-modeling-tool/interactioninfo.png)

minaccia Hello generato quest'ultimo consente di comprendere i potenziali difetti di progettazione. categorizzazione STRIDE Hello consente un'idea su vettori di attacco potenziale, mentre hello descrizione aggiuntiva indica esattamente quali è errato, insieme ai potenziali toomitigate modi. Si possono usare note toowrite campi modificabili in dettagli giustificazione hello o modificare le classificazioni di priorità a seconda della barra di bug della propria organizzazione.

Modelli di Azure sono utenti toohelp dettagli aggiuntivi comprendere non solo qual è il problema, ma anche come toofix per l'aggiunta di descrizioni, esempi e i collegamenti ipertestuali documentazione tooAzure specifiche.

Descrizione Hello apportate lui comprendono hello importanza dell'aggiunta di un utenti tooprevent meccanismo di autenticazione dal spoofing, divulgazione di hello prima minaccia toobe lavorando. Alcuni minuti in discussione hello con Cristina, sono riconosciute importanza hello dell'implementazione di controllo di accesso e i ruoli. Ricardo compilato toomake alcune brevi note che questi sono stati implementati.

Come Ricardo è entrato nella minacce hello sotto la diffusione di informazioni, ha realizzato piano di controllo di accesso hello necessari alcuni account di sola lettura per la generazione di report e di controllo. Ha chiesto se deve essere una minaccia per la nuova, ma sono state le misure di attenuazione hello hello stesso, in modo egli conseguentemente annotato minaccia hello.
Ha inoltre pensato la diffusione di informazioni di un bit più e realizzata che prevede di nastri di backup hello tooneed crittografia, un processo per il team addetto alle operazioni hello.

Minacce progettazione toohello non applicabile a causa di sicurezza o le misure di attenuazione tooexisting garantisce può essere modificato troppo "Non applicabile" dall'elenco a discesa stato hello. Vi sono tre altre opzioni: non è stato avviato: selezione predefinita, richiede analisi: utilizzato toofollow sugli elementi e motivo attenuato: una volta che viene completamente elaborata.

## <a name="reports--sharing"></a>Report e condivisione

Una volta Ricardo passa attraverso l'elenco di hello con Cristina e consente di aggiungere note importanti, le misure di attenuazione/motivazioni, priorità e lo stato viene modificato, egli Seleziona report -> Creazione Report completo -> Salva Report, un accessorio che stampa un report di quest'ultimo toogo tramite con i colleghi tooensure hello di sicurezza appropriate lavoro viene implementato.

![Informazioni di interazione](./media/azure-security-threat-modeling-tool/report.png)

Ricardo file hello tooshare invece, deve è possibile farlo facilmente salvando nell'account OneDrive dell'organizzazione. Una volta lo fa che egli può copiare il collegamento al documento hello e condividerlo con i colleghi. 

## <a name="threat-modeling-meetings"></a>Riunioni per la modellazione delle minacce

È stato underwhelmed quando Ricardo inviati minaccia modello toohis colleghi utilizzando OneDrive, Ashish, tester hello. Apparentemente Ricardo e Cristina hanno trascurato alcune aree importanti che potrebbero essere compromessi facilmente. Il suo completo scetticismo è un modello di toothreat complemento.

In questo scenario, una volta Ashish impiegato nel modello di minaccia hello, ha chiamato per le riunioni di modellazione delle minacce due: una riunione toosynchronize procedura diagrammi hello e quindi una riunione di secondo per la revisione di minaccia e approvazione e il processo di hello.

Nella prima riunione hello, Ashish impiegato per scorrere tutti gli utenti tramite hello SDL processo di modellazione di 10 minuti. Quindi verso diagramma del modello di minaccia hello e avviata, descrivere in dettaglio. Entro cinque minuti viene individuato un importante componente mancante.

Alcuni minuti in seguito, Ashish e Ricardo ottenuto in un'analisi approfondita su come server Web hello è stata compilata. Non è ideale hello per tooproceed una riunione, ma tutti gli utenti concordato infine che l'individuazione discrepanza hello in anticipo stava toosave che li periodo di tempo in futuro hello.

In hello secondo riunione, il team di hello esaminato in dettaglio minacce hello, trattati alcuni tooaddress modi firmati e usarle off per il modello di minaccia hello. Sono archiviati documento hello nel controllo del codice sorgente e continua con lo sviluppo.

## <a name="thinking-about-assets"></a>Considerazione degli asset

Alcuni lettori che si sono occupati di modellazione di minacce possono notare che non abbiamo parlato di asset. È stato individuato che molti ingegneri comprendano meglio che comprendano il concetto di hello delle risorse e quali risorse un utente malintenzionato potrebbe risultare interessante il proprio software.

Se si ha intenzione di toothreat del modello di una casa, è possibile iniziare definendo sull'importante grafica o di foto di famiglia, non sostituibili. È possibile iniziare ad esempio pensare che potrebbero interrompere il funzionamento e il sistema di sicurezza corrente hello. Oppure potrebbe considerare innanzitutto hello caratteristiche fisiche, ad esempio pool hello o piedistallo anteriore hello. Questi sono analoghi toothinking sulle risorse, gli utenti malintenzionati o la progettazione del software. Ciascuno di questi tre approcci funziona.

modellazione di toothreat approccio Hello che è stata presentata in questo documento è notevolmente più semplice rispetto a quello Microsoft ha eseguito in hello precedente. È stato rilevato che l'approccio di progettazione software hello funziona bene per molti team. Ci auguriamo che sia così anche per il lettore.

## <a name="next-steps"></a>Passaggi successivi

Inviare domande, commenti e dubbi tootmtextsupport@microsoft.com. **[Scaricare](https://aka.ms/tmtpreview)**  tooget strumento di modellazione delle minacce hello avviato.
