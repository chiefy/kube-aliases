# kube-aliases

This is an oh-my-zsh plugin (or source `kube-aliases.plugin.zsh` for bash) to
make working with Kubernetes easier. It provides a bunch of bash aliases and
Zsh functions. 

## Usage

### Aliases

For help, run `khelp`:

In general and when it makes sense, aliases follow the following conventions.

```bash
k           # kubectl
kdel<r>       # kubectl delete <resource>, e.g. kgp for kubectl delete pods
kd<r>      # kubectl describe <resource>, e.g. kdsp for kubectl describe pod
ke<r>       # kubectl edit <resource>, e.g. kgp for kubectl edit pods
kg<r>       # kubectl get <resource>, e.g. kgp for kubectl get pods
kga<r>      # kubectl get --all-namespaces -o wide <resource>, e.g. kgap for kubectl --all-namespaces -o wide get pods
```

However, these aliases can be customize by editing the config file
aliases.yaml. See customizing.

There is also some other useful commands such as the following:

```bash
kcon       # create configuration files
kdap       # delete all pods within a namespace
kdrain     # drain a node
keit       # execute a command in a specified pod,
           # default drops user into a shell
kfind      # use a regular expression to find items across everything except
           # custom resources
kgpns      # Get just pod names in a namespace
kl         # kubectl logs <podname>
klf        # kubectl logs -f <podname>: i.e. watch logs live
kpfind     # Search through pods with regular expressions
kdfind     # Search through deployments with regular expressions
krd        # restart a deployment
kstatus    # search across namespaces to find pods statuses
```
There is more, but can be found in `bin/` or by running `khelp -f`.

Not everything is currently implemented, but more and more is being added to
the list. If something is missing that is desired, feel free to submit a pull
request.


## Installation

### Oh-My-Zsh

```
git clone git@github.com:Dbz/kube-aliases.git ~/.oh-my-zsh/custom/plugins/kube-aliases
echo "plugins+=(kube-aliases)" >> ~/.zshrc
```

You can also manually place `zsh-kuberenetes` inside of `plugins=(...)`

If you have set the `ZSH_CUSTOM` environment variable in your zshrc, then you should modify the git clone directory to be `$ZSH_CUSTOM/plugins/kube-aliases`.

### Antigen

Add `antigen bundle dbz/kube-aliases` to your antigen bundles in your `.zshrc`

### Zgen

Add `zgen load dbz/kube-aliases` to your zgen plugins in your `.zshrc`

### Bash

Source `kube-aliases.plugin.zsh` in your `.bashrc`.

### Aliases for Kubernetes Extensions

#### kubectx
For easy context and namespace switching there is
[kubectx](https://github.com/ahmetb/kubectx). `kubectx` allows users context
switching, and the linked github comes with `kubens` which allows for simple
namespace switching. You can use the following aliases:

```bash
alias kctx='kubectx'
alias kns='kubens'
```

# Customizing Aliases

Edit the file `aliases.yaml` and then run `mk_kube_aliases` to generate a new list.

`mk_kube_aliases` is written in go and can be built inside of the directory
`generate_aliases` with `make build`.
