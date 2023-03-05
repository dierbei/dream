## 代码
```go
import (
	"log"
	
	"awesomeProject/informer/2/lib"
	
	corev1 "k8s.io/api/core/v1"
	metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
	"k8s.io/apimachinery/pkg/fields"
	"k8s.io/client-go/tools/cache"
)

func main() {
	_client := lib.InitClient()

	podListWatch := cache.NewListWatchFromClient(_client.CoreV1().RESTClient(), "pods", "default", fields.Everything())
	watcher, err := podListWatch.Watch(metav1.ListOptions{})
	if err != nil {
		log.Fatalln(err)
	}

	for {
		select {
		case v, ok := <-watcher.ResultChan():
			if ok {
				log.Println(v.Type, v.Object.(*corev1.Pod).Name)
			}
		}
	}

```