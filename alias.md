complete -F __start_kubectl k

alias k='kubectl'
alias kg='k get'
alias kd='k describe'
alias kl='k logs'
alias ka='k apply -f'
alias krm='k delete'
alias kex='kubectl exec -i -t'
alias ke='k explain –-recursive=true'
alias kn='k config set-context --current --namespace '
do='--dry-run=client -o yaml'
now='--grace-period 0 --force'

alias kn='kubectl config set-context --current --namespace '


set tabstop=2
set expandtab
set shiftwidth=2


# display list of contexts
kubectl config get-contexts
# display the current-context
kubectl config current-context  
    
# set the default context to my-cluster-name
kubectl config use-context my-cluster-name



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
