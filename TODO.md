# FORKED TODOS

## Testing
- [ ] Extract error messages from .xcresult files

## Destinations
- [ ] Add watchOS physical device support
- [ ] Add visionOS simulator support
- [ ] Add visionOS physical device support


## Buidling
- [ ] Use `xcodemake` to build the project
- [ ] Check issue with entitlements for macOS projects
- [ ] Add integration with `Inject` for how reloading

## General
- [ ] Improve error message when no Xcode toolchain is found
- [ ] Improve workspace detection for Flutter projects

# **NEOVIM TODOS**

> Porting SweetPad from VSCode to Neovim would require a full rewrite, not a simple migration.

SweetPad is a VSCode extension designed to make Swift/iOS development possible in VSCode by integrating with tools like xcodebuild, swift-format, swiftlint, and sourcekit-lsp. VSCode extensions are built on a Node.js/TypeScript API and rely heavily on VSCode's extension host, UI, and event system. Neovim, on the other hand, is a completely different beast: it's a terminal-based editor with its own plugin ecosystem, written in Lua or Vimscript, and it doesn't natively support VSCode extensions.

**Here's what you'd actually have to do:**

## **1. Rebuild the Extension as a Neovim Plugin**

You can't "port" a VSCode extension directly. You'd need to reimplement SweetPad's features as a Neovim plugin, likely in Lua (the modern Neovim plugin language).

**This means writing new code to handle:**
- [ ]  Autocomplete (using Neovim's built-in LSP client, nvim-lspconfig, and configuring it for sourcekit-lsp)
- [ ]  Build & Run (wrapping xcodebuild/xcrun in Lua functions and exposing them as Neovim commands)
- [ ]  Formatting (integrating swift-format via null-ls or a custom Lua wrapper)
- [ ]  Simulator/device management (invoking xcrun simctl and parsing output)
- [ ]  Debugging (integrating with CodeLLDB or another LLDB frontend for Neovim)
- [ ]  Test running (again, wrapping xcodebuild test or similar)

## **2. Replace VSCode APIs with Neovim Equivalents**

- [ ]  All the UI, notifications, and command palette stuff in VSCode would need to be mapped to Neovim's command system, floating windows, or statusline.
- [ ]  Any VSCode-specific APIs (like the extension host, workspace events, etc.) have no direct equivalent in Neovim.

## **3. Leverage Existing Neovim Plugins**

- [ ]  Use nvim-lspconfig for LSP integration (sourcekit-lsp for Swift).
- [ ]  Use null-ls.nvim for formatting/linting (wrapping swift-format and swiftlint).
- [ ]  Use telescope.nvim for fuzzy finding and project navigation.
- [ ]  Use plenary.nvim for async jobs and utility functions.
- [ ]  Use dap.nvim for debugging (with LLDB).

## **4. Handle Platform-Specific Requirements**

- SweetPad only works on macOS with Xcode installed. Your Neovim plugin would have the same requirements.
- You'd need to shell out to xcodebuild, xcrun, and simctl, and parse their output in Lua.

## **5. Community and Maintenance**

- VSCode has a huge extension ecosystem and userbase; Neovim's is smaller but very active and fast-moving.
- Expect to maintain your plugin as Neovim evolves (especially as the Lua API changes).

## **TL;DR**

- No, you can't just "port" SweetPad to Neovim. You'd need to reimplement it from scratch as a Neovim plugin, using Lua, and leveraging Neovim's LSP, DAP, and job control APIs.
- The good news: most of the underlying tools (sourcekit-lsp, xcodebuild, swift-format, etc.) are CLI-based and can be integrated with Neovim.
- The bad news: it's a non-trivial project, but if you pull it off, you'll be a hero to every Swift dev who hates Xcode and loves modal editing.

If you want to see how others have approached similar migrations, check out the [__CoC.nvim__](https://github.com/neoclide/coc.nvim) project (which lets you run some VSCode extensions in Neovim, but not all, and not ones as complex as SweetPad), and the [__nvim-lspconfig__](https://github.com/neovim/nvim-lspconfig) docs for LSP integration. [__Using VSCode extensions in Neovim__](https://www.reddit.com/r/neovim/comments/11142r8/using_vscode_extensions_in_neovim/) | [__A pragmatic approach to migrating from VSCode to Neovim__](https://dev.to/tolomeo/a-pragmatic-approach-to-migrating-from-vscode-to-neovim-4fae)

**If you want to get started, I'd recommend:**
- [ ]  Setting up nvim-lspconfig with sourcekit-lsp for Swift
- [ ]  Writing Lua wrappers for xcodebuild, xcrun, and simctl
- [ ]  Using null-ls for formatting/linting
- [ ]  Looking at dap.nvim for debugging

> You'll be writing a lot of Lua, but you'll learn a ton about both Neovim and the Apple toolchain.
