# atari.ops

This repositry regroups the configuration-as-code to provision, configure,
deploy and manage the EPFL's atari app. It uses [Ansible] wrapped in a
convenient [suitcase], called [`atarisible`](./atarisible).


## TL;DR

`./atarisible`

1. Uses the [common-web] to build the atari image, checkouting the code from [github].
1. Adds some secrets and config map, create a service, routes and a deployment config.
1. If needed or asked, it will redeploy the pod.

Detailled operations might look like:
```
./atarisible -vvv -t atari.is,atari.build
$ oc logs -f bc/atari --version=NN -n atari-test
./atarisible -vvv -t atari.promote --prod
./atarisible -vvv -t atari.secrets,atari.routes,atari.service,atari.cm,atari.dc --prod
```

## Prerequisites

* Access to our [Keybase] `/keybase/team/epfl_atari/` directory.
* Access to `atari-test` & `atari-prod` namespaces on our [OpenShift] cluster.


## Tags
<!--- for f in $(find . -path ./ansible-deps-cache -prune -false -o -name '*.yml'); do cat $f | yq '.[] | {name, tags}| with_entries( select( .value != null ) )' 2>/dev/null; done --->

| name                             | tags                                                                          |
|:---------------------------------|:------------------------------------------------------------------------      |
|Secrets                           | `atari.dbs`<br>`atari.secrets`                                  |
|Service                           | `atari.service`                                                        |
|Routes                            | `atari.routes`                                                         |
|Config Map                        | `atari.config`<br>`atari.cm`                                    |
|Deployment Config                 | `atari.dc`<br>`atari.deploy`<br>`atari.deploymentconfig` |
|Redeploy                          | `atari.deploy.force`                                                   |
|Build image                       | `atari.is`<br>`atari.image`<br>`atari.imagestream`       |
|Rebuild now                       | `atari.build`                                                          |
|Promote                           | `atari.promote`                                                        |



[Ansible]: https://www.ansible.com (Ansible is Simple IT Automation)
[suitcase]: https://github.com/epfl-si/ansible.suitcase (Install Ansible and its dependency stack into a temporary directory)
[github]: https://github.com/epfl-si/atari
[Keybase]: https://keybase.io
[OpenShift]: https://openshift.com
[common-web]: https://github.com/epfl-si/common-web
[//]: # "comment"
