# Выполнено ДЗ № 1

 - [x] Основное ДЗ
 - [x] Задание со *

## В процессе сделано:
 - Настроен локальный K8S кластер с помощью утилиты Minikube
 - Проведено исследование механизма запуска подов в неймсейпсе kube-system
 - Написаны Dockerfile в соответствии с заданиями, собраны образы и загружены на Docker Hub:
 https://hub.docker.com/repository/docker/soapj/otus.homework1.kubernetes-intro.web
 https://hub.docker.com/repository/docker/soapj/otus.homework1.kubernetes-intro.frontend

## Основное задание:
 - Запуском kube-apiserver/kube-controller-manager/kube-scheduler-minikube подов в Minikube управляет kubelet, который в свою очередь запускается, как systemd демон на VM, статические манифесты этих компонент лежат в /etc/kubernetes/manifests/
 - coredns задеплоен в кластер, как реплика set, с помощью механизма deployment, поэтому при удалении подов scheduler поднимает их в соответствии с параметрами заданными в манифестах
 - kube-proxy задеплоен в кластер как daemon set, scheduler поднимает его в соответствии с параметрами заданными в манифесте

### Hipster Shop | Задание со ⭐
Для запуска приложения на базе имаджа из задания не хватало переменных окружения:
https://github.com/GoogleCloudPlatform/microservices-demo/blob/master/kubernetes-manifests/frontend.yaml#L52
Необходимые переменные добавлены в манифест frontend-pod-healthy.yaml

## Как запустить проект:
 - Поднять локальный кластер командой:
 ```minikube start```
 - Задеплоить под web в кластер, для этого в директории kubernetes-intro запустить команду:
 ```kubectl apply -f web-pod.yaml```

## Как проверить работоспособность:
 - Пробросить порт приложения себе на локальную машину:
 ```kubectl port-forward --address 0.0.0.0 pod/web 8000:8000```
 - Перейти по ссылке http://localhost:8080

## PR checklist:
 - [x] Выставлен label с темой домашнего задания
