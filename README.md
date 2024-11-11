# Тестовове задание на позицию Junior DevOps.

Необходимо развернуть микросервисное приложение в локальный кластер и поправить возможные в нём мисконфигурации.

## Статьи которые помогут решить задание

1. https://codersociety.com/blog/articles/helm-best-practices
2. https://habr.com/ru/articles/726636/
3. https://asankov.dev/blog/2022/05/15/demystifying-the-kubernetes-iceberg-part-1/
4. https://asankov.dev/blog/2022/05/22/demystifying-the-kubernetes-iceberg-part-2/

Ниже представленна инструкция как запустить тестовое, что бы проверить что ничего не поломалось.

## Зависимости

Docker, kubectl, helm, [k3d](https://k3d.io/v5.7.4/)

## Установка локального кластера

```bash
k3d cluster create devops-bs-test --image rancher/k3s:v1.27.10-k3s2
```

## Установка микросервисов в локальный кластер

```bash
helm upgrade -i --atomic --timeout 5m onlineboutique ./helm-chart
```

## Прокидывание порта до фронтенда

```bash
kubectl port-forward -n default svc/frontend 8080:80
```
Далее в браузере можно открыть приложение по localhost:8080