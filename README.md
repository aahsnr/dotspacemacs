# README
## Keybindings
Based on the provided Spacemacs configuration, here is a breakdown of the default keybindings for the enabled layers, formatted in Markdown. This configuration uses the `vim` editing style, so the primary leader key is `SPC`. The major-mode leader key, which is a shortcut for `SPC m`, is `,`.

### General Keybindings

Spacemacs provides a discoverable key binding system. Pressing `SPC` will open a `which-key` buffer that lists available commands. You can search for specific key bindings by pressing `SPC ?`.

### Ivy Layer

Ivy is a powerful completion framework. When a command prompts for input in the minibuffer, Ivy takes over to provide a list of candidates.

| Keybinding | Description |
|---|---|
| `RET` | Call the default action on the current candidate. |
| `M-RET` | Same as `RET` but doesn't close the completion minibuffer. |
| `C-RET` | When completing file names, selects the current directory and starts a new completion session there. |
| `C-SPC` | Preview the file under the point without leaving Ivy. |
| `C-o` or `M-SPC` | Enter the transient state for more actions. |

### Git Layer

Spacemacs uses `magit` for Git integration.

| Keybinding | Description |
|---|---|
| `SPC g s` | Open the Magit status window. |
| `SPC g m` | Open the Magit dispatch popup. |
| `SPC g /` | Search for text in the project using `git grep`. |
| `SPC g b` | Open a Magit blame for the current file. |
| `SPC g f f` | View a file at a specific branch or commit. |
| `SPC g f l` | View the commits log for the current file. |
| `SPC g t` | Launch the git time machine. |

### Version Control Layer

This layer provides generic version control commands.

| Keybinding | Description |
|---|---|
| `SPC g .` | Open the version control transient-state. |
| `SPC g o` | Open the current file on the remote forge (e.g., GitHub). |
| `SPC g v =` | Open a hunk under the point in a diff buffer. |
| `SPC g v g` | Visually annotate the current file (blame). |

### Treemacs Layer

Treemacs provides a file and project explorer sidebar.

| Keybinding | Description |
|---|---|
| `SPC f t` or `SPC p t` | Toggle the Treemacs buffer. |
| `?` | In the Treemacs buffer, show the help menu with all keybindings. |
| `RET` | Open the selected file or directory. |
| `g` | Refresh the Treemacs view. |
| `TAB` | Expand or collapse a directory. |

### Multiple Cursors Layer

This layer enables editing with multiple cursors. The default backend is `evil-mc`.

| Keybinding | Description |
|---|---|
| `g r j` | Create a new cursor on the line below. |
| `g r k` | Create a new cursor on the line above. |
| `g r m` | Create cursors on all matches of the symbol under the cursor or selection. |
| `g r I` | Create cursors on all selected lines. |
| `M-n` | Create and go to the next cursor. |
| `M-p` | Create and go to the previous cursor. |

### Org Layer

This layer provides extensive support for Org mode. Many keybindings are available under the major-mode leader key (`,`).

| Keybinding | Description |
|---|---|
| `SPC a o` | Access Org agenda views. |
| `SPC m` (`,`) | Major-mode leader key for Org-specific commands. |
| `, a` | `org-agenda` |
| `, c` | `org-capture` |
| `, e` | `org-export-dispatch` |
| `C-c C-c` | In an Org buffer, this has various context-sensitive actions. |

### Markdown Layer

Provides keybindings for editing Markdown files, primarily under the major-mode leader key.

| Keybinding | Description |
|---|---|
| `, c p` | Preview the Markdown file in a browser. |
| `, t` | Insert a table. |
| `, i l` | Insert a link. |
| `, i i` | Insert an image. |
| `, b` | Toggle bold text. |
| `, i` | Toggle italic text. |

### Shell Layer

This layer integrates various shells into Emacs.

| Keybinding | Description |
|---|---|
| `SPC '` | Toggle the default pop-up shell. |
| `SPC "` | Open an external terminal emulator in the current directory. |
| `SPC a t s e` | Toggle a pop-up Eshell. |

### Syntax Checking Layer

This layer uses Flycheck for on-the-fly syntax checking.

| Keybinding | Description |
|---|---|
| `SPC e l` | Display a list of all errors in the buffer. |
| `SPC e n` | Go to the next error. |
| `SPC e p` | Go to the previous error. |
| `SPC t s` | Toggle syntax checking on or off for the current buffer. |

### LSP (Language Server Protocol) Layer

