# Setup Namespace

Namespaces are the default way for kubernetes to separate resources.
    Namespaces do not share anything between them, which is important to know,
    and thus come in handy when you have multiple users on the same cluster,
    that you don't want stepping on each other's toes :)

## 1.1 Create a namespace

Choose a name for your namespace, something unique so you don't clash with one of the .

```shell
$ kubectl create namespace my-namespace
namespace "my-namespace" created
```

## 1.2 Scoping the kubectl command

You want to target your own namespace instead of default one every time you use `kubectl`.
    You can run a command in a specific namespace by using the `-n, --namespace=''`-flag.

The below commands do the same thing, because kubernetes commands will default to the default namespace:

```shell
kubectl get pods -n default
kubectl get pods
```

## 1.3 Set your default namespace

It gets tedious however to write this every time you want to select your own namespace,
    so it makes sense to set this as the default.

To overwrite the default namespace for your current `context`, run:

```shell
$ kubectl config set-context $(kubectl config current-context) --namespace=my-namespace
Context "<your current context>" modified.
```

Or perform the same step with two individual commands:
```
$ kubectl config current-context


## 1.4 More on Namespaces

Namespaces are quite powerful. On a user level, it is also possible to limit namespaces and resources by users but this is a bit too involved for your first experience with Kubernetes.

Kubernetes clusters come with a namespace called `default`, which in this case might contain some pods deployed previously by Praqma,
    and usually one called `kube-system` which will contain some of the kubernetes services running in the cluster.

You might see later that the namespace is specified directly in the yaml files describing the resources.
    This makes it possible to have the resource created in the specific namespace without specifying the `-n` flag on creation.
