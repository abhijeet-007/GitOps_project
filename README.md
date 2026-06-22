# GitOps Project - App Code & CI

This repo contains the **application source code**, **CI pipeline**, and **Dockerfile** for the GitOps project.

## What's in this repo
- Application source code
- `Dockerfile` for building the container image
- `.circleci/config.yml` for CI pipeline — builds and pushes Docker image to DockerHub, then updates the manifest repo with the new image tag

## How it works
Any push to this repo triggers CircleCI to:
1. Build a new Docker image tagged with the build number
2. Push the image to DockerHub
3. Update the image tag in the Kubernetes manifest repo

## Related Repos
| Repo | Purpose |
|------|---------|
| [GitOps-project-kube-manifest](https://github.com/abhijeet-007/GitOps-project-kube-manifest) | Kubernetes manifests — ArgoCD watches this repo to sync deployments to EKS |
| [gitops-project-terraform](https://github.com/abhijeet-007/gitops-project-terraform) | Terraform code to provision AWS EKS cluster and related infrastructure |

## Overall GitOps Flow
```
Code Push → CircleCI → Docker Build → Push to DockerHub
                                            ↓
                              Update Kube Manifest Repo
                                            ↓
                         ArgoCD detects change → Deploys to EKS
```
