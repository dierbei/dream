## 代码
```go
import (
	"fmt"

	"awesomeProject/informer/2/lib"

	corev1 "k8s.io/api/core/v1"
	"k8s.io/apimachinery/pkg/fields"
	"k8s.io/client-go/tools/cache"
)

func main() {
	_client := lib.InitClient()
	store := cache.NewStore(cache.MetaNamespaceKeyFunc)

	podListWatch := cache.NewListWatchFromClient(_client.CoreV1().RESTClient(), "pods", "default", fields.Everything())
	df := cache.NewDeltaFIFOWithOptions(cache.DeltaFIFOOptions{
		KeyFunction:  cache.MetaNamespaceKeyFunc,
		KnownObjects: store,
	})
	rf := cache.NewReflector(podListWatch, &corev1.Pod{}, df, 0)
	ch := make(chan struct{})
	go func() {
		rf.Run(ch)
	}()

	for {
		df.Pop(func(obj interface{}) error {
			for _, delta := range obj.(cache.Deltas) {
				fmt.Println(delta.Type, ":", delta.Object.(*corev1.Pod).Name,
					":", delta.Object.(*corev1.Pod).Status.Phase)
				switch delta.Type {
				case cache.Sync, cache.Added:
					store.Add(delta.Object)
				case cache.Updated:
					store.Update(delta.Object)
				case cache.Deleted:
					store.Delete(delta.Object)
				}

			}
			return nil
		})
	}
}
```