# Kubectl Tips and Tricks

Part 2 of the infamous "Boosting your kubectl productivity" article.

## Content

- Display help and `kubectl explain` output in terminal pager (`less`) by default
- Auto-generate resource manifests with `kubectl run --dry-run`
    - For example, `kubectl run test --image=nginx --dry-run -o yaml` outputs the manifest of the Deployment that would be created with the `kubectl run` command. You can save this output to a file and use it as a starting point for customising the resource definition.
    - The `kubectl run` command can create Deployments, Jobs, and Pods (differentiated by the value of the `--restart` option), as well as Services (when the `--expose` option is present).
    - See "Cloud-Native DevOps with Kubernetes", p. 118
- kubectl that help save typing and look things up
    - https://github.com/kubermatic/fubectl
        - ~600 stars
        - No activity since 2 years    
    - https://github.com/thecasualcoder/kube-fzf
        - ~180 starts
        - No activity since 2 years
        - Standalone tools
    - https://github.com/bonnefoa/kubectl-fzf
        - ~500 starts
        - No activity since half a year
        - Most promising project
- kubectl-foreach: https://github.com/ahmetb/kubectl-foreach
    - kubectl plugin for running a kubectl command in multiple contexts (from kubeconfig file)
- kubespy: https://github.com/pulumi/kubespy
    - Tool for very detailed observation of Kubernetes resources
- kubecolor: https://github.com/hidetatz/kubecolor
    - Colorise kubectl output
- Advanced output formats and their applications
    - JSONPath
        - Resources:
            - [JSONPath - XPath for JSON](https://goessner.net/articles/JsonPath/)
            - https://github.com/json-path/JsonPath
            - [Jayway JsonPath evaluator](http://jsonpath.herokuapp.com/)
            - [JSONPath Support - Kubernetes](https://kubernetes.io/docs/reference/kubectl/jsonpath/)
    - Go template
        - Resources
            - [template - The Go Programming Language](https://golang.org/pkg/text/template/)
    - See `~/.bashrc` for applications
- kubectl alternatives to interact with Kubernetes
    - https://github.com/derailed/k9s
        - ~20k stars
        - Actively developed
    - https://github.com/kubernetes-sigs/kui
        - ~2.5k stars
        - Actively developed
        - GUI tool that combines command-line kubectl usage with graphical visualisations of output
    - https://github.com/databricks/click
        - ~1.4k stars
        - Semi-actively developed
        - Wrapper around kubectl (REPL)
    - https://github.com/alitari/kubexp
        - ~160 stars
        - No activity since 1 year
        - More ambitious Kubernetes frontend, similar to k9s
    - https://github.com/cloudnativelabs/kube-shell
        - ~2k stars
        - No activity since 5 years
    - https://github.com/c-bata/kube-prompt
        - ~1.7k stars
        - No activity since 2 years
    - https://github.com/errordeveloper/kubeplay
        - ~90 stars
        - No activity since 5 years
        - Allows printing Kubernetes resources as JSON. However, the same can quite easily be done with kubectl and maybe jq.
    - https://github.com/CanopyTax/ckube
        - ~130 stars
        - No activity since 2 years
        - Yet another limited kubectl wrapper
    - https://github.com/nii236/kk
        - ~120 stars
        - No activity since 6 years
        - Yet another very limited kubectl wrapper
    - https://github.com/rottencandy/vimkubectl
        - ~60 stars
        - Semi-actively developed

## Remarks

The published "Boosting your kubectl productivity" article contains the following topics:

1. Command completion (`kubectl completion`)
2. `kubectl explain`
3. `custom-columns` output
4. Switch between clusters and namespaces (`kubectx`/`kubens`, Bash aliases, `kubectl-ctx`/`kubectl-ns` plugins)
5. `kubectl-aliases`
6. kubectl plugins

## Resources

- https://medium.com/itnext/boosting-your-kubectl-productivity-b348f7c25712
