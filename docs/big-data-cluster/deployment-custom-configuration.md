---
title: Настройка развертывания
titleSuffix: SQL Server big data clusters
description: Дополнительные сведения о настройке развертывания в кластере больших данных с файлами конфигурации.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7dd774d390587d0c2c0248ab9b419ad40f8f212b
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759171"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Настройка параметров развертывания для больших данных кластеров

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Чтобы настроить файл конфигурации развертывания кластера, можно использовать любой редактор формат json, например VSCode. Для использования в сценариях эти изменения в целях автоматизации, мы предоставляем **раздел конфигурации кластера mssqlctl** команды. В этой статье объясняется, как настраивать развертывание кластера больших данных, изменяя файлы конфигурации развертывания. Содержит примеры по изменению конфигурации для разных сценариев. Дополнительные сведения об использовании файлов конфигурации в развертываниях см. в разделе [руководство по развертыванию](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>предварительные требования

- [Установка mssqlctl](deploy-install-mssqlctl.md).

- В каждом из примеров в этом разделе предполагается, что вы создали копию одного из файлов стандартной конфигурации. Дополнительные сведения см. в разделе [создать пользовательский файл конфигурации](deployment-guidance.md#customconfig). Например, следующая команда создает **custom.json** файла на основе стандартной **aks-dev-test.json** конфигурации:

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

## <a id="clustername"></a> Изменение имени кластера

Имя кластера — это имя кластера больших данных и пространств имен Kubernetes, который будет создан при развертывании. Он указан в следующей части файла конфигурации развертывания:

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

Следующая команда отправляет пару "ключ значение" для **--json-значения** параметр, чтобы изменить имя кластера больших данных, чтобы **тестового кластера**:

```bash
mssqlctl cluster config section set -f custom.json -j ".metadata.name=test-cluster"
```

> [!IMPORTANT]
> Имя кластера должно быть только буквенно цифровые символы в нижнем регистре, не должно быть пробелов. Все артефакты Kubernetes (контейнеры, модулей, вертикальное наборов, службы) для кластера будет создан в пространство имен с тем же именем, что и кластер указанное имя.

## <a id="ports"></a> Порты обновления конечной точки

Конечные точки определяются для плоскости управления, а также отдельные пулы. В следующей части в файле конфигурации показаны определения конечной точки для плоскости управления.

```json
"endpoints": [
    {
        "name": "Controller",
        "serviceType": "LoadBalancer",
        "port": 30080
    },
    {
        "name": "ServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30777
    },
    {
        "name": "AppServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30778
    },
    {
        "name": "Knox",
        "serviceType": "LoadBalancer",
        "port": 30443
    }
]
```

В следующем примере используется встроенный JSON, чтобы изменить порт для **контроллера** конечной точки:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.controlPlane.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> Настройка пула реплик

Характеристики каждого пула, например в пул носителей, определяется в файле конфигурации. Например следующий фрагмент показано определение пула хранения:

```json
"pools": [
    {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
            "storage": {
                "usePersistentVolume": true,
                "className": "managed-premium",
                "accessMode": "ReadWriteOnce",
                "size": "10Gi"
            }
        }
    }
]
```

Число экземпляров в пуле можно настроить, изменив **реплик** значение для каждого пула. В следующем примере используется встроенный JSON, чтобы изменить эти значения для хранения данных и пулов для `10` и `4` соответственно:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4'
```

> [!IMPORTANT]
> В этом выпуске нельзя изменить количество экземпляров в пуле вычислительных.

## <a id="storage"></a> Настройка хранилища

Можно также изменить класс хранения и характеристики, используемые для каждого пула. В следующем примере присваивается класс пользовательского хранилища в пул носителей:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec={""replicas"": 2,""storage"": {""className"": ""newStorageClass"",""size"": ""20Gi"",""accessMode"": ""ReadWriteOnce"",""usePersistentVolume"": true},""type"": ""Storage""}"
```

В следующем примере обновляется только размер пула в `32Gi`:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.size=32Gi"
```

В следующем примере обновляется размер всех пулов `32Gi`:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type[*])].spec.storage.size=32Gi"
```

> [!NOTE]
> Файл конфигурации на основе **kubeadm-dev-test.json** не содержит определения хранения для каждого пула, но это можно добавить вручную при необходимости.

Дополнительные сведения о конфигурации хранилища, см. в разделе [сохранение данных с SQL Server, большие данные кластера в Kubernetes](concept-data-persistence.md).

## <a id="podplacement"></a> Настройка размещения pod с метками для Kubernetes

Вы можете управлять pod размещение на узлах Kubernetes, определенные ресурсы с учетом различных типов требований рабочей нагрузки. Например может потребоваться убедиться, модулей POD пула хранения будут размещены на узлах с большим объемом хранилища, или главным экземплярам SQL Server размещаются на узлах, которые имеют более высокая загрузка ЦП и памяти. В этом случае следует построить разнородных кластера Kubernetes с различными типами оборудования, а затем [назначить метки узла](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) соответствующим образом. Во время развертывания кластера больших данных можно указать одинаковые заголовки на уровне пула в файле конфигурации развертывания кластера. Затем Kubernetes позаботится о привязывая POD, содержащихся на узлах, которые соответствуют указанной метки.

В следующем примере показано, как изменить пользовательский файл конфигурации для включения параметра метка узла для главного экземпляра SQL Server. Следует отметить, что не *nodeLabel* ключа в встроенных конфигурациях, поэтому необходимо либо изменить пользовательский файл конфигурации вручную, или создать файл исправления и применить его к настраиваемый файл конфигурации.

Создайте файл с именем **patch.json** в текущем каталоге со следующим содержимым:

```json
{
  "patch": [
     {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
      "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
mssqlctl cluster config section set -f custom.json -p ./patch.json
```

## <a id="jsonpatch"></a> Файлы исправления JSON

Файлы исправления JSON за один раз настроить несколько параметров. Дополнительные сведения об исправлениях JSON см. в разделе [исправления JSON в Python](https://github.com/stefankoegl/python-json-patch) и [JSONPath Online вычислителя](https://jsonpath.com/).

Следующие **patch.json** файл выполняет следующие изменения:

- Обновляет порт одной конечной точки.
- Обновляет все конечные точки (**порт** и **serviceType**).
- Обновляет хранилище плоскости управления.
- Обновляет имя класса хранения в хранилище плоскости управления.
- Обновления пула хранения, включая реплики (пул носителей).
- Обновляет параметры Spark для конкретного пула (пул носителей).

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port",
      "value": 30000
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.endpoints",
      "value": [
        {
          "serviceType": "LoadBalancer",
          "port": 30001,
          "name": "Controller"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "ServiceProxy"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "AppServiceProxy"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30443,
            "name": "Knox"
        }
      ]
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage",
      "value": {
        "usePersistentVolume":true,
        "accessMode":"ReadWriteMany",
        "className":"managed-premium",
        "size":"10Gi"
      }
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage.className",
      "value": "default"
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "replicas": 2,
        "type": "Storage",
        "storage": {
          "usePersistentVolume": true,
          "accessMode": "ReadWriteOnce",
          "className": "managed-premium",
          "size": "10Gi"
        }
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].hadoop.spark",
      "value": {
        "driverMemory": "2g",
        "driverCores": 1,
        "executorInstances": 3,
        "executorCores": 1,
        "executorMemory": "1536m"
      }
    }
  ]
}
```

> [!TIP]
> Дополнительные сведения о структуре и параметры для изменения файла конфигурации развертывания см. в разделе [ссылка на файл конфигурации развертывания для больших данных кластеров](reference-deployment-config.md).

Используйте **набор раздел конфигурации кластера mssqlctl** для применения изменений в файл исправления JSON. В следующем примере применяется **patch.json** файл в файл конфигурации развертывания целевой **custom.json**.

```bash
mssqlctl cluster config section set -f custom.json -p ./patch.json
```

## <a name="next-steps"></a>Следующие шаги

Дополнительные сведения об использовании файлов конфигурации при развертывании кластера больших данных, см. в разделе [развертывание больших данных в SQL Server кластеров Kubernetes](deployment-guidance.md#configfile).