---
title: Prise en charge de transaction | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be133079c1b6beffd484942eb9ae058c14dd5c1f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808937"
---
# <a name="transaction-support"></a>Prise en charge des transactions
Le degré de prise en charge des transactions est définie par le pilote. ODBC est conçue pour être implémentée sur une base de données utilisateur unique ou de bureau qui n’a pas besoin de gérer plusieurs mises à jour ses données. En outre, certaines bases de données qui prennent en charge les transactions faire donc uniquement pour les instructions de langage de Manipulation de données (DML) de SQL ; Il existe les restrictions ou la sémantique de transaction spéciales concernant l’utilisation du langage DDL (Data Definition) lorsqu’une transaction est active. Autrement dit, il peut être prise en charge de transaction pour plusieurs mises à jour simultanées tables mais ne pas pour modifier le nombre et la définition des tables lors d’une transaction.  
  
 Une application détermine si les transactions sont prises en charge, DDL peut être inclus dans une transaction, ainsi que tous les effets spéciaux de, notamment DDL dans une transaction, en appelant **SQLGetInfo** avec l’option SQL_TXN_CAPABLE. Pour plus d’informations, consultez le [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) description de fonction.  
  
 Si le pilote ne prend pas en charge les transactions, mais l’application a la possibilité (à l’aide d’une API autre que ODBC) pour verrouiller et déverrouiller des données, les applications peuvent atteindre prise en charge de la transaction par verrouillage et déverrouillage des enregistrements et les tables en fonction des besoins. Pour implémenter l’exemple de transfert de compte, l’application serait verrouiller les enregistrements pour les deux comptes, copiez les valeurs actuelles, le premier compte de débit, le deuxième compte de crédit et déverrouiller les enregistrements. En cas d’échec de toutes les étapes, l’application serait réinitialiser les comptes à l’aide de la copie.  
  
 Les sources de données même qui prennent en charge des transactions n’est peut-être pas en mesure de prendre en charge de plusieurs transactions à la fois dans un environnement particulier. Applications appellent **SQLGetInfo** avec l’option SQL_MULTIPLE_ACTIVE_TXN pour déterminer si une source de données peut prendre en charge les transactions actives simultanées sur plusieurs connexions dans le même environnement. Étant donné qu’une seule transaction par connexion, cela n’est plus intéressant pour les applications qui ont plusieurs connexions à la même source de données.