Provides IDE-like features using the Language Server Protocol. Keybindings are generally available under `SPC l`.

| Keybinding | Description |
|---|---|
| `SPC l d` | Go to definition. |
| `SPC l r` | Find references. |
| `SPC l h` | Show documentation for the symbol at point. |
| `SPC l a a` | Show available code actions. |

### Emacs Lisp Layer

Provides keybindings for working with Emacs Lisp files, primarily under the `,` (major-mode leader) key.

| Keybinding | Description |
|---|---|
| `, e b` | Evaluate the buffer. |
| `, e d` | Evaluate the defun at point. |
| `, e e` | Evaluate the expression before the point. |
| `, h d v` | Describe the variable at point. |
| `, h d f` | Describe the function at point. |

### Better Defaults Layer

This layer enhances some default Emacs behaviors. While primarily for the `emacs` editing style, some features are style-agnostic. For instance, it provides a smarter `C-a` that toggles between the beginning of the line and the first non-whitespace character.

For a complete and interactive list of keybindings, you can always use the `which-key` feature by pressing `SPC` in normal mode.
## Modularization

Of course! Modularizing your Spacemacs configuration is an excellent way to keep it organized, maintainable, and easier to manage as it grows. The standard way to do this is by using the `~/.spacemacs.d/` directory.

Here is a comprehensive guide on how to convert your single `.spacemacs` file into a modular configuration within `~/.spacemacs.d/` on Linux.

### Why Modularize?

Before we dive in, let's look at the benefits:
*   **Readability:** Instead of one massive file, you have smaller files, each with a specific purpose (e.g., `layers.el`, `keybindings.el`, `ui.el`).
*   **Maintainability:** It's much easier to find and change a specific setting when you know which file it's in.
*   **Version Control:** You can track changes to different parts of your configuration more cleanly using Git.
*   **Sharing:** You can easily share specific parts of your configuration (like your custom keybindings) with others without sharing your entire setup.

---

### Step 1: Create the Directory and Your New `init.el`

Spacemacs is designed to look for `~/.spacemacs.d/init.el` if it cannot find a `~/.spacemacs` file. We will use this to our advantage.

1.  **Create the directory:**
    ```bash
    mkdir -p ~/.spacemacs.d/
    ```

2.  **Move your existing `.spacemacs` file** and rename it to `init.el` inside the new directory. This will become your main entry point.
    ```bash
    mv ~/.spacemacs ~/.spacemacs.d/init.el
    ```

At this point, if you restart Spacemacs, everything should work exactly as before. The only difference is that Spacemacs is now loading `~/.spacemacs.d/init.el` instead of `~/.spacemacs`.

### Step 2: Create Separate Files for Your Configuration

Now, let's create a few new files inside `~/.spacemacs.d/` to hold different parts of your configuration. A good starting structure is to separate layers, initial settings, and user configurations.

```bash
cd ~/.spacemacs.d/
touch layers.el
touch settings.el
touch user-init.el
touch user-config.el
```

Your directory should now look like this:
```
~/.spacemacs.d/
├── init.el
├── layers.el
├── settings.el
├── user-init.el
└── user-config.el
```

### Step 3: Move Your Configuration into the New Files

We will now cut the Lisp code from `init.el` and paste it into the appropriate new files.

#### A. `layers.el`
This file will hold your `dotspacemacs/layers` function.

**Cut** the entire `(defun dotspacemacs/layers () ...)` block from `init.el` and **paste** it into `~/.spacemacs.d/layers.el`.

The contents of `~/.spacemacs.d/layers.el` should be:
```emacs-lisp
;; ~/.spacemacs.d/layers.el

(defun dotspacemacs/layers ()
  "Layer configuration:
This function should only modify configuration layer settings."
  (setq-default
   ;; Base distribution to use...
   dotspacemacs-distribution 'spacemacs-base

   ;; Lazy installation of layers...
   dotspacemacs-enable-lazy-installation 'unused

   ;; ... (and so on for the rest of the variables in this function)

   ;; List of configuration layers to load.
   dotspacemacs-configuration-layers
   '(
     better-defaults
     emacs-lisp
     git
     ivy
     lsp
     markdown
     multiple-cursors
     org
     (shell :variables
            shell-default-height 30
            shell-default-position 'bottom)
     syntax-checking
     version-control
     treemacs)

   ;; List of additional packages...
   dotspacemacs-additional-packages '()

   ;; A list of packages that cannot be updated.
   dotspacemacs-frozen-packages '()

   ;; A list of packages that will not be installed and loaded.
   dotspacemacs-excluded-packages '()

   ;; Defines the behaviour of Spacemacs when installing packages.
   dotspacemacs-install-packages 'used-only))
```

