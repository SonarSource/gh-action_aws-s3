# gh-action_aws-s3

SonarSource GitHub Action for AWS S3

![GitHub Release](https://img.shields.io/github/v/release/SonarSource/gh-action_aws-s3)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=SonarSource_gh-action_aws-s3&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=SonarSource_gh-action_aws-s3)
[![.github/workflows/it-test.yml](https://github.com/SonarSource/gh-action_aws-s3/actions/workflows/it-test.yml/badge.svg)](https://github.com/SonarSource/gh-action_aws-s3/actions/workflows/it-test.yml)

## Usage

### Upload local dir to S3

```yaml
    steps:
    - name: Publish some dir to S3
        uses: SonarSource/gh-action_aws-s3@<tag>
        with:
          command: cp
          flags: --recursive
          source: some_dir
          destination: s3://some-bucket-name/some_dir
          aws_access_key_id: ${{ env.AWS_ACCESS_KEY_ID }}
          aws_secret_access_key: ${{ env.AWS_SECRET_ACCESS_KEY }}
          aws_session_token: ${{ env.AWS_SESSION_TOKEN }}
          aws_region: eu-central-1
```

### Remove existing dir on S3

```yaml
  steps:
        - name: Delete dir named test in S3
          uses: SonarSource/gh-action_aws-s3@<tag>
          with:
          command: rm
          source: s3://some-bucket-name/some_dir_to_remove
          aws_access_key_id: ${{ env.AWS_ACCESS_KEY_ID }}
          aws_secret_access_key: ${{ env.AWS_SECRET_ACCESS_KEY }}
          aws_session_token: ${{ env.AWS_SESSION_TOKEN }}
          aws_region: eu-central-1
          continue-on-error: true # should not fail in case the dir didn't exist
```

## Options

| Option name         | Description                                                                                                                       | Default |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|---------|
| `command`           | The command that will be performed. [More info](https://docs.aws.amazon.com/cli/latest/reference/s3/#available-commands)          | -       |
| `source`            | The file path that the file will be sourced from. This can be either a local file or S3 file. The S3 file should lead with s3://. | -       |
| `destination`       | The file path that the file will be place. This can be either a local file or S3 file. The S3 file should lead with s3://.        | -       |
| `aws_access_key_id` | The AWS access key part of your credentials                                                                                       | -       |
| `aws_secret_access_key` | The AWS secret access key part of your credentials                                                                                | -       |
| `aws_session_token` | The session token part of your credentials (session tokens only)                                                                  | -       |
| `aws_region` | Define the region of the bucket. S3 namespace is global but the bucket is regional.                                               | -       |
| `metadata_service_timeout` | The number of seconds to wait until the metadata service request times out                                                        | -       |
| `flags` | Additional query flags                                                                                                            | -       |
| `ignore-failure` | Used to not fail the gh-action in case of pre-commit check failure | `false`                    |

## Versioning

This project is using [Semantic Versioning](https://semver.org/).

The `master` branch shall not be referenced by end-users,
please use tags such as ![GitHub Release](https://img.shields.io/github/v/release/SonarSource/gh-action_aws-s3)instead
and [Renovate](https://docs.renovatebot.com/)
or [Dependabot](https://docs.github.com/en/code-security/dependabot) to stay up to date.

## Contribute

Contributions are welcome, please have a look at [DEV.md](./DEV.md)
