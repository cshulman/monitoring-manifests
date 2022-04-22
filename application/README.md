#!/bin/bash

# Patch application service so it includes:
# 1) name of port
# 2) correct label
# Both required to ensure service monitor config allows metrics to be scraped

oc apply -f service-patch.yaml

# Create Service Monitor

oc apply -f serviceMonitor.yaml





