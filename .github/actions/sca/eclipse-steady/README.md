# SCA Eclipse Steady Action

## Description

An action to configure and run a [Eclipse Steady](https://projects.eclipse.org/projects/technology.steady) SCA scan.

JSON result is uploaded as a build artifact.

## Inputs

| name                           | required | type   | default                   | description                                             |
| ------------------------------ | -------- | ------ | ------------------------- | ------------------------------------------------------- |
| language                       | true     | string |                           | Language to scan using Eclipse Steady                   |
| eclipse-steady-workspace-token | true     | string |                           | Token used to identify project workspace                |
| eclipse-steady-host-url        | true     | string |                           | Hostname of Eclipse Steady                              |
| project-name                   | true     | string |                           | Name of the project being scanned                       |
| project-source-directories     | true     | string |                           | Project source directories to scan (separated by comma) |
| path                           | false    | string | ${{ github.workspace }}   | Path to run the Eclipse Steady scan                     |
| build-artifact-name            | false    | string | sca-eclipse-steady-report | Name of Eclipse Steady build artifact                   |

## Example Execution

```yaml
- name: Run Eclipse Steady SCA Scan
  uses: seansmith39/H6060-Experiment-Resources/.github/actions/sca/eclipse-steady
  with:
    language: python
    eclipse-steady-workspace-token: 1111-2222-3333-4444
    eclipse-steady-host-url: https://my-eclipse-steady-instance.com
    project-name: my-project
    project-source-dir: src
```

## Note

- Due to difficulties in Eclipse Steady profile maintenance for Maven projects, the Eclipse Steady plugin for Maven was configured at runtime.
- If application is not starting, run the following steps:
  1. SSH into EC2 instance hosting Eclipse Steady.
  2. Stop all docker containers by running `docker stop $(docker ps -a -q)`
  3. Run `setup-steady.sh` and select `a`.
- In other cases, Eclipse Steady may not start due to docker space issues. In that scenario, increase the volume size attached to the EC2 instance hosting Eclipse Steady and restart the EC2 instance.