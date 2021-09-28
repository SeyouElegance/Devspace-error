# Devspace-error

<details>
  <summary>Installation</summary>
  
  ## Heading
Installation helm on Ubuntu :
Install devspace CLI (v5.15)
Ensure you have docker, helm (v2.17.0) and kubectl installed on your machine

Download 2.17.0
-> Extract here
-> On terminal access to last folder of helm downloaded file
-> which helm
-> sudo mv helm (copy/paste result of last commande)
-> helm version
</details>

<details>
   <summary>Usage</summary>

### First time

If this is the first time you start devspace, run the following command to tell devspace which namespace you prefer to use:

```bash
devspace use namespace my-namespace
```

### Deploy the application

All devspace commands must be run at the root of the folder.

To deploy your application, run the following command:

```bash
devspace deploy
```

### Update your hosts file for the new ingress(es)

When creating ingresses, you need to update your hosts file to map the custom domain(s) with the Ingress Controller Nginx IP, `34.79.192.20`.

Example for the Varnish ingress:
```
34.79.192.20 dev-yourname.laprovence.com dev-yourname-www.laprovence.com dev-yourname-api.laprovence.com dev-yourname-abonnement.laprovence.com
```

You can retrieve the URLs from the GCP Console

### Use the dev mode with hot-reloading

To start your application in dev mode and use the hot-reloading feature, run the following command:

```bash
devspace dev
```

It will deploy your application and its dependencies, then open a shell in the running container. You can now update your files locally and the changes will be reflected inside the container.

### Delete the application

To delete the deployment, run the following command:

```bash
devspace purge
```

If your deployment contains dependencies (e.g.: varnish) or if you want to fully clean your environment, run the following command to delete everything:

```bash
devspace purge -a
```

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

### Clear Varnish cache

If you deploy the application with Varnish as a dependency (default behavior), you can run the following command to clear its cache:

```bash
devspace run varnish.purge
```
</details>

### Useful commands

* `devspace enter` will open a shell in the selected container
* `devspace open` will create a port-forward from the cluster to your local machine, useful if you don't need an ingress to test your application
* `devspace ui` will deploy the web interface (also deployed when running in dev mode)
* `devspace logs` will retrieve the container logs (use the `-f` flag to stream it)
* `devspace list vars` will display the current variables and their values used in `devspace.yaml`
* `devspace reset vars` will reset the variables to their original value




**Two important rules:**
1. Make sure you have an **empty line** after the closing `</summary>` tag, otherwise the markdown/code blocks won't show correctly.
2. Make sure you have an **empty line** after the closing `</details>` tag if you have multiple collapsible sections.
