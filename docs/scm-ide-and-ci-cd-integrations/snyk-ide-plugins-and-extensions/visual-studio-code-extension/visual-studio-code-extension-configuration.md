# Visual Studio Code extension configuration

## Environment variables

To analyze projects, the plugin uses the Snyk CLI which requires environment variables:

* `PATH`: the path to needed binaries, for example, to maven
* `JAVA_HOME`: the path to the JDK you want to use to analyze Java dependencies

Setting these variables only in a shell environment (for example, using `~/.bashrc`) is not sufficient, if you do not start the IDE from the command line or create a script file that starts the IDE using a shell environment.

* On `Windows`, you can set the variables using the GUI or on the command line using the `setx` tool.
* On `macOS`, the process `launchd` must know the environment variables to launch the IDE from Finder directly. You can set environment variables for applications launched using Finder by using the `launchctl setenv` command, for example, on start-up or through a script you launch at user login.\
  **Note:** The provision of environment variables to the macOS UI can change between operating system releases, so it may be easier to create a small shell script that launches the IDE to leverage the shell environment that can be defined via `~/.bashrc`.
* On `Linux`, updating the file /etc/environment can propagate the environment variables to the Windows manager and UI.

## Proxy

If you are behind a proxy, configure the proxy settings using VS Code proxy settings or set the proxy settings using `http_proxy` and `https_proxy` environment variables.

## Visual Studio Code extension configuration options

After the extension is installed, you can set the following configuration options for the extension. Note: Be sure to review the **Advanced** setting **Organization**.

* **Features**
  * **Code Security**: Configure if code security analysis should run over your code.
  * **Code Quality**: Configure if code quality analysis should run over your code.
  * **Open Source Security**: Configure if security analysis should run over your open source dependencies.
  * **Infrastructure as Code**: Configure if security analysis should run over your IaC configuration files.
* **Severity**: Set severity level to display in the analysis result tree.
* **Crash Report**: Send error reports to Snyk.
* **Telemetry**: Send usage statistics to Snyk.
* **Scanning Mode:** Run Snyk scans automatically in the background (Code and IaC)
* **Advanced**
  * **Auto Scan Open Source Security**: Run Snyk Open Source analysis in automatic mode.
  * **Additional Parameters**: Set additional `snyk test` [CLI options](../../../snyk-cli/commands/test.md) for the Open Source scanning. For **unmanaged** [**C/C++**](../../../supported-languages-package-managers-and-frameworks/c-c++/) **scanning**, use the CLI option `--unmanaged` to find vulnerabilities in open-source packages. This option works only for unmanaged C/C++ scanning; do not use this option for other languages. For all .NET Projects, Snyk recommends adding the `--all-projects` additional parameter.\
    Additional parameters do not apply to Snyk Code or Snyk IaC.
  * **Organization**: Specify an Organization to run tests for that Organization. Snyk recommends using `ORG_ID`. If you specify an Organization slug name, the value of the Organization setting `snyk.advanced.organization` must be the ORG slug as displayed in the URL of your org in the Snyk UI: `https://app.snyk.io/org/[orgslugname]`. If not specified, the preferred Organization defined in your [web account settings](https://app.snyk.io/account) is used to run tests.
  * **Custom endpoint**: Specify the Snyk API endpoint for custom multi-tenant or single-tenant setup, The default is `https://api.snyk.io`. For details, see [IDE URLs](../../../working-with-snyk/regional-hosting-and-data-residency.md#ides-urls).
  *   **Proxy Strict SSL:** Check to specify that the proxy server certificate should be verified against the list of supplied CAs specific to Snyk Code.\


      <figure><img src="../../../.gitbook/assets/image (1) (2) (1).png" alt="roxy strict SSL option"><figcaption><p>Proxy strict SSL option</p></figcaption></figure>
  * **Automatic Dependency Management** and **Cli Path**: Uncheck to opt out of downloading the CLI through the plugin and thus use your own installation of the CLI. Snyk recommends always using the most recent version of the CLI.
    * When **Automatic Dependency Management** is checked, the plugin will automatically download and keep the CLI updated.
    *   When **Automatic Dependency Management** is not checked and **Cli Path** contains a path, the plugin uses the provided CLI path. Use this option if downloading the CLI is not possible due to your network configuration (for example, due to firewall rules), and you need to obtain the CLI through other means.

        <figure><img src="../../../.gitbook/assets/Screenshot 2022-08-23 at 14.08.05 (1).png" alt="Automatic Dependency Management and CLI Path"><figcaption><p>Automatic Dependency Management and CLI Path</p></figcaption></figure>
