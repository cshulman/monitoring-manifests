#!/bin/bash

# Patch application service so it includes:
# 1) name of port
# 2) correct label
# Both required to ensure service monitor config allows metrics to be scraped

oc apply -f service-patch.yaml

# Additional configurations required for Prometheus to be able to scrape metrics using TLS
# https://access.redhat.com/articles/6675491 
# Current workaround to avoid additional config for TLS:

# Create http route to /metrics endpoint only
oc apply -f metrics-route.yaml

# Create Service Monitor

oc apply -f serviceMonitor.yaml





