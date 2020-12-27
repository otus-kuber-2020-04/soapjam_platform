# Выполнено ДЗ № 2
 - [x] Основное ДЗ
 - [x] Задание со *
 - [x] Задание с **

## В процессе сделано:
 - Настроен локальный K8S кластер с помощью утилиты kind
 - Проведено исследование механизма работы контроллеров: ReplicaSet, Deployment, DaemonSet
 - Проведен тест Probes механизма в рамках деплоймента сервиса frontend

## Основное задание:
 - ReplicaSet контроллер не умеет рестартовать существующие поды при обновлении шаблона, поэтому при изменении докер имаджа в манифесте и его применении старые поды остались жить, ReplicaSet контролирует количество подов опираясь на лейблы


### Deployment задание со ⭐
 - Аналог blue-green: maxSurge:3 and maxUnavailable:0
 - Аналог reverse rolling update: maxSurge:0 and maxUnavailable:1
 - Оба манифеста к заданию внутри PR

### DaemonSet задание со ⭐
 - DaemonSet манифест для установки Node Exporter взят из оффициального репозитория:
 https://github.com/prometheus-operator/kube-prometheus/blob/master/manifests/node-exporter-daemonset.yaml
 - Для установки Node Exporter с помощью приложенного манифеста также нужен service account, который можно создать с помощью манифеста по ссылке ниже, а также создать неймспейс monitoring с помощью команды: ```kubectl create ns monitoring```:
 https://github.com/prometheus-operator/kube-prometheus/blob/master/manifests/node-exporter-serviceAccount.yaml

### DaemonSet задание со ⭐⭐
 - В манифесте для установки Node Exporter скопированном из оффициацльного репозитория есть настройка:
 ```tolerations:
    - operator: Exists```
 Эта настройка является особым случаям использования механизма tollerations, который возволит применить манифест на всех нодах в обход всех ограничений. Разрешение запуска подов на мастер нодах также может быть достигнуто с помощью следующей настройки:
 ```tolerations:
    - key: node-role.kubernetes.io/master
      effect: NoSchedule```

## Как запустить проект:
 - Поднять локальный кластер командой:
 ```kind create cluster --config kubernetes-controllers/kind-config.yaml```
 - Команды для создания нужных RS & Deployments:
 ```kubectl apply -f <manifest_name>```
 - Команды для создания DaemonSet с Node Exporter:
 ```kubectl create ns monitoring```
 ```kubectl apply -f node-exporter-serviceAccount.yaml```
 ```kubectl apply -f node-exporter-daemonset.yaml```

## Как проверить работоспособность:
 - Для проверки доступности метрик с пода воспользоваться командой:
 ```kubectl port-forward <pod_name> -n monitoring 9100:9100```

## PR checklist:
 - [x] Выставлен label с темой домашнего задания
