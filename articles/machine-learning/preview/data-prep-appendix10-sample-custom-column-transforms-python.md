---
title: Codice Python di esempio per la derivazione di nuove colonne nella preparazione dati di Azure Machine Learning | Microsoft Docs
description: Questo documento fornisce esempi di codice Python per la creazione di nuove colonne nella preparazione dati di Azure Machine Learning.
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.custom: 
ms.devlang: 
ms.topic: article
ms.date: 09/12/2017
ms.openlocfilehash: e576d44a854159054d4f7886fe7859ae34875c8f
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2018
---
# <a name="sample-of-custom-column-transforms-python"></a>Esempio di trasformazioni di colonna personalizzate (Python) 
Il nome di questa trasformazione nel menu è **Add Column (Script)** (Aggiungi colonna - Script).

Prima di leggere questa appendice, leggere la [panoramica dell'estendibilità di Python](data-prep-python-extensibility-overview.md).

## <a name="test-equivalence-and-replace-values"></a>Testare l'equivalenza e sostituire i valori 
Se il valore in Col1 è minore di 4, la nuova colonna deve contenere il valore 1. Se il valore in Col1 è maggiore di 4, la nuova colonna contiene il valore 2. 

```python
    1 if row["Col1"] < 4 else 2
```
## <a name="current-date-and-time"></a>Data e ora corrente 

```python
    datetime.datetime.now()
```
## <a name="typecasting"></a>Cast del tipo 
```python
    float(row["Col1"]) / float(row["Col2"] - 1)
```
## <a name="evaluate-for-nullness"></a>Valutare la presenza di null 
Se Col1 contiene un valore Null, contrassegnare la nuova colonna come **non valida**. In caso contrario, contrassegnarla come **valida**. 

```python
    'Bad' if pd.isnull(row["Col1"]) else 'Good'
```
## <a name="new-computed-column"></a>Nuova colonna calcolata 
```python
    np.log(row["Col1"])
```
## <a name="epoch-computation"></a>Calcolo di periodo 
Numero di secondi trascorsi dal periodo Unix (presupponendo che Col1 sia già una data): 
```python
    row["Col1"] - datetime.datetime.utcfromtimestamp(0)).total_seconds()
```

## <a name="hash-a-column-value-into-a-new-column"></a>Hash di un valore di colonna in una nuova colonna
```python
    import hashlib
    hash(row["MyColumnToHashCol1"])

```




