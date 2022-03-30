### Alias
``` bash
alias k='kubectl'
alias kg='k get'
alias kd='k describe'
alias ka='k apply -f'
alias krm='k delete'
alias kl='k logs'
alias kex='kubectl exec -i -t'
alias ke='k explain –-recursive=true'
alias kn='k config set-context --current --namespace '

do='--dry-run=client -o yaml'
now='--grace-period 0 --force'
```

### Config VIM
``` bash
### Definir expandtab significa que você nunca mais quer ver um \t em seu arquivo - em vez disso, os pressionamentos de tecla tabs serão expandidos em espaços.
set expandtab
### Quantas colunas de espaço em branco um \t vale.
set tabstop=2
### Quantas colunas de espaço em branco vale um "nível de recuo".
set shiftwidth=2
### Quantas colunas de espaço em branco valem um pressionamento de tecla tab ou um pressionamento de tecla de retrocesso.
set softtabstop=2

Resumindo:
adicionar ao ~/.vimrc
set et
set sw=2 sts=2 ts=2
```