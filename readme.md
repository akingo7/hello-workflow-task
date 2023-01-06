# Steps

Deploy Temporal and Jenkins on Kubernetes Cluster

```bash
kubectl kustomize apps/base/ --enable-helm | kubectl apply -f -
```

Install **Docker** and **Kubernetes Continuous Deploy** Jenkins plugin.

Create a Pipeline Jenkins job and configure it with the git repository. Create **Jenkins credentials** with CredentialID **Dockerhub**. Run the Jenkin job which will build the **worker** and **hello workflow** image from the Dockerfiles in the `docker` directory, push them to the docker registry, and deploy them to the Kubernetes cluster using the manifest file `deploy.yaml`.

To improve the app, I would consider the following options:

- Implementing additional features or functionality that would enhance the app's usefulness or user experience.
- Optimizing the app's performance, such as by optimizing database queries or implementing caching.
- Adding security measures, such as implementing authentication and authorization or encrypting sensitive data.
- Refactoring the app's code to make it more modular, maintainable, or testable.
- Use a private docker registry for the docker images.
- Implement measures like multi-zone or multi-region deployment to improve the app's availability in case of failures or outages.
