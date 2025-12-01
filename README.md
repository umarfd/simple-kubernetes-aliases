Here you go — everything, including the README content and the example alias file, all inside one single code block exactly as you requested:

# Kubernetes Alias Setup (Modular .bashrc.d Method)

This document explains how to manage Kubernetes (kubectl/k3s) aliases using a modular configuration approach without placing them directly in `~/.bashrc`.  
This method keeps your shell configuration clean, organized, and easy to maintain.

---

## 1. Objective

- Store Kubernetes aliases in a dedicated file outside `.bashrc`.
- Keep `.bashrc` clean and readable.
- Use a modular configuration folder: `~/.bashrc.d/`.
- Allow easy updates or removal of alias groups.

---

## 2. Directory Structure

All aliases will be placed inside:



~/.bashrc.d/
└── kube_aliases.sh


You may also store other modular files:



docker_aliases.sh
git_aliases.sh
custom_env.sh


---

## 3. Installation Steps

### **1. Create the configuration directory**
```bash
mkdir -p ~/.bashrc.d

2. Create the Kubernetes alias file
nano ~/.bashrc.d/kube_aliases.sh


Paste the alias content inside.

3. Add a loader to .bashrc (if not already present)

Add this line at the bottom of ~/.bashrc:

# Load modular bash configuration
for file in ~/.bashrc.d/*.sh; do
  [ -r "$file" ] && source "$file"
done

4. Reload your bash session
source ~/.bashrc

4. Example: Contents of kube_aliases.sh
##############################################
# KUBERNETES / K3S ALIAS
##############################################

alias k="kubectl"
alias kg="kubectl get"
alias kd="kubectl describe"
alias ka="kubectl apply -f"
alias ke="kubectl edit"
alias krm="kubectl delete"
alias kl="kubectl logs"
alias klo="kubectl logs -f"
alias kex="kubectl exec -it"

alias kgn="kubectl get ns"
alias kcn="kubectl config set-context --current --namespace"

alias kgp="kubectl get pods"
alias kgd="kubectl get deployments"
alias kgs="kubectl get svc"
alias kgi="kubectl get ingress"
alias kgcm="kubectl get configmap"
alias kgse="kubectl get secret"

alias kdp="kubectl describe pod"
alias kdd="kubectl describe deployment"
alias kds="kubectl describe svc"

alias klf="kubectl logs -f"
alias kexe="kubectl exec -it"

alias k3slog="sudo journalctl -u k3s -f"
alias k3sser="systemctl status k3s"
alias k3sctl="sudo k3s kubectl"

alias ktop="kubectl top pods"
alias ktopn="kubectl top nodes"
alias kpf="kubectl port-forward"
alias kdesc="kubectl describe"

alias kapply="kubectl apply -f"
alias krestart="kubectl rollout restart"
alias kundo="kubectl rollout undo"

kexec() {
  pod=$(kubectl get pod | grep $1 | awk '{print $1}')
  kubectl exec -it "$pod" -- /bin/sh
}

klog() {
  pod=$(kubectl get pod | grep $1 | awk '{print $1}')
  kubectl logs -f "$pod"
}
##############################################

5. Testing the Aliases

Try running:

k get pods


or:

kcn staging


If the command works, the alias setup is successful.

6. Extra Tips

You can add more modular files such as:

helm_aliases.sh

docker_aliases.sh

env_vars.sh

Ensure all script files are readable:

chmod 644 ~/.bashrc.d/*.sh

7. Uninstalling

To remove Kubernetes aliases:

rm ~/.bashrc.d/kube_aliases.sh
source ~/.bashrc


If you want, I can generate:

an automatic installer script

an uninstaller

a global version for /etc/profile.d

or a GitHub-ready folder structure
Just tell me!


If you'd like this exported as a **README.md file**, say the word — I can generate it via python_user_visible so you can download it.
