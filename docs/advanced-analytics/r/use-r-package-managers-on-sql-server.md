---
title: Использование диспетчеров пакетов R
description: Используйте стандартные команды R, такие как install.packages, для добавления новых пакетов R в SQL Server 2016 R Services или службы машинного обучения SQL Server (в базе данных).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f6d828a7267ab2b4b1def17f9d1c6bf4a6018dc
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633615"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Используйте диспетчеры пакетов R для установки пакетов R на SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Вы можете использовать стандартные инструменты R для установки новых пакетов на экземпляре SQL Server 2016 или SQL Server 2017, если у компьютера открыт порт 80 и у вас есть права администратора.

> [!IMPORTANT] 
> Установите пакеты в библиотеке по умолчанию, связанной с текущим экземпляром. Никогда не устанавливайте пакеты в каталог пользователя.

В этой процедуре используется RGui, но можно использовать RTerm или любую другую программу командной строки R, поддерживающую повышенный уровень доступа.

## <a name="install-a-package-using-rgui"></a>Установка пакета с помощью RGui

1. [Определите расположение библиотеки экземпляров](../package-management/r-package-information.md). Перейдите к папке, в которую были установлены инструменты R. Например, путь по умолчанию для экземпляра SQL Server 2017 выглядит следующим образом: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. Щелкните правой кнопкой мыши файл RGui.exe и выберите команду **Запуск от имени администратора**. Если у вас нет необходимых разрешений, обратитесь к администратору базы данных и предоставьте список необходимых пакетов.

1. Если имя пакета известно, в командной строке можно ввести следующее: `install.packages("the_package-name")` Двойные кавычки обязательны для имени пакета.

1. При запросе указать зеркальный сайт выберите любой, удобный для вашего расположения.

Если целевой пакет зависит от дополнительных пакетов, установщик R автоматически скачает нужные зависимости и установит их.

Если у вас несколько экземпляров SQL Server, например параллельные экземпляры SQL Server 2016 R Services и Служб машинного обучения SQL Server, выполните установку отдельно для каждого экземпляра, если вы хотите использовать пакет в обоих контекстах. Пакеты не могут совместно использоваться разными экземплярами.

## <a name = "bkmk_offlineInstall"></a> Автономная установка с помощью средств R

Если сервер не имеет доступа к Интернету, необходимо выполнить дополнительные действия для подготовки пакетов. Для установки пакетов R на сервере без доступа к Интернету необходимо выполнить следующие действия:

+ Проанализируйте зависимости заранее.
+ Загрузите целевой пакет на компьютер с доступом к Интернету.
+ Загрузите все необходимые пакеты на один и тот же компьютер и разместите все пакеты в одном архиве.
+ Создайте ZIP-файл, если архив имеет другой формат.
+ Скопируйте архив пакета в расположение на сервере.
+ Установите целевой пакет, указав файл архива в качестве источника.

> [!IMPORTANT] 
>  Обязательно проанализируйте все зависимости и загрузите **все** необходимые пакеты **до** начала установки. Для этого процесса рекомендуется [miniCRAN](https://mran.microsoft.com/package/miniCRAN). Этот пакет R принимает список пакетов, которые необходимо установить, анализирует зависимости и получает все ZIP-файлы автоматически. Затем miniCRAN создает один репозиторий, который можно скопировать на серверный компьютер. Дополнительные сведения см. в разделе [Создание локального репозитория пакетов с помощью miniCRAN](create-a-local-package-repository-using-minicran.md)

В этой процедуре предполагается, что вы подготовили все необходимые пакеты в формате ZIP и готовы к их копированию на сервер.

1. Скопируйте ZIP-файл пакета или нескольких пакетов, полный репозиторий, содержащий все пакеты в формате ZIP, в расположение, к которому сервер может получить доступ.

2. Откройте папку на сервере, где установлены средства R для экземпляра. Например, если вы используете командную строку Windows в системе с SQL Server 2016 R Services, переключитесь на `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Щелкните правой кнопкой мыши файл RGui или RTerm и выберите команду **Запуск от имени администратора**.

4. Выполните команду R `install.packages` и укажите имя пакета или репозитория, а также расположение ZIP-файлов.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Эта команда извлекает пакет R `mynewpackage` из локального ZIP-архива (при условии что копия сохранена в каталоге `C:\Temp\Downloaded packages`) и устанавливает пакет на локальном компьютере. Если у пакета есть зависимости, установщик проверяет наличие существующих пакетов в библиотеке. Если вы создали репозиторий, включающий зависимости, установщик также установит необходимые пакеты.

    Если необходимые пакеты отсутствуют в библиотеке экземпляров и не найдены в ZIP-файлах, установка целевого пакета завершается сбоем.

## <a name="see-also"></a>См. также раздел

+ [Установка новых пакетов R](install-additional-r-packages-on-sql-server.md)
+ [Установка новых пакетов Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Руководства, примеры, решения](../tutorials/machine-learning-services-tutorials.md)
