# Linux-Troubleshooting
- **reset prompt**: `PROMPT='%n@%m:%~$ '`
- **permanent** `:user@fedora:`
``` bash
    cp ~/.zshrc ~/.zshrc.backup.$(date +%Y%m%d-%H%M%S) 2>/dev/null

    cat > ~/.zshrc <<'EOF'
    
    export PATH="$HOME/.local/bin:$PATH"
    
    PROMPT='%n@%m:%~$ '
    RPROMPT=''
    EOF
    
    exec zsh
```

- [XAMPP](https://github.com/ciavel/Linux-Troubleshooting/blob/main/Installing_XAMPP.md)
- [VSCODE](https://github.com/ciavel/Linux-Troubleshooting/blob/main/Visual_studio-install.md)

**VSCODE EXTENSIONS**
```bash
    # PHP
    code --install-extension bmewburn.vscode-intelephense-client
    code --install-extension xdebug.php-debug
    
    # HTML/CSS/JS/React
    code --install-extension esbenp.prettier-vscode
    code --install-extension dbaeumer.vscode-eslint
    code --install-extension dsznajder.es7-react-js-snippets
    code --install-extension formulahendry.auto-rename-tag
    code --install-extension bradlc.vscode-tailwindcss
    code --install-extension ritwickdey.LiveServer
    
    # Colors, readability, UI
    code --install-extension naumovs.color-highlight
    code --install-extension usernamehw.errorlens
    code --install-extension oderwat.indent-rainbow
    code --install-extension PKief.material-icon-theme
    code --install-extension GitHub.github-vscode-theme
    code --install-extension zhuangtongfa.Material-theme
    code --install-extension Catppuccin.catppuccin-vsc
    
    # AI coding
    code --install-extension GitHub.copilot
    code --install-extension GitHub.copilot-chat
    code --install-extension openai.chatgpt
```



