# DOCUMENTATION DEVSPACE

<details>
  <summary>Installation</summary>
  
  ## Installation on Ubuntu  
* Install [devspace CLI](https://devspace.sh/cli/docs/quickstart#1-download-cli) (v5.15)
* Ensure you have docker, helm (v2.17.0) and kubectl installed on your machine
  ## DETAILS Installation on Ubuntu
* [Download 2.17.0](https://get.helm.sh/helm-v2.17.0-linux-amd64.tar.gz)
-> Extract here
-> On terminal access to last folder of helm downloaded file
-> which helm
-> sudo mv helm (copy/paste result of last commande)
-> helm version
</details>

<details>
  
   <summary>Use it now</summary>

<br />

### First time
If this is the first time you start devspace, run the following command to tell devspace which namespace you prefer to use:

```bash
devspace use namespace my-namespace
```
<br />

### Deploy the applicationsudo vim /etc/hosts
All devspace commands must be run at the root of the folder.

To deploy your application, run the following command:

```bash
devspace deploy
```
<br />

### Update your hosts file for the new ingress(es)

When creating ingresses, you need to update your hosts file to map the custom domain(s) with the Ingress Controller Nginx IP, `34.79.192.20`.
DO IT => sudo vim /etc/hosts => CHANGE YOUR IP INGRESS HERE (You can retrieve the URLs from the GCP Console)
Example for the Varnish ingress:
```
34.79.192.20 dev-yourname.laprovence.com dev-yourname-www.laprovence.com dev-yourname-api.laprovence.com dev-yourname-abonnement.laprovence.com
```
<br />

### Use the dev mode with hot-reloading

To start your application in dev mode and use the hot-reloading feature, run the following command:

```bash
devspace dev
```
It will deploy your application and its dependencies, then open a shell in the running container. You can now update your files locally and the changes will be reflected inside the container.

<br />

### Delete the application

- To delete the deployment, run the following command:

```bash
devspace purge
```

- If your deployment contains dependencies (e.g.: varnish) or if you want to fully clean your environment, run the following command to delete everything:

```bash
devspace purge -a
```
<br />
  
### Deploy without Varnish

To deploy your application without Varnish, simply comment the following block in the `devspace.yaml` configuration file:

```yaml
# comment this block to disable varnish dependency
dependencies:
- name: varnish
  source:
    path: ../vcl-varnish
  vars:
    - name: backend_api
      value: api
```

<br />  

### Clear Varnish cache

If you deploy the application with Varnish as a dependency (default behavior), you can run the following command to clear its cache:

```bash
devspace run varnish.purge
```
</details>

<br />

#Abo

### JS

sudo apt install clang make ruby ruby-dev libffi-dev
sudo gem install ffi
sudo gem install compass:1.0.3

npm install && npm run webpack --watch

<br />  




# FAQ

<details>
   <summary>Problem with your certificat ?</summary>
  
  ```bash
    kubectl delete ns dev-yourname
  ```
</details>

<details>
   <summary>How to see if my namespace is existing already?</summary>
  
  ```bash
    devspace use namespace
  ```
</details>

<details>
   <summary>Waiting for pods...</summary>
  
  ```bash
    VOIR AVEC NICOLAS(OP-RATE) PROBLEME DE LE VOLUME
  ```
</details>

<details>
   <summary>start sync: unable to start sync: initial sync: upstream: apply changes: apply creates: upload archive: after upload: rpc error: code = Unknown desc = untar all: decompress: create /var/www/html/.git: open /var/www/html/.git: is a directory</summary>
  
  ```bash
    LANCER LA COMMANDE DEVSPACE DEV DEPUIS UN AUTRE TERMINAL QUE CELUI DE VSCODE
  ```
</details>

<details>
  <summary>
deploy dependencies: Deploy dependency varnish error : error building image eu.gcr.io/la-provence-develop/lp-varnish:dev-nadia-8443a97f: The command '/bin/sh -c wget https://varnish-cache.org/_downloads/ce820265a5403ff564d62b2651705460/varnish-4.1.9.tgz   && tar zxf varnish-4.1.9.tgz     && cd varnish-4.1.9   && bash configure    && make  && make install         && ldconfig   && rm -rf ../varnish-4.1.9.tgz ../varnish-4.1.9       && cd ../    && wget https://package.datadome.co/linux/DataDome-Varnish-latest.tgz  && tar zxf DataDome-Varnish-latest.tgz     && cd DataDome-VarnishDome-*     && bash autogen.sh    && bash configure    && make  && make install         && rm -rf ../DataDome-Varnish-latest.tgz ../DataDome-VarnishDome-*' returned a non-zero code: 8</summary>
  
 ```bash
    devspace update dependencies
 ```
</details>



