<!-- ABOUT THE PROJECT -->
## About The Project
This is a helm chart based on a docker image built from this [repo](https://github.com/salesforce/generic-sidecar-injector).
Follow the INSTALL.md to deploy a service injector. There's also steps to launch a demo pod to test functionality.
Note instructions in the INSTALL.md to enable/disable TLS connections.
<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- GETTING STARTED -->
## Getting Started

See [INSTALL.md](INSTALL.md) for instructions

### Prerequisites

This is an example of how to list things you need to use the software and how to install them.
* npm
  ```sh
  npm install npm@latest -g
  ```

### Installation

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

  helm repo add qrypt-sc https://docs.qrypt.com/sidecarinjector/

If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the packages.  You can then run `helm search repo
qrypt-sc` to see the charts.

To install the sidecarinjector chart:

    helm install my-sidecarinjector qrypt-sc/sidecarinjector

To uninstall the chart:

    helm delete my-sidecarinjector

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- LICENSE -->
## License

Distributed under the MIT License. See [LICENSE](LICENSE) for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>
