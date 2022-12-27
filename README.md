# GitHub Action


## Sample Repositories

| Repository                          | Workflow File | Actions |
|---|--------------------------------|------|
| gke-workload-identity | [build.yml](https://github.com/DevSecOpsSamples/gke-workload-identity/blob/master/.github/workflows/build.yml)     | [actions](https://github.com/DevSecOpsSamples/gke-workload-identity/actions/workflows/build.yml) | GCP, gcloud, Docker, Terraform, Python, pytest, Sonarqube |
| jenkins-fargate-cdk   | [build.yml](https://github.com/DevSecOpsSamples/jenkins-fargate-cdk/blob/master/.github/workflows/build.yml)     | [actions](https://github.com/DevSecOpsSamples/gke-workload-identity/actions/workflows/build.yml) | Docker, CDK, Sonarqube |

## Docker

## Cache

- Cache Gradle dependencies: [java/README.md](java/README.md)

    [java/.github/workflows/build-java.yml](java/.github/workflows/build-java.yml)

    [java/.github/workflows/build-java-sonarqube.yml](java/.github/workflows/build-java-sonarqube.yml)

## Metric

- [gke-workload-identity](https://github.com/DevSecOpsSamples/gke-workload-identity/blob/master/.github/workflows/build.yml)

## Reference

- [GitHub Actions /Using workflows / Cache dependencies / Caching dependencies to speed up workflows](https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows#managing-caches)

- https://github.com/actions/cache

- https://github.com/actions/cache/blob/main/examples.md#java---gradle
