## Rolling Updates and Rollbacks in Kubernetes

Rolling Updates and Rollbacks are essential features in Kubernetes for managing application deployments. They allow you to update your application to a new version or revert to a previous version with minimal downtime and disruption.

## Rolling Updates

#### What Are Rolling Updates?
A Rolling Update is a strategy for updating applications by gradually replacing old Pods with new ones.

It ensures that the application remains available during the update process.

#### How Rolling Updates Work:

- Create New Pods:

Kubernetes creates new Pods with the updated version of the application.

- Gradual Replacement:

Kubernetes replaces old Pods with new Pods one by one (or in batches).

- Health Checks:

Kubernetes ensures that new Pods are healthy before replacing the next set of old Pods.

- Completion:

Once all old Pods are replaced, the Rolling Update is complete.

#### Rollbacks

What Are Rollbacks?<br>

A Rollback is the process of reverting an application to a previous version.

It is used when a new version of the application has issues (e.g., bugs, performance problems).

How Rollbacks Work:

- Check Deployment History:

Kubernetes maintains a history of all revisions of a Deployment.

- Revert to a Previous Revision:

You can revert the Deployment to a previous revision.

- Rollback Process:

Kubernetes performs a Rolling Update to replace the current Pods with Pods from the previous revision.

