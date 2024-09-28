# py-lite

* All you need is a TensorFlow model converted to TensorFlow Lite
* install just the LiteRT interpreter - tflite_runtime
* If the models have any dependencies to the Select TF opsor - install the full version : pip install tensorflow ;

```
import tflite_runtime.interpreter as tflite
interpreter = tflite.Interpreter(model_path=args.model_file)
```


* example label-image : https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/examples/python/