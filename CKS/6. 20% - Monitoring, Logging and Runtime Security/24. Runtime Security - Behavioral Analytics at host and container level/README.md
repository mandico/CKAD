# install falco
curl -s https://falco.org/repo/falcosecurity-packages.asc | apt-key add -
echo "deb https://download.falco.org/packages/deb stable main" | tee -a /etc/apt/sources.list.d/falcosecurity.list
apt-get update -y
apt-get install -y linux-headers-$(uname -r)
apt-get install -y falco=0.32.1


# docs about falco
https://v1-16.docs.kubernetes.io/docs/tasks/debug-application-cluster/falco


# Syscall talk by Liz Rice
https://www.youtube.com/watch?v=8g-NUUmCeGI

