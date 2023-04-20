## Get a Kubernetes Cluster 

- [Kubernetes cluster](https://kubernetes.io/docs/setup/)
- [Helm](https://helm.sh/docs/intro/using_helm/)

## Install Crossplane 

```
kubectl create namespace crossplane-system
helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update

helm install crossplane --namespace crossplane-system crossplane-stable/crossplane
```

## Adding Microsoft Azure to Crossplane

### Preparing your Microsoft Azure Account 

In order to manage resources in Azure, you must provide credentials for a Azure service principal that Crossplane can use to authenticate. This assumes that you have already set up the Azure CLI client with your credentials.

Create a JSON file that contains all the information needed to connect and authenticate to Azure:

```
# create service principal with Owner role
az ad sp create-for-rbac --sdk-auth --role Owner --scopes="/subscriptions/{subscriptionId}" -n "crossplane-sp-rbac" > crossplane-azure-provider-key.json
```

Take note of the `clientID` value from the JSON file that we just created, and save it to an environment variable:

```
export AZURE_CLIENT_ID=<clientId value from json file>
```

Now add the required permissions to the service principal that will allow it to manage the necessary resources in Azure:

```
# add required Azure Active Directory permissions
az ad app permission add --id ${AZURE_CLIENT_ID} --api 00000002-0000-0000-c000-000000000000 --api-permissions 1cda74f2-2616-4834-b122-5cb1b07f8a59=Role 78c8a3c8-a07e-4b9e-af1b-b5ccab50a175=Role

# grant (activate) the permissions
az ad app permission grant --id ${AZURE_CLIENT_ID} --api 00000002-0000-0000-c000-000000000000 --expires never
```

You might see an error similar to the following, but that is OK, the permissions should have gone through still:

```
Operation failed with status: 'Conflict'. Details: 409 Client Error: Conflict for url: https://graph.windows.net/e7985bc4-a3b3-4f37-b9d2-fa256023b1ae/oauth2PermissionGrants?api-version=1.6
```

Finally, you need to grant admin permissions on the Azure Active Directory to the service principal because it will need to create other service principals for your `AKSCluster`:

```
# grant admin consent to the service princinpal you created
az ad app permission admin-consent --id "${AZURE_CLIENT_ID}"
```

Note: You might need `Global Administrator` role to `Grant admin consent for Default Directory`. Please contact the administrator of your Azure subscription. To check your role, go to `Azure Active Directory` -> `Roles and administrators`. You can find your role(s) by clicking on `Your Role (Preview)`

After these steps are completed, you should have the following file on your local filesystem:

- `crossplane-azure-provider-key.json`
