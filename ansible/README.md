# businesscard.ops

This repositry regroups the configuration-as-code to provision, configure,
deploy and manage the EPFL's businesscard app. It uses [Ansible] wrapped in a
convenient [suitcase], called [`busible`](./busible).


## TL;DR

`./busible`

1. Uses the [common-web] to build the businesscard image, checkouting the code from [github].
1. Adds some secrets and config map, create a service, routes and a deployment config.
1. If needed or asked, it will redeploy the pod.

Detailled operations might look like:
```
./busible -vvv -t businesscard.is,businesscard.build
$ oc logs -f bc/businesscard --version=NN -n businesscard-test
./busible -vvv -t businesscard.promote --prod
./busible -vvv -t businesscard.secrets,businesscard.routes,businesscard.service,businesscard.cm,businesscard.dc --prod
```

## Prerequisites

* Access to our [Keybase] `/keybase/team/epfl_businesscard/` directory.
* Access to `businesscard-test` & `businesscard-prod` namespaces on our [OpenShift] cluster.


## Tags
<!--- for f in $(find . -path ./ansible-deps-cache -prune -false -o -name '*.yml'); do cat $f | yq '.[] | {name, tags}| with_entries( select( .value != null ) )' 2>/dev/null; done --->

| name                             | tags                                                                          |
|:---------------------------------|:------------------------------------------------------------------------      |
|Secrets                           | `businesscard.dbs`<br>`businesscard.secrets`                                  |
|Service                           | `businesscard.service`                                                        |
|Routes                            | `businesscard.routes`                                                         |
|Config Map                        | `businesscard.config`<br>`businesscard.cm`                                    |
|Deployment Config                 | `businesscard.dc`<br>`businesscard.deploy`<br>`businesscard.deploymentconfig` |
|Redeploy                          | `businesscard.deploy.force`                                                   |
|Build image                       | `businesscard.is`<br>`businesscard.image`<br>`businesscard.imagestream`       |
|Rebuild now                       | `businesscard.build`                                                          |
|Promote                           | `businesscard.promote`                                                        |



[Ansible]: https://www.ansible.com (Ansible is Simple IT Automation)
[suitcase]: https://github.com/epfl-si/ansible.suitcase (Install Ansible and its dependency stack into a temporary directory)
[github]: https://github.com/epfl-si/businesscard
[Keybase]: https://keybase.io
[OpenShift]: https://openshift.com
[common-web]: https://github.com/epfl-si/common-web
[//]: # "comment"
