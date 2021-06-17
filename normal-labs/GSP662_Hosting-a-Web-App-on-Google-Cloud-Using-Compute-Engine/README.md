# GSP662 —— Hosting a Web App on Google Cloud Using Compute Engine

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Create Compute Engine Instances](#create-compute-engine-instances)
- [Create Managed Instance Groups](#create-managed-instance-groups)
- [Create Load Balancers](#create-load-balancers)
  - [HTTP Load Balancer Instruction](#http-load-balancer-instruction)
  - [Operations](#operations)
- [Scale Compute Engine](#scale-compute-engine)
- [References](#references)

</details>

## Overview

There are many ways to deploy web sites within Google Cloud with each solution offering different features, capabilities, and levels of control. Compute Engine offers a deep level of control over the infrastructure used to run a web site, but also requires a little more operational management compared to solutions like Google Kubernetes Engines (GKE), App Engine, or others. With Compute Engine, you have fine-grained control of aspects of the infrastructure, including the virtual machines, load balancers, and more. In this lab you will deploy a sample application, the "Fancy Store" ecommerce website, to show how a website can be deployed and scaled easily with Compute Engine.

## Create Compute Engine Instances

```bash
# create compute engine instance
$ gcloud compute instances create <NAME>\
    --machine-type="<MACHINE_TYPE>" \
    --tags="<TAG>" \
    --metadata="startup-script-url"="<FILE_PATH>"

# check the instances
$ gcloud compute instances list

# configure network
$ gcloud compute firewall-rules create <RULE_NAME> \
    --allow="tcp:<PORT>" \
    --target-tags="<TAGS>"
```

## Create Managed Instance Groups

A managed instance group (MIG) contains identical instances that you can manage as a single entity in a single zone. Managed instance groups maintain high availability of your apps by proactively keeping your instances available, that is, in the RUNNING state. We will be using managed instance groups for our frontend and backend instances to provide autohealing, load balancing, autoscaling, and rolling updates.

```bash
# create instance template
$ gcloud compute instance-templates create <TEMPLATE_NAME> --source-instance="<INSTANCE_NAME>"

# check the instance templates
$ gcloud compute instance-templates list

# create manged instance group
$ gcloud compute instance-groups managed create <GROUP_NAME> \
    --base-instance-name="<BASE_NAME>" \
    --size="<SIZE>" \
    --template="<TEMPLATE_NAME>"

# setup the ports
$ gcloud compute instance-groups set-named-ports <GROUP_NAME> \
    --named-ports="<NAME:PORT>"

# create health check
$ gcloud compute health-checks create http <CHECK_NAME> \
    --port="<PORT>" \
    --check-interval="<INTERVAL>" \
    --healthy-threshold="<THRESHOLD>" \
    --timeout="<TIMEOUT>" \
    --unhealthy-threshold="<THRESHOLD>"

# create firewall rules to allow the health check
$ gcloud compute firewall-rules create <RULE_NAME> \
    --allow="<PROTOCOL:PORT_RANGE>" \
    --source-ranges="<RANGE>" \
    --network="default"

# apply health checks to services
$ gcloud compute instance-groups managed update <GROUP_NAME> \
    --health-check="<CHECK_NAME>" \
    --initial-delay="<DELAY>"
```

## Create Load Balancers

### HTTP Load Balancer Instruction

1. A forwarding rule directs incoming requests to a target HTTP proxy.
2. The target HTTP proxy checks each request against a URL map to determine the appropriate backend service for the request.
3. The backend service directs each request to an appropriate backend based on serving capacity, zone, and instance health of its attached backends. The health of each backend instance is verified using an HTTP health check. If the backend service is configured to use an HTTPS or HTTP/2 health check, the request will be encrypted on its way to the backend instance.
4. Sessions between the load balancer and the instance can use the HTTP, HTTPS, or HTTP/2 protocol. If you use HTTPS or HTTP/2, each instance in the backend services must have an SSL certificate.

### Operations

```bash
# create health checks used to determine which instances are capable of serving traffic for each service
$ gcloud compute http-health-checks create <CHEKC_NAME> \
    --request-path="<PATH>" --port="<PORT>"

# create backend services that are the target for load-balanced traffic
$ gcloud compute backend-services create <SERVICE_NAME> \
    --http-health-checks="<CHECK_NAME>" \
    --port-name="<PORT_NAME>" \
    --global

# add the Load Balancer's backend services
$ gcloud compute backend-services add-backend <SERVICE_NAME> \
    --instance-group="<GROUP_NAME>" \
    --instance-group-zone="<ZONE_NAME>" \
    --global

# create URL map (defines which URLs are directed to which backend services)
$ gcloud compute url-maps create <MAP_NAME> \
    --default-service="<SERVICE_NAME>"

# create path matcher to allow the paths to route to their respective
$ gcloud compute url-maps add-path-matcher fancy-map \
   --default-service="<SERVICE_NAME>" \
   --path-matcher-name="<PATH_MATCHER_NAME>" \
   --path-rules="<RULES>"

# create the proxy which ties to the URL map
$ gcloud compute target-http-proxies create <PROXY_NAME> \
    --url-map="<MAP_NAME>"

# create global forwarding rule that ties a public IP address and port to the proxy
$ gcloud compute forwarding-rules create <RULE_NAME> \
    --target-http-proxy="<PROXY_NAME>" \
    --ports="<PORT>" \
    --global

# find the IP address for the Load Balancer
$ gcloud compute forwarding-rules list --global

# issue a rolling restart command
$ gcloud compute instance-groups managed rolling-action replace <GROUP_NAME> \
    --max-unavailable="100%"
```

## Scale Compute Engine

```bash
# create the autoscaling policy
$ gcloud compute instance-groups managed set-autoscaling <GROUP_NAME>
    --max-num-replicas="<NUM>" \
    --target-load-balancing-utilization="<UTILIZATION>"

# enable Content Delivery Network (CDN) service
$ gcloud compute backend-services update <SERVICE_NAME> \
    --enable-cdn --global
```

## References

- [Virtual machine instances | Compute Engine Documentation](https://cloud.google.com/compute/docs/instances/)
- [Instance templates | Compute Engine Documentation](https://cloud.google.com/compute/docs/instance-templates/)
- [Instance groups | Compute Engine Documentation](https://cloud.google.com/compute/docs/instance-groups/)
- [Setting up health checking and autohealing | Compute Engine Documentation](https://cloud.google.com/compute/docs/instance-groups/autohealing-instances-in-migs)
- [Cloud Load Balancing Documentation](https://cloud.google.com/load-balancing/docs)
- [Creating health checks | Cloud Load Balancing Documentation](https://cloud.google.com/load-balancing/docs/health-checks)
- [Cloud CDN Documentation](https://cloud.google.com/cdn/docs)