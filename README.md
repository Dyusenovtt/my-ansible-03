# Домашнее задание к занятию 3 «Использование Ansible»

Репозиторий содержит инфраструктурный код (Ansible playbook) для автоматизированного развертывания системы сбора, хранения и визуализации логов. Инфраструктура разворачивается на виртуальных машинах в Yandex Cloud.
С использованием Terraform

## Описание проекта

Плейбук `site.yml` состоит из трех основных частей (plays) и настраивает следующие компоненты:
1. **Clickhouse** (СУБД для аналитики и логов) — устанавливается из официальных `.rpm` пакетов на ОС AlmaLinux. Создается база данных `logs`.
2. **Vector** (Агент маршрутизации логов) — скачивается в виде архива и настраивается через шаблонизатор Jinja2 на ОС Ubuntu.
3. **Lighthouse** (Веб-интерфейс для Clickhouse) — скачивается напрямую из репозитория. Настраивается веб-сервер Nginx для отдачи статических файлов интерфейса на ОС Ubuntu.

## Структура репозитория
* `site.yml` — основной плейбук с задачами.
* `inventory/prod.yml` — файл инвентаризации с IP-адресами серверов Yandex Cloud.
* `templates/` — директория с jinja2-шаблонами (конфигурации для Nginx и Vector).
* `terraform/` — код для поднятия серверов и настройки `cloud-init` (передача SSH-ключей).

## Параметры и запуск плейбука

Параметр `--check` позволяет проверить доступность хостов и синтаксис задач без реального внесения изменений в систему.
```bash
ansible-playbook -i inventory/prod.yml site.yml --check
```
## Входе синхронизации виртуальных машин myterra и myansible несколько раз менялись публичные IP адреса
<img width="974" height="618" alt="image" src="https://github.com/user-attachments/assets/79217826-f91b-4644-b139-672de85c4ae5" />
<img width="974" height="915" alt="image" src="https://github.com/user-attachments/assets/a232b295-2b88-4700-bd04-1bc28a630ae9" />
<img width="974" height="464" alt="image" src="https://github.com/user-attachments/assets/9fff6111-a2da-4259-b8f3-a54a5c2fb9c5" />
<img width="974" height="594" alt="image" src="https://github.com/user-attachments/assets/836aa1a3-edbd-463a-a38e-24f352a505b7" />
<img width="974" height="304" alt="image" src="https://github.com/user-attachments/assets/88a63a67-8130-4e1c-b086-557ea6baf3e7" />
<img width="974" height="584" alt="image" src="https://github.com/user-attachments/assets/a940bad7-1e6c-4d3e-b630-2449a403bb2c" />
<img width="974" height="906" alt="image" src="https://github.com/user-attachments/assets/e112d56f-010f-4d64-90d9-a39d92e03c1c" />
<img width="974" height="754" alt="image" src="https://github.com/user-attachments/assets/ea8029f7-af75-40ce-a63a-546c3a16528a" />
<img width="974" height="703" alt="image" src="https://github.com/user-attachments/assets/15ea4742-900d-4bd7-a5a9-ce7eb39305c7" />
<img width="974" height="567" alt="image" src="https://github.com/user-attachments/assets/ae054595-7c4b-41f1-b660-014fe2dd0622" />

