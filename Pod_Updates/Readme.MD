# Make them executable
chmod +x k8s-native-rollout-strategies.sh
chmod +x k8s-bluegreen-canary.sh

# Run (optionally set a different namespace)
./k8s-native-rollout-strategies.sh
./k8s-bluegreen-canary.sh

# Or with a custom namespace
NAMESPACE=my-app ./k8s-bluegreen-canary.sh
