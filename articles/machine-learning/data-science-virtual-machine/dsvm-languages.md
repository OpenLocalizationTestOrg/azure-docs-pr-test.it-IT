---
title: Linguaggi per la macchina virtuale per data science in Azure | Microsoft Docs
description: Linguaggi per la macchina virtuale per data science in Azure
keywords: strumenti di analisi scientifica dei dati, macchina virtuale per l'analisi scientifica dei dati, strumenti per l'analisi scientifica dei dati, analisi scientifica dei dati per Linux
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/11/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 2f2125e739b738847e03ce429d65801969611685
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="languages-supported-on-the-data-science-virtual-machine"></a>Linguaggi supportati dalla macchina virtuali per data science 

La macchina virtuale per data science è fornita con diversi linguaggi predefiniti e con strumenti di sviluppo per la compilazione di applicazioni AI. Di seguito sono elencate alcune delle principali. 

## <a name="python"></a>Python

|    |           |
| ------------- | ------------- |
| Versioni di linguaggio supportate | 2.7 e 3.5 |
| Edizioni supportate della macchina virtuale per data science      | Linux, Windows     |
| Come viene configurato o installato sulla macchina virtuale per data science?  | Vengono creati due ambienti `conda` globali. <br /> L'ambiente * `root` disponibile all'indirizzo `/anaconda/` è Python 2.7. <br/> L'ambiente * `py35` disponibile all'indirizzo `/anaconda/envs/py35` è Python 3.5.       |
| Collegamenti a esempi      | Sono inclusi Notebook di Jupyter di esempio per Python.     |
| Strumenti correlati nella macchina virtuale per data science      | PySpark, R, Julia      |
### <a name="how-to-use--run-it"></a>Come usarlo o eseguirlo?    

**Windows**:

* Esecuzione nel prompt dei comandi

Aprire il prompt dei comandi e seguire le procedure seguenti a seconda della versione di Python da eseguire. 

```
# To run Python 2.7
activate 
python --version

# To run Python 3.5
activate py35
python --version

```
* Utilizzo in un IDE

Usare gli strumenti Python Tools for Visual Studio (PTVS) installati in Visual Studio Community Edition. L'unico ambiente viene configurato automaticamente in PTVS in Python 2.7. 
> [!NOTE]
> Per passare a PTVS in Python 3.5, è necessario creare un ambiente personalizzato in PTVS. Per impostare questi percorsi per gli ambienti in Visual Studio Community Edition, passare a **Strumenti** -> **Strumenti Python** -> **Ambienti Python** e quindi fare clic su **+ Personalizza**. Impostare quindi il percorso su `c:\anaconda\envs\py35` e fare clic su _Rilevamento automatico_. 

* Utilizzo in Jupyter

Aprire Jupyter e fare clic sul pulsante `New` per creare un nuovo notebook. A questo punto è possibile scegliere il tipo di kernel _Python [Conda Root]_ per Python 2.7 e _Python [Conda env:py35]_ per l'ambiente di Python 3.5. 

* Installazione di pacchetti Python

Gli ambienti Python predefiniti nella macchina virtuale per data science sono ambienti globali leggibili da tutti gli utenti. Tuttavia, solo gli amministratori possono scrivere/installare i pacchetti globali. Per installare il pacchetto nell'ambiente globale, attivare la radice o l'ambiente py35 usando il comando `activate` come amministratore. È quindi possibile usare un gestore pacchetti come `conda` o `pip` per installare o aggiornare i pacchetti. 


**Linux**:

* Esecuzione nel terminale

Aprire il terminale e seguire le procedure seguenti a seconda della versione di Python da eseguire. 

```
# To run Python 2.7
source activate 
python --version

# To run Python 3.5
source activate py35
python --version

```
* Utilizzo in un IDE

Usare PyCharm installato in Visual Studio Community Edition. 

* Utilizzo in Jupyter

Aprire Jupyter e fare clic sul pulsante `New` per creare un nuovo notebook. A questo punto è possibile scegliere il tipo di kernel _Python [Conda Root]_ per Python 2.7 e _Python [Conda env:py35]_ per l'ambiente di Python 3.5. 

* Installazione di pacchetti Python

Gli ambienti Python predefiniti nella macchina virtuale per data science sono ambienti globali leggibili da tutti gli utenti. Tuttavia, solo gli amministratori possono scrivere/installare i pacchetti globali. Per installare il pacchetto nell'ambiente globale, attivare la radice o l'ambiente py35 usando il comando `source activate` come amministratore o come utente con autorizzazione sudo. È quindi possibile usare un gestore pacchetti come `conda` o `pip` per installare o aggiornare i pacchetti. 

## <a name="r"></a>R

|    |           |
| ------------- | ------------- |
| Versioni di linguaggio supportate | Microsoft R Open 3.x (compatibile al 100% con CRAN-R)<br /> Microsoft R Server 9.x Developer Edition (una piattaforma R di livello enterprise scalabile)|
| Edizioni supportate della macchina virtuale per data science      | Linux, Windows     |
| Come viene configurato o installato sulla macchina virtuale per data science?  | Windows: `C:\Program Files\Microsoft\R Server\R_SERVER` <br />Linux: ` /usr/lib64/microsoft-r/3.3/lib64/R`    |
| Collegamenti a esempi      | Sono inclusi i Notebook di Jupyter di esempio per R     |
| Strumenti correlati nella macchina virtuale per data science      | SparkR, Python, Julia      |
### <a name="how-to-use--run-it"></a>Come usarlo o eseguirlo?    

**Windows**:

