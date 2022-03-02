alias k='kubectl'
alias kg='k get'
alias kd='k describe'
alias kl='k logs'
alias ka='k apply -f'
alias krm='k delete'
alias kex='kubectl exec -i -t'
alias ke='k explain –-recursive=true'
opt='--dry-run=client -o yaml'

# Get current context
alias krc='kubectl config current-context'
# List all contexts
alias klc='kubectl config get-contexts -o name | sed "s/^/  /;\|^  $(krc)$|s/ /*/"'
# Change current context
alias kcc='kubectl config use-context "$(klc | fzf -e | sed "s/^..//")"'

# Get current namespace
alias krn='kubectl config get-contexts --no-headers "$(krc)" | awk "{print \$5}" | sed "s/^$/default/"'
# List all namespaces
alias kln='kubectl get -o name ns | sed "s|^.*/|  |;\|^  $(krn)$|s/ /*/"'
# Change current namespace
alias kcn='kubectl config set-context --current --namespace "$(kln | fzf -e | sed "s/^..//")"'

Alias de apoio:

adicionar ao ~/.vimrc
set et
set sw=2 sts=2 ts=2

Outros uteis.
tr -d “\n”
>> remover quebra de linha

base64 (-d)
>> converter para base 64 (ou de base64)

openssl x509 -noout -text
>> Ler o conteudo base64 do certificado.