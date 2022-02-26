#alias kubectl
alias k='kubectl'
alias kg='kubectl get'
alias kgp='kubectl get pod'
alias kgs='kubectl get service'

alias kd='kubectl describe'


#### 
alias ka='kubectl apply -f'
alias klo='kubectl logs -f'
alias kex='kubectl exec -i -t'


alias krm='kubectl delete'
alias krmf='kubectl delete -f'



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
Executar no shell ou adicionar ao ~/.bashrc
alias k=’kubectl’
alias kg=’k get’
alias kd=’k describe’
alias kl=’k logs’
alias ke=’k explain –recursive=true’
opt=’–dry-run=client -o yaml’
Outros uteis.
ctr -n <namespace> c ls
>> listar containers do containerd

grep -Rw . -e “image” -i
>> filtrar e localizar a palavra image dentro dos arquivos no diretorio local case insensitive

tr -d “\n”
>> remover quebra de linha

base64 (-d)
>> converter para base 64 (ou de base64)

openssl x509 -noout -text
>> Ler o conteudo base64 do certificado.

helm
>> Gerenciador de pacotes

docker build
Binario da Docker para gerenciar containers /construir imagens

curl -m -k
wget -o-
>> Utilitários para acesso HTTP/HTTPs por linha de comando.



alias kw='watch -n1 “kubectl get pod | grep -i $1″‘



alias ksysgpo='kubectl --namespace=kube-system get pod'

alias krm='kubectl delete'
alias krmf='kubectl delete -f'
alias krming='kubectl delete ingress'
alias krmingl='kubectl delete ingress -l'
alias krmingall='kubectl delete ingress --all-namespaces'

alias kgsvcoyaml='kubectl get service -o=yaml'
alias kgsvcwn='kubectl get service --watch --namespace'
alias kgsvcslwn='kubectl get service --show-labels --watch --namespace'

alias kgwf='kubectl get --watch -f'