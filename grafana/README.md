#!/bin/bash

# Create namespace for custom grafana instance
oc apply -f grafana-namespace.yaml

# Deploy custom grafana instance
oc apply -f grafana-subscription.yaml

# MUST WAIT UNTIL OPERATOR INSTALLED TO PROCEED

# Create grafana instance
oc apply -f grafana-instance.yaml

# Add required cluster rolebinding to grafana service account
oc apply -f grafana-sa-rolebinding.yaml


# Modify grafana-datasource.yaml so it includes bearer token for the grafana-serviceaccount
# Retrieve bearer token for service account
oc serviceaccounts get-token grafana-serviceaccount -n custom-grafana

# Insert token in place of ${BEARER_TOKEN} or set output of above command to be BEARER_TOKEN


# Create datasource
oc apply -f grafana-datasource.yaml

# Create route to custom grafana dashboard
oc apply -f grafana-route.yaml


---
# Access grafana dashboard

# Retrieve route for grafana
oc get routes -n custom-grafana

# Retrieve user & password for authentication to grafana
# View files created containing the user and password
oc extract secret/grafana-admin-credentials

# Route and grafana user credentials can also be accessed vi OCP console


