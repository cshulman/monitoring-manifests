- Follow instructions in application and grafana sub directories
	- Application & grafana configs are not dependant and order does not matter. 
	- Application configs ensure the metrics are scraped correctly via prometheus
	- Grafana configs deploy a new instance of grafana that can be customized,
	- Metrics scraped from the application configs can then be configured to display in grafana via dashboard configuration

------------
- Ensure the metrics are being scraped correctly by debugging & accesing user-workload prometheus

# Access user workload prometheus UI by portforwarding prometheus pod & opening locally in browser
# by port forwarding the prometheus-user-workload pod to port 9090 and then open locally

# Port forward
oc port-forward -n openshift-user-workload-monitoring pod/prometheus-user-workload-0 9090

# Open locally in browser
http://localhost:9090/targets



----------
# To move user-workload monitoring components to infra nodes, create configmap
# with neccessary node selector & toleration
oc apply -f user-workload-monitoring-config.yaml
