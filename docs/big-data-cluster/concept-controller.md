---
title: Что такое большие данные контроллера кластера SQL Server? | Документы Майкрософт
description: В этой статье описывается контроллер кластера SQL Server 2019 больших данных.
author: mihaelablendea
ms.author: mihaelab
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: abf8c174379ad444cd29b5115240ad7c404b2c4b
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221520"
---
# <a name="what-is-the-sql-server-big-data-clusters-controller"></a>Что такое контроллер кластеров SQL Server больших данных?

На контроллере размещены основную логику для развертывания и управления ими кластерам больших данных. Она отвечает за все взаимодействия с помощью Kubernetes, экземпляры SQL Server, которые являются частью кластера и другие компоненты, такие как HDFS и Spark. 

Служба контроллера предоставляет следующие основные функции:

- Управление жизненным циклом кластера: начальная загрузка кластера и удаление, обновление конфигураций
- Управление главным экземплярам SQL Server
- Управление пулами вычисления, хранения и данных
- Предоставляют средства мониторинга для наблюдения за состоянием кластера
- Предоставляют средства устранения неполадок для обнаружения и устранения неожиданных неполадок
- Управление безопасностью кластера: конечные точки защищенного кластера убедитесь, управлять пользователями и ролями, Настройка учетных данных для обмена данными внутри кластера
- Управлять рабочий процесс обновления, таким образом, чтобы они реализуются безопасно (недоступно в CTP 2.1)
- Управление высокий уровень доступности и аварийного восстановления для служб сведениями в кластере (недоступно в CTP 2.1)

## <a name="deploying-the-controller-service"></a>Развертывание службы контроллера

Контроллер развернут и размещенной в том же пространстве имен Kubernetes, где клиент хочет создать кластерам больших данных. Эта служба устанавливается администратором Kubernetes во время начальной загрузки кластера, с помощью служебной программы командной строки mssqlctl:

```bash
mssqlctl create cluster <name of your cluster>
```

Рабочий процесс занимались будет макета на основе Kubernetes полнофункциональные кластера больших данных SQL Server, включающий все компоненты, описанные в [Обзор](big-data-cluster-overview.md) статьи. Рабочего процесса начальной загрузки сначала создает службу контроллера, а после развертывания это службой контроллера будет координировать установку и настройку остальной части служб master, вычислений, данных и пулах носителей.

## <a name="managing-the-cluster-through-the-controller-service"></a>Управление кластером через службу контроллера
Вы можете управлять кластером исключительно через службу контроллера, с помощью `mssqlctl` API-интерфейсы или на портал администрирования кластера, который размещается в кластере. При развертывании дополнительных объектов Kubernetes как POD, содержащихся в одном пространстве имен, они не управляются и наблюдение за службой контроллера.

Контроллер и объекты Kubernetes (наборы с отслеживанием состояния, модулей, секреты и др.), созданные для работы с большими данными кластера размещаются в выделенном пространстве имен Kubernetes. Служба контроллера будет предоставлено разрешение, администратор кластера Kubernetes может управлять всеми ресурсами в этом пространстве имен.  Политики RBAC для этого сценария настраивается автоматически в рамках первоначального развертывания с помощью `mssqlctl`. 

### <a name="mssqlctl"></a>mssqlctl

`mssqlctl` создается это программа командной строки на языке Python, который позволяет администраторам кластера для начальной загрузки и управление кластерами больших данных с помощью REST API, предоставляемые службой контроллера.

### <a name="cluster-administration-portal"></a>Портал администрирования кластера

После выпуска службы контроллера приступить к работе, администратор кластера можно использовать портал администрирования кластера отслеживать ход выполнения развертывания, обнаружение и устранение неполадок со службами в кластере. 

## <a name="monitoring-and-troubleshooting-the-controller-service"></a>Мониторинг и устранение неполадок службы контроллера

Скоро...

## <a name="controller-service-security"></a>Контроллер службы безопасности
Весь обмен данными с контроллером службы проводится через REST API по протоколу HTTPS. Самозаверяющий сертификат автоматически создается автоматически во время начальной загрузки. 

Проверка подлинности, в конечную точку службы контроллера основана на имя пользователя и пароль. Эти учетные данные подготавливаются во время начальной загрузки кластера, с помощью входных данных для переменных среды `CONTROLLER_USERNAME` и `CONTROLLER_PASSWORD`.
```

> [!NOTE]
> You must provide a password that is in compliance with [SQL Server password complexity requirements](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## Next steps

To learn more about the SQL Server big data clusters, see the following overview:

- [What are SQL Server 2019 big data clusters?](big-data-cluster-overview.md)