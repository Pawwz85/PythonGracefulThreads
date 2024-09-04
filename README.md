# PythonGracefulThreads

**PythonGracefulThreads** is a simple, single-file implementation for creating service threads that can be stopped gracefully.

## Example Usage

### 1. Creating a Service that can be stopped gracefully:

```python
import GracefulThreads
from threading import Thread
import time

@GracefulThreads.GracefulThread
class SomeService(Thread):
    def __init__(self):
        # Initialization goes here
        super().__init__()

    @GracefulThreads.loop_forever_gracefully
    def run(self):
        time.sleep(10)
        # Job implementation goes here
```

### 2. Start service:
```python
service = SomeService()
service.start();
```

### 3. stopping service:
 ```python
service.stop()
service.join()
```
### If you want to stop service when main proces terminate register signal handlers:
```python
 service.start()
 def stop_service(signum, frame):
        print("stopping...")
        service.stop()
        print("Killing main process in 10s")
        time.sleep(10)
        os.kill(os.getpid(), signal.SIGINT)

  signal.signal(signal.SIGINT, stop_service)
  signal.signal(signal.SIGTERM, stop_service)
  service.join()
```
