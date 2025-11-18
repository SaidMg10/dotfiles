# Dotfiles – Setup & Explanation

Este documento resume únicamente **los requisitos técnicos**, **las versiones necesarias** y **las notas importantes** sobre los cambios realizados en mis configuraciones (dotfiles), especialmente después de actualizar Neovim, LazyVim, Catppuccin, mini.nvim y Copilot.

No incluye detalles personales ni procesos de formateo.

---

# ✅ Requisitos técnicos

## Neovim

- **Versión mínima:** `Neovim >= 0.11.2`
- LazyVim dejó de funcionar correctamente en versiones anteriores.
- Algunas integraciones requieren ahora la API moderna de Neovim.

### Cambios relevantes

- Eliminados módulos obsoletos de Catppuccin como:
  - `catppuccin.groups.integrations.bufferline`

- Sustituidos por la integración nueva:

  ```lua
  integrations = {
    bufferline = true,
  }
  ```

- Actualizaciones necesarias para mini.nvim (repos cambiaron a `nvim-mini/…`).

---

## Node.js

- **Versión mínima requerida por Copilot.nvim:** `Node >= 22`
- Error antes del upgrade:

  ```
  Node.js version 22 or newer required but found 20.x
  ```

- Solución aplicada: actualización mediante `nvm`.

---

## mini.nvim / mini.files / mini.icons

- Los repos antiguos quedaron obsoletos.
- Cambios necesarios:
  - De: `echasnovski/mini.files`
  - A: `nvim-mini/mini.files`

Este cambio afecta configuraciones que usen LazyVim.

---

## Catppuccin

### Cambios importantes

- Se removió el módulo viejo de bufferline:

  ```lua
  require("catppuccin.groups.integrations.bufferline").get()
  ```

- Ahora se usa únicamente:

  ```lua
  integrations = { bufferline = true }
  ```

### Tema + transparencia

- Se mantiene configuración de fondo transparente:

  ```lua
  transparent_background = true
  ```

- Se fuerzan highlights en floating windows:

  ```lua
  vim.api.nvim_set_hl(0, "NormalFloat", { bg = "NONE" })
  vim.api.nvim_set_hl(0, "FloatBorder", { fg = "#89b4fa", bg = "NONE" })
  ```

---

# ⚙️ Instalación con Stow

```bash
stow --target ~/.config
```

Cada carpeta del repo debe reflejar la estructura exacta que va en:

- `~/.config/...`
- o `$HOME/...`

Ejemplo:

```
dotfiles/nvim/.config/nvim/init.lua
→ ~/.config/nvim/init.lua
```

---

# 🍺 Homebrew – respaldo y restauración

### Generar lista de paquetes:

```bash
brew leaves > leaves.txt
```

### Instalar en una máquina nueva:

```bash
xargs brew install < leaves.txt
```

---

# 📌 Resumen de requisitos mínimos (2025)

| Herramienta | Versión mínima                             |
| ----------- | ------------------------------------------ |
| Neovim      | 0.11.2                                     |
| LazyVim     | Última versión estable (requiere 0.11+)    |
| Node        | 22+ (Copilot)                              |
| mini.nvim   | Repos nuevos `nvim-mini/…`                 |
| Catppuccin  | Última versión sin integraciones obsoletas |

#
