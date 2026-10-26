# Make them executable
chmod +x k8s-native-rollout-strategies.sh
chmod +x k8s-bluegreen-canary.sh

# Run (optionally set a different namespace)
./k8s-native-rollout-strategies.sh
./k8s-bluegreen-canary.sh

# Or with a custom namespace
NAMESPACE=my-app ./k8s-bluegreen-canary.sh




Workload Type,Preferred Strategy,Why
Customer-facing APIs / high traffic,Controlled Rolling or Blue/Green,Lowest risk + observability
Critical / regulated systems,Blue/Green,"Instant rollback, full isolation"
Internal tools / batch / jobs,Recreate,"Simple, acceptable downtime"
Most microservices,Controlled Rolling (maxSurge=1),Best balance of safety vs speed


File,Strategy,Purpose
production-ramped-rollout.sh,Controlled Rolling (maxSurge=1),Safest default for most services
production-blue-green.sh,Blue/Green,Instant switch + instant rollback
production-recreate.sh,Recreate,Full downtime (batch/internal only)


# Make executable (if needed)
chmod +x production-*.sh

# Run with defaults
./production-ramped-rollout.sh
./production-blue-green.sh
./production-recreate.sh

# Or override variables
NAMESPACE=staging APP_NAME=my-service IMAGE=myreg.io/app:v1.2.3 ./production-ramped-rollout.sh

NAMESPACE=prod APP_NAME=checkout \
  BLUE_IMAGE=myreg.io/checkout:v3.1.0 \
  GREEN_IMAGE=myreg.io/checkout:v3.2.0 \
  ./production-blue-green.sh
