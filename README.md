# 🏔️ CachyOS Hyprland Rice

Um setup limpo, produtivo e altamente customizado rodando **Hyprland** no **CachyOS** (Arch Linux).

![OS](https://img.shields.io/badge/OS-CachyOS-green?style=for-the-badge&logo=archlinux)
![WM](https://img.shields.io/badge/WM-Hyprland-blue?style=for-the-badge&logo=hyprland)
![Shell](https://img.shields.io/badge/Shell-Fish-orange?style=for-the-badge&logo=fish)

---

## 🛠️ Componentes do Sistema

* **OS:** CachyOS (Linux)
* **Compositor:** Hyprland
* **Barra / Dock:** Noctalia
* **Idle Daemon:** Hypridle
* **Lockscreen:** Hyprlock
* **Terminal:** Kitty
* **Shell:** Fish Shell

---

## 🔧 Destaques & Correções Técnicas

### ⚡ Fix de Congelamento da Dock/Barra (DPMS / Idle)
Em sistemas com GPUs como a Intel Iris Xe, o gerenciamento de energia da tela (`DPMS off`) pode fazer com que interfaces Wayland como o **Noctalia** percam a sincronização de renderização ao acordar o monitor.

Este repositório inclui um mecanismo de autorecovery integrado no `hypridle.conf` que força o redesenho da interface via `on-resume`:

```ini
listener {
    timeout = 660 # 11 minutos
    on-timeout = hyprctl dispatch dpms off
    on-resume = hyprctl dispatch dpms on && (noctalia-cli reload || nohup noctalia >/dev/null 2>&1 &)
}
