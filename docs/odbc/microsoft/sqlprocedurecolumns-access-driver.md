---
title: SQLProcedureColumns (pilote Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a438823d1aa71eecb25c4935026c1b43e45842d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812697"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (pilote Access)
> [!NOTE]  
>  Cette rubrique fournit des informations d’accès spécifiques au pilote. Pour obtenir des informations générales sur cette fonction, consultez la rubrique appropriée sous [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Les développeurs d’applications doivent se présenter pour les colonnes définies par le pilote en commençant à la fin du jeu de résultats et en procédant par ordre décroissant.  
  
|colonne|Commentaires|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT ou SQL_RESULT_COL|  
|ORDINAL|Il s’agit d’une colonne spécifiques au pilote qui est retournée à la fin du jeu de résultats. Le type SQL de la colonne est un entier.|
