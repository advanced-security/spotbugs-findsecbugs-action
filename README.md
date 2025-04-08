# spotbugs-findsecbugs-action

> [!NOTE]
> This is an _unofficial_ tool created by Field Security Services, and is not officially supported by GitHub.

This Action run SpotBugs with FindSecBugs, and uploads the results to GitHub Code Scanning.

Set up a workflow that builds your JVM language project, then run this Action on the resulting build artifacts (JARs, WARs, class files, etc.).

## Usage

First, build your Java, Scala or other JVM language project in an Actions workflow.

Then, set up this Action as a step in your Actions workflow, e.g. for a typical Scala project where you have locally published a Jar file:

```yaml
    - name: Run SpotBugs with FindSecBugs
      uses: advanced-security/spotbugs-findsecbugs-action@45266478cb8627da923977dacd1fa413fdb616a5 # v1.0.6
```

## Inputs

* `spotbugs_version`: The version of SpotBugs to use. Default: `4.7.3`
* `spotbugs_checksum`: The SHA256 checksum of the SpotBugs tarball. Default is the checksum for the default version. Set to '' to disable checksum verification (not recommended).
  * find the checksum for the SpotBugs version you specify on the [GitHub release page](https://github.com/spotbugs/spotbugs/releases)
* `findsecbugs_version`: The version of FindSecBugs to use. Default: `1.12.0`
  * Maven Central releases are immutable, so there is no need to specify a checksum, but it is shown in the workflow log for traceability
* `spotbugs_target`: The target directory to run SpotBugs against. Default: `target/`
* `spotbugs_filename_glob`: The filenames to locate for SpotBugs, e.g. `*.class`, `*.jar`. Default: `*.jar`
* `upload_sarif`: Whether to upload the SARIF file to GitHub Code Scanning. Default: `true`
* `java_distribution`: The Java distribution to use. Default: `microsoft`
* `java_version`: The Java version to use. Default: `11`
* `no_cache`: Do not use cached versions of the Spotbugs and FindSecBugs tools. Default: `false`
* `path_prefix`: Add this path prefix to the start of file locations. Required: `false`
* `base_path`: The base path to use for installing the tools. Default: `/home/runner/work/`
* `ram`: The RAM to use in MB. Default: `768`

## Full sample workflow

See [starter-workflow.yml](starter-workflow.yml) for a full sample workflow.

## Q&A

Q: Why is this Action needed?

A: Several SpotBugs plugins are usable in CI/CD and Actions, but don't output SARIF, and they're not available for all JVM languages and build systems.

Q: Why doesn't the Action support setting argument X of SpotBugs?

A: It's a work-in-progress. Please raise an issue or a PR if you need a feature.

Q: Why do the files not resolve in the Code Scanning results?

A: The paths in the Jar or Class file metadata might not match up with the root of the repository. Try using the input `path_prefix`. If two build targets don't share the same prefix, then try running this Action twice, once per target with a different prefix for each.

Q: Why doesn't FindSecBugs find vulnerability X?

A: This Action just wraps those tools. Raise an issue on the [FindSecBugs repo](https://github.com/find-sec-bugs/find-sec-bugs/).

## Requirements

* GitHub Actions runner

## License

This project is licensed under the terms of the MIT open source license. Please refer to the [LICENSE](LICENSE) for the full terms.

## Maintainers

See [CODEOWNERS](CODEOWNERS) for the list of maintainers.

## Support

> [!NOTE]
> This is an _unofficial_ tool created by Field Security Services, and is not officially supported by GitHub.

See the [SUPPORT](SUPPORT.md) file.

## Background

See the [CHANGELOG](CHANGELOG.md), [CONTRIBUTING](CONTRIBUTING.md), [SECURITY](SECURITY.md), [SUPPORT](SUPPORT.md), [CODE OF CONDUCT](CODE_OF_CONDUCT.md) and [PRIVACY](PRIVACY.md) files for more information.
