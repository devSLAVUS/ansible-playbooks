# 🚀 Ansible Playbook for Infrastructure Setup

Этот Ansible-плейбук автоматизирует развертывание и настройку инфраструктуры, включая:

- **Настройку NAT** на `vm1` (маршрутизатор).
- **Добавление маршрута** на `vm2` и `vm3` для выхода в интернет через `vm1`.
- **Настройку сети** с Netplan.
- **Установку Docker и других пакетов**.
- **Использование Jump Host (`vm1`) для подключения к `vm2` и `vm3`**.

---

## 📂 Структура проекта

- `ansible/`
  - `inventory/`
    - `hosts.yml` – Инвентарь (список серверов)
    - `group_vars/`
      - `all.yml` – Общие переменные
      - `router.yml` – Переменные для маршрутизатора
      - `workers.yml` – Переменные для worker-нод
  - `playbooks/`
    - `nat_setup.yml` – Настройка NAT
    - `gateway_setup.yml` – Настройка маршрутизации
    - `base_setup.yml` – Установка базовых пакетов (Docker и т. д.)
  - `roles/`
    - `nat/`
      - `tasks/main.yml` – Роль NAT
    - `gateway/`
      - `tasks/main.yml` – Роль для маршрутизации
    - `base/`
      - `tasks/main.yml` – Роль для базовой настройки серверов
  - `ansible.cfg` – Конфигурация Ansible
  - `README.md` – Документация

---

## 🔧 **Настройка переменных**
Перед запуском плейбуков убедитесь, что заданы переменные окружения:

```bash
export ANSIBLE_JUMP_HOST="your-public-ip"
export ANSIBLE_PRIVATE_KEY="/path/to/private_key.pem"