---
title: "Azure Operator Nexus: How to configure cluster metrics configuration management"
description: Instructional for the inputs and methods for creating, updating, retrieving, and deleting cluster metrics configurations.
author: bryan-strassner
ms.author: bstrassner
ms.service: azure-operator-nexus
ms.topic: how-to
ms.date: 02/09/2023
ms.custom: template-how-to
---

# Cluster metrics configuration

When the user deploys a Cluster, a standard set of metrics are enabled for collection. For the list of metrics, see
[List of Metrics Collected](List-of-metrics-collected.md).

Users can't control the behavior (enable or disable) for collection of these included standard metrics. Though, users can control the collection of some optional metrics that aren't part of the link to the list. To enable this experience, users have to create and update a MetricsConfiguration resource for a cluster. By default, creation of this MetricsConfiguration resource doesn't change the collection of metrics. User has to update the resource to enable or disable these optional metrics collection.  

> [!NOTE] 
> * For a cluster, at max, only one MetricsConfiguration resource can be created.
> * Users need to create a MetricsConfiguration resource to check a list of optional metrics that can be controlled. 
> * Deletion of the MetricsConfiguration resource results in the standard set of metrics being restored.

## How to manage cluster metrics configuration

To support the lifecycle of cluster metrics configurations, the following interactions allow for the creation and management of a cluster's metrics configurations.

### Creating a metrics configuration

Use the `az network cluster metricsconfiguration create` command to create metrics configuration for cluster. If you have multiple Azure subscriptions, select the appropriate subscription ID using the [az account set](/cli/azure/account#az-account-set) command.

```azurecli
az networkcloud cluster metricsconfiguration create \
 --cluster-name "<CLUSTER>" \
 --extended-location name="<CLUSTER_EXTENDED_LOCATION_ID>" type="CustomLocation" \
 --location "<LOCATION>" \
 --collection-interval <COLLECTION_INTERVAL (1-1440)> \
 --enabled-metrics "<METRIC_TO_ENABLE_1>" "<METRIC_TO_ENABLE_2>" \
 --tags <TAG_KEY1>="<TAG_VALUE1>" <TAG_KEY2>="<TAG_VALUE2>" \
 --resource-group "<RESOURCE_GROUP>"
```

* Replace values within `<` `>` with your specific information.
* Query the cluster resource and find the value of `<CLUSTER-EXTENDED-LOCATION-ID>` in the `properties.clusterExtendedLocation`
* The `collectionInterval` field is required, `enabledMetrics` is optional and may be omitted.

> [!NOTE] 
> * The default metrics collection interval for standard set of metrics is set to every 5 minutes. Changing the `collectionInterval` will also impact the collection frequency for default standard metrics.
> * There can be only one set of metrics configuration defined per cluster. The resource is created with the name `default`.

Specifying `--no-wait --debug` options in az cli command results in the execution of this command asynchronously. For more information, see [how to track asynchronous operations](howto-track-async-operations-cli.md).

### Metrics configuration elements

| Parameter name                        | Description                                                                                        |
| --------------------------------------| -------------------------------------------------------------------------------------------------- |
| CLUSTER                               | Resource Name of Cluster                                                                           |
| LOCATION                              | The Azure Region where the Cluster is deployed                                                     | 
| CLUSTER_EXTENDED_LOCATION_ID          | The Cluster extended Location from Azure portal                                                    |
| COLLECTION_INTERVAL                   | The collection frequency for default standard metrics                                              |
| RESOURCE_GROUP                        | The Cluster resource group name                                                                    |
| TAG_KEY1                              | Optional tag1 to pass to Cluster create                                                            |
| TAG_VALUE1                            | Optional tag1 value to pass to Cluster Create                                                      |
| TAG_KEY2                              | Optional tag2 to pass to Cluster create                                                            |
| TAG_VALUE2                            | Optional tag2 value to pass to Cluster create                                                      |
| METRIC_TO_ENABLE_1                    | Optional metric1 that is enabled in addition to the default metrics            |
| METRIC_TO_ENABLE_2                    | Optional metric2 that is enabled in addition to the default metrics            |

Specifying `--no-wait --debug` options in az cli command results in the execution of this command asynchronously. For more information, see [how to track asynchronous operations](howto-track-async-operations-cli.md).

## Retrieving a metrics configuration

After a metrics configuration is created, it can be retrieved using a `az rest` command:


```azurecli
az networkcloud cluster metricsconfiguration show \
 --cluster-name "<CLUSTER>" \
 --resource-group "<RESOURCE_GROUP>"
```

This command returns a JSON representation of the metrics configuration.

## Updating a metrics configuration

Much like the creation of a metrics configuration, an update can be performed to change the configuration or update the tags assigned to the metrics configuration. 

```azurecli
az networkcloud cluster metricsconfiguration update \
 --cluster-name "<CLUSTER>" \
 --collection-interval <COLLECTION_INTERVAL (1-1440)> \
 --enabled-metrics "<METRIC_TO_ENABLE_1>" "<METRIC_TO_ENABLE_2>" \
 --tags <TAG_KEY1>="<TAG_VALUE1>" <TAG_KEY2>="<TAG_VALUE2>" \
 --resource-group "<RESOURCE_GROUP>"
```

The `collection-interval` can be updated independently of `enabled-metrics` list. Omit fields that aren't being changed.

Specifying `--no-wait --debug` options in az cli command results in the execution of this command asynchronously. For more information, see [how to track asynchronous operations](howto-track-async-operations-cli.md).

## Deleting a metrics configuration

Deletion of the metrics configuration returns the cluster to an unaltered configuration. To delete a metrics configuration, use the below command:

```azurecli
az networkcloud cluster metricsconfiguration delete \
 --cluster-name "<CLUSTER>" \
 --resource-group "<RESOURCE_GROUP>"
```

Specifying `--no-wait --debug` options in az cli command results in the execution of this command asynchronously. For more information, see [how to track asynchronous operations](howto-track-async-operations-cli.md).


