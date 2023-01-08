load('ext://color', 'color')

k8s_yaml(['config/rbac/role_binding.yaml', 'config/manager/manager.yaml'])

docker_build('kspan', '.', platform='linux/amd64')

load('ext://helm_resource', 'helm_resource', 'helm_repo')
helm_repo('jaegertracing', 'https://jaegertracing.github.io/helm-charts')
helm_resource('jaeger', 'jaegertracing/jaeger',
 flags=[
  '--set', 'allInOne.enabled=true',
  '--set', 'provisionDataStore.cassandra=false',
  '--set', 'agent.enabled=false',
  '--set', 'query.enabled=false',
  '--set', 'collector.enabled=false',
])

k8s_resource(workload='jaeger', port_forwards=16686)