#### B. `settings.el`
This file will hold your `dotspacemacs/init` function, which controls Spacemacs' core settings.

**Cut** the entire `(defun dotspacemacs/init () ...)` block from `init.el` and **paste** it into `~/.spacemacs.d/settings.el`.

The contents of `~/.spacemacs.d/settings.el` should be:
```emacs-lisp
;; ~/.spacemacs.d/settings.el

(defun dotspacemacs/init ()
  "Initialization:
This function is called at the very beginning of Spacemacs startup,
before layer configuration.
It should only modify the values of Spacemacs settings."
  (setq-default
   ;; Maximum allowed time in seconds to contact an ELPA repository.
   dotspacemacs-elpa-timeout 5

   ;; ... (all the other setq-default settings from your original dotspacemacs/init)

   ;; If non-nil then byte-compile some of Spacemacs files.
   dotspacemacs-byte-compile nil))
```

#### C. `user-init.el` and `user-config.el`
These will hold your personal customizations.

1.  **Cut** `(defun dotspacemacs/user-init () ...)` from `init.el` and **paste** it into `~/.spacemacs.d/user-init.el`.
2.  **Cut** `(defun dotspacemacs/user-config () ...)` from `init.el` and **paste** it into `~/.spacemacs.d/user-config.el`.
3.  **Cut** `(defun dotspacemacs/user-env () ...)` from `init.el` and just place it at the top of your `user-init.el` file.

The contents of `~/.spacemacs.d/user-init.el`:
```emacs-lisp
;; ~/.spacemacs.d/user-init.el

(defun dotspacemacs/user-env ()
  "Environment variables setup."
  (spacemacs/load-spacemacs-env))

(defun dotspacemacs/user-init ()
  "Initialization for user code before packages are loaded."
  ;; Example:
  ;; (setq-default some-variable-to-set-early t)
  )```

The contents of `~/.spacemacs.d/user-config.el`:
```emacs-lisp
;; ~/.spacemacs.d/user-config.el

(defun dotspacemacs/user-config ()
  "Configuration for user code after packages are loaded."
  ;; Example of a custom keybinding:
  ;; (global-set-key (kbd "C-c C-r") 'spacemacs/reload-dotspacemacs)
  )
```

### Step 4: Update `init.el` to Load Your New Files

Your `~/.spacemacs.d/init.el` file is now almost empty. We need to tell it to load the other files. We will use the Emacs Lisp function `load-file`.

Replace the entire content of `~/.spacemacs.d/init.el` with the following:

```emacs-lisp
;; -*- mode: emacs-lisp; lexical-binding: t -*-
;;
;; This is the main entry point for the modular Spacemacs configuration.
;; It loads other files from this directory.
;;

;;;==================================================================
;;; Load configuration files
;;;==================================================================
;; The variable `spacemacs-start-directory` points to `~/.spacemacs.d/`.
;; Using it makes your configuration portable. The order of loading is important!

(load-file (concat spacemacs-start-directory "layers.el"))
(load-file (concat spacemacs-start-directory "settings.el"))
(load-file (concat spacemacs-start-directory "user-init.el"))
(load-file (concat spacemacs-start-directory "user-config.el"))


;; Do not write anything past this comment. This is where Emacs will
;; auto-generate custom variable definitions.
```

**Explanation:**
*   `spacemacs-start-directory` is a special Spacemacs variable that automatically holds the path to `~/.spacemacs.d/`.
*   `(concat ...)` builds the full path to each of your new files.
*   `load-file` executes the Emacs Lisp code contained within that file.
*   **The order is crucial.** Spacemacs needs to know about layers and core settings first, before applying user configurations.

### Step 5: Restart and Verify

That's it! Save all your files and restart Emacs.

Spacemacs will:
1.  Load `~/.spacemacs.d/init.el`.
2.  `init.el` will then execute `load-file` for each of your modular files in the correct order.
3.  The functions (`dotspacemacs/layers`, `dotspacemacs/init`, etc.) will be defined just as they were before, and Spacemacs will call them at the appropriate times during startup.

Your setup is now cleanly modularized. When you want to add a new layer, you'll edit `layers.el`. When you want to tweak a theme or font, you'll edit `settings.el`. When you add your own keybindings or package settings, you'll edit `user-config.el`.
