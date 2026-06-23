# Deploying an Application with Persistent Storage on Kubernetes

Demonstration of the basics of including persistent storage on Kubernetes.

## Content

- Simplest solution: `hostPath` volume
    - Demonstrate problems with this solution
- More avanced solution: manually created PersistentVolume attached to Pod with PersistentVolumeClaim
    - Demonstrate problem of creating PersistentVolumes
- Best solution: StorageClass provider that automatically creates PersistentVolumes
- Integration with cloud: use `awsElasticBlockStore` volume on AWS?

## Remarks

TODO: on what infrastructure to demonstrate it? Use terraform-aws-kubeadm? 

## Resources

<!-- List of resources that might be useful for writing the article -->
