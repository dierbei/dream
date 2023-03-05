## 1. in cluster
```go
func K8sRestConfigInPod() *rest.Config {
	config, err := rest.InClusterConfig()
	if err != nil {
		log.Fatal(err)
	}
	return config
}
```

## 2. out cluster
```go
func K8sRestConfig() *rest.Config {
	config, err := clientcmd.BuildConfigFromFlags("", "resource/config")
	if err != nil {
		log.Fatal(err)
	}
	return config
}
```