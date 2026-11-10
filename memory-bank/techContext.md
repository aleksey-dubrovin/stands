# Technical Context: DevOps Hybrid Stand

## Стек технологий

### JavScript/TypeScript
- **VS Code + Cline** — IDE и автоматизация
- **Ollama** — локальные LLM модели
- **Podman/podman-compose** — контейнеризация (алиас `docker`)

### Python
- **Ansible** — автоматизация инфраструктуры
- **Qwen3.5-9b-deep:latest** — локальная модель для Act mode (Ollama)
- **DeepSeek-v4-flash** — облачная модель для Plan mode

### DevOps инструменты
- **GNS3/EVE-NG/PNETLab** — симуляция сетей
- **KVM/libvirt** — виртуализация с nested support
- **k3s/k3d** — оркестрация контейнеров
- **Jenkins/Argo CD** — CI/CD

### Модели LLM
| Модель | Использование | Стоимость/мес |
|--------|---------------|---------------|
| deepseek-v4-flash | планирование, KB | ~$0.90 |
| kimi-k2.7-code | ревью кода | ~$2.55 |
| claude-sonnet-5 | сложные задачи | ~$2.32 |
| baai/bge-m3-embedding | эмбеддинги KB | ~$0.09 |
| **Итого** | | **≈ $6/мес** |

## Окружение
### Железо (MAIBENBEN X16C)
- CPU: Ryzen 7 H 255
- ОЗУ: 32 ГБ
- GPU: RTX 5060 8 ГБ
- ОС: ALT Linux 11.4

### Требования к установке
- **Nested virtualization**: включить через `options kvm_amd nested=1`
- **Podman** — алиас для Docker
- **Ollama** — порт 11434, systemd-сервис
- **KVM/libvirt** — qemu-kvm, virt-manager

## Зависимости и версии
- **Podman**: latest LTS (алиас docker)
- **Ollama**: qwen3.5-9b-deep:latest
- **KVM**: libvirt, libvirt-kvm, qemu-kvm
- **k3s**: в KVM (1 server + 2 agent ВМ)

## Ограничения
- ОЗУ ~6–8 ГБ для k3s в KVM (1 server + 2 agents по 2 ГБ)
- Nested virtualization обязательна для GNS3/EVE-NG
- Fallback на облачные модели при исчерпании локального контекста
