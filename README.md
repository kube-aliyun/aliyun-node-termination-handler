# Aliyun Node Termination Handler

To reduce the cost, running the stateless application on spot instances is a good idea. But as we know it's always possible that the spot instance might be interrupted. Therefore, we'd better have a handler which can take action for our applications before the instance is terminated.

The handler is deployed on instances as demonset and watches the [Instance metadata](https://www.alibabacloud.com/help/doc-detail/49122.htm?spm=a2c63.p38356.879954.8.43937e77RKzQRN#section-uww-nvm-hfb). When terminating event detected, call the Kubernetes API to cordon the node first, then drain it.

## Major Features

- Monitors ECS Metadata for Spot Instance Termination Notifications
- Cordon first, then drain the node before terminated