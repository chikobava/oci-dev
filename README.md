# OCI development in a devcontainer

This is a repository for OCI development.
The devcontainer includes:

* oci cli
* packer
* terraform
* ansible

You don't need to install tooling on your local machine. Simply start the container and develop inside.

How to start with development?

* create folders .ssh and .oci in your working folder. Both locations are in .gitignore, so you don't need to worry, they won't be pushed. If you prefer a different location - change the mount paths in the `mounts` section of `./devcontainer/devcontainer.json` file.
* start the included devcontainer
* to create configuration for your oci, execute the following command in the container terminal:

```bash
oci setup config
```

Follow prompts and configure your oci accordingly.
You will need to login to oracle console (through browser) and add the generated api key to your profile.
Once you've added your public key to your user in OCI, you can test the config by running:

```bash
oci iam compartment list --compartment-id <compartment_ocid>
```

If you see a list of compartments - the setup was completed successfully.
