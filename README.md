# DO180-apps
DO180 Repository for Sample Applications

image:
  repository: registry.ocp4.example.com:8443/etherpad
  name: etherpad
  tag: 1.8.18
route:
  host: development-etherpad.apps.ocp4.example.com

helm search repo

helm install example-app do280-repo/etherpad -f values.yaml --version 0.0.6