* Esecuzione nel prompt dei comandi

Aprire il prompt dei comandi e digitare `R`.

* Utilizzo in un IDE

Usare gli strumenti R Tools per Visual Studio (RTVS) installati in Visual Studio Community Edition o RStudio. Sono disponibili nel menu Start o come icona sul desktop. 

* Utilizzo in Jupyter

Aprire Jupyter e fare clic sul pulsante `New` per creare un nuovo notebook. A questo punto, è possibile scegliere il tipo di kernel come _R_ per usare il kernel Jupyter R (IRKernel). 

* Installazione di pacchetti R

R è installato nella macchina virtuale per data science in un ambiente globale leggibile da tutti gli utenti. Tuttavia, solo gli amministratori possono scrivere/installare i pacchetti globali. Per poter installare il pacchetto nell'ambiente globale, eseguire R usando uno dei metodi precedenti. È quindi possibile usare il gestore pacchetti di R come `install.packages()` o per installare o aggiornare i pacchetti. 

**Linux**:

* Esecuzione nel terminale

Aprire il terminale ed eseguire `R`.  

* Utilizzo in un IDE

Usare RStudio installato nella macchina virtuale per data science di Linux.  

* Utilizzo in Jupyter

Aprire Jupyter e fare clic sul pulsante `New` per creare un nuovo notebook. A questo punto, è possibile scegliere il tipo di kernel come _R_ per usare il kernel Jupyter R (IRKernel). 

* Installazione di pacchetti R

R è installato nella macchina virtuale per data science in un ambiente globale leggibile da tutti gli utenti. Tuttavia, solo gli amministratori possono scrivere/installare i pacchetti globali. Per poter installare il pacchetto nell'ambiente globale, eseguire R usando uno dei metodi precedenti. È quindi possibile usare il gestore pacchetti di R come `install.packages()` o per installare o aggiornare i pacchetti. 


## <a name="julia"></a>Julia

|    |           |
| ------------- | ------------- |
| Versioni di linguaggio supportate | 0,5 |
| Edizioni supportate della macchina virtuale per data science      | Linux, Windows     |
| Come viene configurato o installato sulla macchina virtuale per data science?  | Windows: installato in `C:\JuliaPro-VERSION`<br /> Linux: installato in `/opt/JuliaPro-VERSION`    |
| Collegamenti a esempi      | Sono inclusi i Notebook di Jupyter di esempio per Julia     |
| Strumenti correlati nella macchina virtuale per data science      | Python, R      |
### <a name="how-to-use--run-it"></a>Come usarlo o eseguirlo?    

**Windows**:

* Esecuzione nel prompt dei comandi

Aprire il prompt dei comandi e digitare `julia`. 
* Utilizzo in un IDE

Usare `Juno`, l'IDE di Julia installato nella macchina virtuale per data science e disponibile come collegamento sul desktop.

* Utilizzo in Jupyter

Aprire Jupyter e fare clic sul pulsante `New` per creare un nuovo notebook. A questo punto, è possibile scegliere il tipo di kernel come `Julia VERSION` 

* Installazione di pacchetti Julia

La posizione predefinita di Julia è un ambiente globale leggibile da tutti gli utenti. Tuttavia, solo gli amministratori possono scrivere/installare i pacchetti globali. Per poter installare il pacchetto nell'ambiente globale, eseguire Julia usando uno dei metodi precedenti. È quindi possibile usare i comandi del gestore pacchetti di Julia come `Pkg.add()` per installare o aggiornare i pacchetti. 


**Linux**:
* Esecuzione nel terminale.

Aprire il terminale ed eseguire `julia`. 
* Utilizzo in un IDE

Usare `Juno`, l'IDE di Julia installato nella macchina virtuale per data science e disponibile come collegamento sul desktop all'applicazione.

* Utilizzo in Jupyter

Aprire Jupyter e fare clic sul pulsante `New` per creare un nuovo notebook. A questo punto, è possibile scegliere il tipo di kernel come `Julia VERSION` 

* Installazione di pacchetti Julia

La posizione predefinita di Julia è un ambiente globale leggibile da tutti gli utenti. Tuttavia, solo gli amministratori possono scrivere/installare i pacchetti globali. Per poter installare il pacchetto nell'ambiente globale, eseguire Julia usando uno dei metodi precedenti. È quindi possibile usare i comandi del gestore pacchetti di Julia come `Pkg.add()` per installare o aggiornare i pacchetti. 

## <a name="other-languages"></a>Altri linguaggi

**C#**: disponibile in Windows e accessibile tramite Visual Studio Community Edition o in un `Developer Command Prompt for Visual Studio` in cui è possibile eseguire il comando `csc`. 

**Java**: OpenJDK è disponibile nelle versioni Linux e Windows della macchina virtuale per data science e impostato nel percorso. Per usare Java è possibile digitare il comando `javac` o `java` nel prompt dei comandi di Windows o nella shell Bash in Linux. 

**node.js**: node.js è disponibile nelle versioni Linux e Windows della macchina virtuale per data science e impostato nel percorso. Per accedere a node.js è possibile digitare il comando `node` o `npm` nel prompt dei comandi di Windows o nella shell Bash in Linux. In Windows, sono installati gli strumenti di node.js per l'estensione di Visual Studio per fornire un IDE con interfaccia grafica nel quale sviluppare l'applicazione node.js. 

**F#**: disponibile in Windows e accessibile tramite Visual Studio Community Edition o in un `Developer Command Prompt for Visual Studio` in cui è possibile eseguire il comando `fsc`. 


