# CI check project namespace information

## Symptoms

When many jobs are being triggered from the same project.

## Possible checks

1. get project id, amount of jobs and build name:
    ```
    Ci::Build.where(status: [:pending, :running], project: Namespace.find(NAMESPACE_ID_GOES_HERE).projects).group(:project_id, :name).order('project_id asc, count(*) desc').pluck('project_id', 'count(*)', 'name')
    ```

1. commands that are being executed on the builds:
    ```
    Ci::Build.where(status: [:pending, :running], project: Namespace.find(NAMESPACE_ID_GOES_HERE).projects).group(:project_id, :commands).order('project_id asc, count(*) desc').pluck('project_id', 'count(*)', 'commands')
    ```

## Example issues

1. https://gitlab.com/gitlab-com/infrastructure/issues/3106
1. https://gitlab.com/gitlab-com/infrastructure/issues/2425
