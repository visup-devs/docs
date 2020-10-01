---
title: Deploy with {{ $names.company.lower }} button
excerpt: The Deploy with {{ $names.company.lower }} button allows users to do a single-click deployment and configuration of an application to {{ $names.cloud.lower }} 
---

# Deploy with {{ $names.company.lower }} button

The **Deploy with {{ $names.company.lower }}** button allows users to perform a single-click deployment and configuration of an application to {{ $names.cloud.lower }}.

![Deploy with {{ $names.company.lower }}](https://balena.io/deploy.png)

Clicking the **Deploy with {{ $names.company.lower }}** button opens the {{ $names.cloud.lower }} dashboard with a modal window pre-populated with everything required to deploy the application. Clicking the _Advanced_ toggle in the modal window allows adding additional configuration options. If the project has provided configuration variables via a [configuration file](#balenayml-configuration-file), they are pre-populated.

<img src="https://www.balena.io/docs/img/configuration/deploy-to-balena.png" width="80%">

Clicking _Create and deploy_ creates a new application and generates a release. Any devices added to the application will immediately download and begin running the release.

__Note:__ Currently git submodules are not supported and will not build properly.

## Adding a deploy with {{ $names.company.lower }} button to a project

You can add the **Deploy with {{ $names.company.lower }}** button to any project that can be deployed to {{ $names.cloud.lower }}. To add the button to a project repository, add the following to, for example, the project repository's README.md file:

`[![balena deploy button](https://www.balena.io/deploy.png)](https://dashboard.balena-cloud.com/deploy?repoUrl=<your-repo-url>)`

Note that you can further customize the button's behavior through the use of [query string parameters](#query-string-parameters).

### Query string parameters

You can further customize the behavior of the **Deploy with {{ $names.company.lower }}** button by providing additional URL parameters. The following URL parameters are available and may be appended to the `https://dashboard.balena-cloud.com/deploy` link:

* `repoUrl` - The URL of the project repository. If you are placing the deploy button in a GitHub repo then {{ $names.cloud.lower }} can auto-determine the `repoUrl` from the referer info in the HTTP headers. However on Firefox and with some ad-blockers this may fail. So we recommend that you populate this query string parameter.
* `tarballUrl` - The URL of the project tarball. Automatically determined from `repoUrl` if not provided.
* `configUrl` - The URL of the configuration file of the application. Automatically determined from `repoUrl` if not provided.
* `defaultDeviceType` - The device type that will be pre-selected in the "Create application" modal. It defaults to Raspberry Pi 4 if not provided. You can find a list of [device types here](reference/hardware/devices/).

### balena.yml configuration file

Through the use of a `balena.yml` config file, you may also provide application [configuration](/learn/manage/configuration/) and [environment](/learn/manage/serv-vars/) variables. If provided, they are pre-populated in the advanced modal dialog when using the **Deploy with {{ $names.company.lower }}** button.

The file should be named `balena.yml` and be located in the root of the project repository, or the `configUrl` link must be specified. A full example of the `balena.yml` file is shown below:

```yaml
repoUrl: "https://github.com/owner/reponame"
tarballUrl: "https://url-pointing-to-a-tarball.tar.gz"
applicationConfigVariables:
 - RESIN_HOST_CONFIG_gpu_mem: 128
applicationEnvironmentVariables:
 - CONFIG_MODE: 0
 - CUSTOM_VALUE: my_value
defaultDeviceType: 'fincm3'
```

__Note:__ You do not need to specify the  `tarballUrl` and `repoUrl` as part of the config file since those are determined automatically from the repository.
