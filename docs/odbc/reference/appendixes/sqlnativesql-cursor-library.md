---
title: SQLNativeSql (bibliothèque de curseurs) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5b87f64963e7b0ad45fbec33e410165cd0c9723
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656708"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (bibliothèque de curseurs)
> [!IMPORTANT]  
>  Cette fonctionnalité sera supprimée dans une future version de Windows. Évitez d’utiliser cette fonctionnalité dans tout nouveau développement et prévoyez de modifier les applications qui utilisent actuellement cette fonctionnalité. Microsoft recommande d’utiliser les fonctionnalités de curseur du pilote.  
  
 Cette rubrique explique comment utiliser le **SQLNativeSql** fonction dans la bibliothèque de curseurs. Pour des informations générales sur **SQLNativeSql**, consultez [sqlnativesql, fonction](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Si le pilote prend en charge cette fonction, la bibliothèque de curseurs appelle **SQLNativeSql** dans le pilote et le transmet l’instruction SQL. Pour la mise à jour positionnée, suppression positionnée, et **Sélectionnez pour mettre à jour** instructions, la bibliothèque de curseurs modifie l’instruction avant de le transmettre au pilote.  
  
> [!NOTE]  
>  La bibliothèque de curseurs retourne incorrectement SQLSTATE 34000 (nom de curseur non valide) si le nom du curseur n’est pas valide dans une mise à jour positionnée ou une instruction delete qui est passée dans le *InStatementText* argument de **SQLNativeSql** . **SQLNativeSql** n’est pas conçue pour retourner des erreurs de syntaxe, qui sont retournées uniquement lors de la préparation ou de l’exécution.
