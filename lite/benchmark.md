# benchmark

* https://ai.google.dev/edge/litert/models/measurement#native_benchmark_binary
* https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/tools/benchmark#profiling-model-operators


## x86 examples

```
/data/tinyai/liteRT/benchmarks/bencTool
========================================
./linux_x86-64_benchmark_model --graph=../tflite/efficientdet-tflite-lite0-detection-default-v1/1.tflite 
INFO: STARTING!
INFO: Log parameter values verbosely: [0]
INFO: Graph: [../tflite/efficientdet-tflite-lite0-detection-default-v1/1.tflite]
INFO: Signature to run: []
INFO: Loaded model ../tflite/efficientdet-tflite-lite0-detection-default-v1/1.tflite
INFO: Created TensorFlow Lite XNNPACK delegate for CPU.
INFO: The input model file size (MB): 4.56118
INFO: Initialized session in 52.687ms.
INFO: Running benchmark for at least 1 iterations and at least 0.5 seconds but terminate if exceeding 150 seconds.
INFO: count=35 first=19105 curr=13909 min=13585 max=19105 avg=14452.5 std=1240

INFO: Running benchmark for at least 50 iterations and at least 1 seconds but terminate if exceeding 150 seconds.
INFO: count=70 first=14941 curr=14066 min=13728 max=16145 avg=14290.9 std=452

INFO: Inference timings in us: Init: 52687, First inference: 19105, Warmup (avg): 14452.5, Inference (avg): 14290.9
INFO: Note: as the benchmark tool itself affects memory footprint, the following is only APPROXIMATE to the actual memory footprint of the model at runtime. Take the information at your discretion.
INFO: Memory footprint delta from the start of the tool (MB): init=21.9492 overall=34.5234


```

enable_op_profiling=true

```

./linux_x86-64_benchmark_model --graph=../tflite/efficientdet-tflite-lite0-detection-default-v1/1.tflite --enable_op_profiling=true
INFO: STARTING!
INFO: Log parameter values verbosely: [0]
INFO: Graph: [../tflite/efficientdet-tflite-lite0-detection-default-v1/1.tflite]
INFO: Signature to run: []
INFO: Enable op profiling: [1]
INFO: Loaded model ../tflite/efficientdet-tflite-lite0-detection-default-v1/1.tflite
INFO: Created TensorFlow Lite XNNPACK delegate for CPU.
INFO: The input model file size (MB): 4.56118
INFO: Initialized session in 32.163ms.
INFO: Running benchmark for at least 1 iterations and at least 0.5 seconds but terminate if exceeding 150 seconds.
INFO: count=32 first=19834 curr=15648 min=14936 max=21608 avg=15997.4 std=1663

INFO: Running benchmark for at least 50 iterations and at least 1 seconds but terminate if exceeding 150 seconds.
INFO: count=64 first=16067 curr=15102 min=14661 max=17579 avg=15517.6 std=551

INFO: Inference timings in us: Init: 32163, First inference: 19834, Warmup (avg): 15997.4, Inference (avg): 15517.6
INFO: Note: as the benchmark tool itself affects memory footprint, the following is only APPROXIMATE to the actual memory footprint of the model at runtime. Take the information at your discretion.
INFO: Memory footprint delta from the start of the tool (MB): init=22.0273 overall=34.8281
INFO: Profiling Info for Benchmark Initialization:
============================== Run Order ==============================
                                     [node type]          [first]        [avg ms]            [%]          [cdf%]          [mem KB]        [times called]  [Name]
                         ModifyGraphWithDelegate            6.348           6.348        55.640%         55.640%          7148.000                1       ModifyGraphWithDelegate/0
                                 AllocateTensors            5.061           5.061        44.360%        100.000%         10292.000                1       AllocateTensors/0

============================== Top by Computation Time ==============================
                                     [node type]          [first]        [avg ms]            [%]          [cdf%]          [mem KB]        [times called]  [Name]
                         ModifyGraphWithDelegate            6.348           6.348        55.640%         55.640%          7148.000                1       ModifyGraphWithDelegate/0
                                 AllocateTensors            5.061           5.061        44.360%        100.000%         10292.000                1       AllocateTensors/0

Number of nodes executed: 2
============================== Summary by node type ==============================
                                     [Node type]          [count]         [avg ms]          [avg %]         [cdf %]       [mem KB]        [times called]
                         ModifyGraphWithDelegate                1            6.348          55.640%         55.640%       7148.000                1
                                 AllocateTensors                1            5.061          44.360%        100.000%      10292.000                1

Timings (microseconds): count=1 curr=11409
Memory (bytes): count=0
2 nodes observed



INFO: Operator-wise Profiling Info for Regular Benchmark Runs:
============================== Run Order ==============================
                                     [node type]          [first]        [avg ms]            [%]          [cdf%]          [mem KB]        [times called]  [Name]
                                        QUANTIZE            0.199           0.203         1.328%          1.328%             0.000                1       [tfl.quantize]:0
                   Convolution (NHWC, QC8) IGEMM            0.398           0.407         2.658%          3.986%             0.000                1       Delegate/Convolution (NHWC, QC8) IGEMM:0
                  Convolution (NHWC, QC8) DWConv            0.428           0.051         4.317%          8.304%             0.000               13       Delegate/Convolution (NHWC, QC8) DWConv:1
                    Convolution (NHWC, QC8) GEMM            0.125           0.023         1.944%         10.248%             0.000               13       Delegate/Convolution (NHWC, QC8) GEMM:2
                    Convolution (NHWC, QC8) GEMM            0.464           0.473         3.087%         13.334%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:3
                  Convolution (NHWC, QC8) DWConv            0.385           0.320         2.088%         15.423%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:4
                    Convolution (NHWC, QC8) GEMM            0.110           0.109         0.709%         16.132%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:5
                    Convolution (NHWC, QC8) GEMM            0.203           0.066         1.713%         17.845%             0.000                4       Delegate/Convolution (NHWC, QC8) GEMM:6
                  Convolution (NHWC, QC8) DWConv            0.455           0.258         3.376%         21.221%             0.000                2       Delegate/Convolution (NHWC, QC8) DWConv:7
                    Convolution (NHWC, QC8) GEMM            0.146           0.092         1.203%         22.424%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:8
                                   Add (ND, QS8)            0.024           0.024         0.156%         22.580%             0.000                1       Delegate/Add (ND, QS8):9
                    Convolution (NHWC, QC8) GEMM            0.206           0.060         1.579%         24.159%             0.000                4       Delegate/Convolution (NHWC, QC8) GEMM:10
                  Convolution (NHWC, QC8) DWConv            0.273           0.169         2.212%         26.371%             0.000                2       Delegate/Convolution (NHWC, QC8) DWConv:11
                    Convolution (NHWC, QC8) GEMM            0.053           0.048         0.622%         26.993%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:12
                    Convolution (NHWC, QC8) GEMM            0.108           0.108         0.707%         27.700%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:13
                  Convolution (NHWC, QC8) DWConv            0.437           0.462         3.020%         30.720%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:14
                    Convolution (NHWC, QC8) GEMM            0.082           0.084         0.551%         31.271%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:15
                                   Add (ND, QS8)            0.009           0.003         0.061%         31.332%             0.000                3       Delegate/Add (ND, QS8):16
                    Convolution (NHWC, QC8) GEMM            0.107           0.111         0.722%         32.054%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:17
                  Convolution (NHWC, QC8) DWConv            0.046           0.050         0.326%         32.380%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:18
                    Convolution (NHWC, QC8) GEMM            0.036           0.036         0.235%         32.615%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:19
                    Convolution (NHWC, QC8) GEMM            0.085           0.087         0.571%         33.186%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:20
                  Convolution (NHWC, QC8) DWConv            0.090           0.054         0.709%         33.894%             0.000                2       Delegate/Convolution (NHWC, QC8) DWConv:21
                    Convolution (NHWC, QC8) GEMM            0.066           0.039         0.508%         34.402%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:22
                                   Add (ND, QS8)            0.004           0.004         0.028%         34.430%             0.000                1       Delegate/Add (ND, QS8):23
                    Convolution (NHWC, QC8) GEMM            0.084           0.048         0.632%         35.062%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:24
                  Convolution (NHWC, QC8) DWConv            0.090           0.056         0.738%         35.799%             0.000                2       Delegate/Convolution (NHWC, QC8) DWConv:25
                    Convolution (NHWC, QC8) GEMM            0.065           0.039         0.510%         36.309%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:26
                                   Add (ND, QS8)            0.004           0.004         0.028%         36.337%             0.000                1       Delegate/Add (ND, QS8):27
                    Convolution (NHWC, QC8) GEMM            0.084           0.049         0.641%         36.978%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:28
                  Convolution (NHWC, QC8) DWConv            0.215           0.121         1.586%         38.564%             0.000                2       Delegate/Convolution (NHWC, QC8) DWConv:29
                    Convolution (NHWC, QC8) GEMM            0.092           0.052         0.677%         39.240%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:30
                    Convolution (NHWC, QC8) GEMM            0.153           0.158         1.031%         40.271%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:31
                  Convolution (NHWC, QC8) DWConv            0.346           0.319         2.086%         42.357%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:32
                    Convolution (NHWC, QC8) GEMM            0.127           0.131         0.854%         43.210%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:33
                                   Add (ND, QS8)            0.006           0.006         0.041%         43.251%             0.000                1       Delegate/Add (ND, QS8):34
                    Convolution (NHWC, QC8) GEMM            0.173           0.155         1.015%         44.267%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:35
                  Convolution (NHWC, QC8) DWConv            0.315           0.309         2.021%         46.287%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:36
                    Convolution (NHWC, QC8) GEMM            0.132           0.129         0.843%         47.130%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:37
                                   Add (ND, QS8)            0.006           0.006         0.040%         47.170%             0.000                1       Delegate/Add (ND, QS8):38
                    Convolution (NHWC, QC8) GEMM            0.159           0.157         1.025%         48.195%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:39
                  Convolution (NHWC, QC8) DWConv            0.091           0.081         0.528%         48.723%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:40
                    Convolution (NHWC, QC8) GEMM            0.062           0.061         0.398%         49.121%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:41
                    Convolution (NHWC, QC8) GEMM            0.115           0.061         0.792%         49.912%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:42
                  Convolution (NHWC, QC8) DWConv            0.136           0.069         0.908%         50.820%             0.000                2       Delegate/Convolution (NHWC, QC8) DWConv:43
                    Convolution (NHWC, QC8) GEMM            0.104           0.054         0.707%         51.527%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:44
                                   Add (ND, QS8)            0.003           0.003         0.019%         51.545%             0.000                1       Delegate/Add (ND, QS8):45
                    Convolution (NHWC, QC8) GEMM            0.116           0.060         0.778%         52.323%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:46
                  Convolution (NHWC, QC8) DWConv            0.136           0.070         0.908%         53.231%             0.000                2       Delegate/Convolution (NHWC, QC8) DWConv:47
                    Convolution (NHWC, QC8) GEMM            0.103           0.054         0.701%         53.932%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:48
                                   Add (ND, QS8)            0.003           0.003         0.018%         53.950%             0.000                1       Delegate/Add (ND, QS8):49
                    Convolution (NHWC, QC8) GEMM            0.117           0.060         0.778%         54.728%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:50
                  Convolution (NHWC, QC8) DWConv            0.136           0.071         0.928%         55.657%             0.000                2       Delegate/Convolution (NHWC, QC8) DWConv:51
                    Convolution (NHWC, QC8) GEMM            0.100           0.053         0.697%         56.354%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:52
                                   Add (ND, QS8)            0.003           0.003         0.018%         56.372%             0.000                1       Delegate/Add (ND, QS8):53
                    Convolution (NHWC, QC8) GEMM            0.155           0.060         0.785%         57.158%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:54
                  Convolution (NHWC, QC8) DWConv            0.056           0.031         0.406%         57.563%             0.000                2       Delegate/Convolution (NHWC, QC8) DWConv:55
                    Convolution (NHWC, QC8) GEMM            0.172           0.088         1.153%         58.716%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:56
                    Convolution (NHWC, QC8) GEMM            0.010           0.011         0.069%         58.785%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:57
                    Convolution (NHWC, QC8) GEMM            0.010           0.023         0.295%         59.080%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:58
                    Convolution (NHWC, QC8) GEMM            0.016           0.016         0.102%         59.183%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:59
                    Convolution (NHWC, QC8) GEMM            0.015           0.015         0.098%         59.280%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:60
                    Convolution (NHWC, QC8) GEMM            0.031           0.032         0.208%         59.489%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:61
                    Convolution (NHWC, QC8) GEMM            0.010           0.005         0.072%         59.561%             0.000                2       Delegate/Convolution (NHWC, QC8) GEMM:62
                          Max Pooling (NHWC, S8)            0.001           0.001         0.008%         59.569%             0.000                1       Delegate/Max Pooling (NHWC, S8):63
                          Max Pooling (NHWC, S8)            0.000           0.000         0.001%         59.569%             0.000                1       Delegate/Max Pooling (NHWC, S8):64
                         RESIZE_NEAREST_NEIGHBOR            0.002           0.002         0.014%         59.583%             0.000                1       [fpn_cells/cell_0/fnode0/resample_1_4_5/ResizeNearestNeighbor]:66
                                   Add (ND, QS8)            0.000           0.005         0.411%         59.995%             0.000               12       Delegate/Add (ND, QS8):0
                                   Add (ND, QS8)            0.000           0.002         0.093%         60.088%             0.000                9       Delegate/Add (ND, QS8):3
                         RESIZE_NEAREST_NEIGHBOR            0.002           0.002         0.012%         60.100%             0.000                1       [fpn_cells/cell_0/fnode1/resample_1_5_6/ResizeNearestNeighbor]:70
                    TFLite_Detection_PostProcess            3.894           3.653        23.862%         83.962%             0.000                1       [StatefulPartitionedCall:3, StatefulPartitionedCall:2, StatefulPartitionedCall:1, StatefulPartitionedCall:0]:266
                          Convert (NC, QS8, F32)            0.046           0.028         0.180%         84.142%             0.000                1       Delegate/Convert (NC, QS8, F32):113
                                   Copy (NC, X8)            0.007           0.006         0.037%         84.179%             0.000                1       Delegate/Copy (NC, X8):112
                                   Copy (NC, X8)            0.000           0.000         0.001%         84.181%             0.000                1       Delegate/Copy (NC, X8):111
                          Convert (NC, QS8, F32)            0.848           0.835         5.455%         89.636%             0.000                1       Delegate/Convert (NC, QS8, F32):110
                               Sigmoid (NC, QS8)            0.073           0.064         0.416%         90.053%             0.000                1       Delegate/Sigmoid (NC, QS8):109
                                   Copy (NC, X8)            0.125           0.103         0.675%         90.728%             0.000                1       Delegate/Copy (NC, X8):108
                                   Copy (NC, X8)            0.000           0.000         0.000%         90.728%             0.000                1       Delegate/Copy (NC, X8):107
                                   Copy (NC, X8)            0.000           0.000         0.000%         90.728%             0.000                1       Delegate/Copy (NC, X8):106
                                   Copy (NC, X8)            0.000           0.000         0.000%         90.728%             0.000                1       Delegate/Copy (NC, X8):105
                                   Copy (NC, X8)            0.000           0.000         0.000%         90.728%             0.000                1       Delegate/Copy (NC, X8):104
                                   Copy (NC, X8)            0.000           0.000         0.000%         90.728%             0.000                1       Delegate/Copy (NC, X8):103
                                   Copy (NC, X8)            0.000           0.000         0.000%         90.728%             0.000                1       Delegate/Copy (NC, X8):102
                                   Copy (NC, X8)            0.000           0.000         0.000%         90.728%             0.000                1       Delegate/Copy (NC, X8):101
                                   Copy (NC, X8)            0.000           0.000         0.000%         90.728%             0.000                1       Delegate/Copy (NC, X8):100
                                   Copy (NC, X8)            0.000           0.000         0.000%         90.728%             0.000                1       Delegate/Copy (NC, X8):99
                    Convolution (NHWC, QC8) GEMM            0.007           0.007         0.045%         90.773%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:98
                  Convolution (NHWC, QC8) DWConv            0.000           0.000         0.000%         90.773%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:97
                    Convolution (NHWC, QC8) GEMM            0.000           0.000         0.001%         90.774%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:96
                  Convolution (NHWC, QC8) DWConv            0.000           0.000         0.000%         90.774%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:95
                    Convolution (NHWC, QC8) GEMM            0.000           0.000         0.003%         90.777%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:94
                  Convolution (NHWC, QC8) DWConv            0.000           0.000         0.001%         90.778%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:93
                    Convolution (NHWC, QC8) GEMM            0.000           0.000         0.001%         90.779%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:92
                  Convolution (NHWC, QC8) DWConv            0.000           0.000         0.000%         90.779%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:91
                    Convolution (NHWC, QC8) GEMM            0.000           0.000         0.001%         90.780%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:90
                  Convolution (NHWC, QC8) DWConv            0.000           0.000         0.000%         90.780%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:89
                    Convolution (NHWC, QC8) GEMM            0.000           0.000         0.002%         90.782%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:88
                  Convolution (NHWC, QC8) DWConv            0.001           0.000         0.001%         90.783%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:87
                    Convolution (NHWC, QC8) GEMM            0.000           0.000         0.001%         90.784%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:86
                  Convolution (NHWC, QC8) DWConv            0.000           0.000         0.000%         90.784%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:85
                    Convolution (NHWC, QC8) GEMM            0.000           0.000         0.000%         90.785%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:84
                  Convolution (NHWC, QC8) DWConv            0.000           0.000         0.000%         90.785%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:83
                    Convolution (NHWC, QC8) GEMM            0.000           0.000         0.001%         90.786%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:82
                  Convolution (NHWC, QC8) DWConv            0.000           0.000         0.001%         90.786%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:81
                                   Add (ND, QS8)            0.000           0.000         0.000%         90.786%             0.000                1       Delegate/Add (ND, QS8):80
                          Max Pooling (NHWC, S8)            0.000           0.000         0.000%         90.786%             0.000                1       Delegate/Max Pooling (NHWC, S8):79
                    Convolution (NHWC, QC8) GEMM            0.012           0.011         0.072%         90.858%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:78
                  Convolution (NHWC, QC8) DWConv            0.001           0.001         0.006%         90.865%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:77
                    Convolution (NHWC, QC8) GEMM            0.001           0.001         0.007%         90.871%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:76
                  Convolution (NHWC, QC8) DWConv            0.001           0.001         0.007%         90.878%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:75
                    Convolution (NHWC, QC8) GEMM            0.001           0.001         0.006%         90.885%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:74
                  Convolution (NHWC, QC8) DWConv            0.001           0.001         0.005%         90.890%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:73
                    Convolution (NHWC, QC8) GEMM            0.001           0.001         0.006%         90.896%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:72
                  Convolution (NHWC, QC8) DWConv            0.001           0.001         0.007%         90.903%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:71
                    Convolution (NHWC, QC8) GEMM            0.001           0.000         0.002%         90.905%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:70
                  Convolution (NHWC, QC8) DWConv            0.001           0.001         0.006%         90.911%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:69
                    Convolution (NHWC, QC8) GEMM            0.001           0.001         0.006%         90.917%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:68
                  Convolution (NHWC, QC8) DWConv            0.001           0.001         0.004%         90.921%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:67
                    Convolution (NHWC, QC8) GEMM            0.001           0.001         0.005%         90.926%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:66
                  Convolution (NHWC, QC8) DWConv            0.001           0.001         0.007%         90.933%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:65
                    Convolution (NHWC, QC8) GEMM            0.001           0.001         0.006%         90.938%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:64
                  Convolution (NHWC, QC8) DWConv            0.001           0.001         0.007%         90.945%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:63
                  Convolution (NHWC, QC8) DWConv            0.001           0.001         0.007%         90.952%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:61
                                   Add (ND, QS8)            0.000           0.000         0.000%         90.952%             0.000                1       Delegate/Add (ND, QS8):60
                          Max Pooling (NHWC, S8)            0.000           0.000         0.000%         90.952%             0.000                1       Delegate/Max Pooling (NHWC, S8):59
                  Convolution (NHWC, QC8) DWConv            0.003           0.003         0.021%         90.973%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:57
                  Convolution (NHWC, QC8) DWConv            0.005           0.003         0.021%         90.994%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:53
                  Convolution (NHWC, QC8) DWConv            0.005           0.004         0.023%         91.017%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:49
                  Convolution (NHWC, QC8) DWConv            0.005           0.003         0.021%         91.038%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:45
                  Convolution (NHWC, QC8) DWConv            0.005           0.004         0.023%         91.061%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:41
                                   Add (ND, QS8)            0.001           0.001         0.008%         91.069%             0.000                1       Delegate/Add (ND, QS8):40
                          Max Pooling (NHWC, S8)            0.003           0.001         0.008%         91.077%             0.000                1       Delegate/Max Pooling (NHWC, S8):39
                    Convolution (NHWC, QC8) GEMM            0.151           0.132         0.864%         91.941%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:38
                  Convolution (NHWC, QC8) DWConv            0.019           0.014         0.089%         92.030%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:37
                    Convolution (NHWC, QC8) GEMM            0.012           0.010         0.066%         92.097%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:36
                  Convolution (NHWC, QC8) DWConv            0.018           0.014         0.089%         92.185%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:35
                    Convolution (NHWC, QC8) GEMM            0.012           0.010         0.066%         92.251%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:34
                  Convolution (NHWC, QC8) DWConv            0.020           0.014         0.088%         92.340%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:33
                    Convolution (NHWC, QC8) GEMM            0.010           0.010         0.067%         92.406%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:32
                  Convolution (NHWC, QC8) DWConv            0.013           0.014         0.090%         92.497%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:31
                         RESIZE_NEAREST_NEIGHBOR            0.005           0.005         0.036%         92.532%             0.000                1       [fpn_cells/cell_0/fnode2/resample_1_6_7/ResizeNearestNeighbor]:74
                         RESIZE_NEAREST_NEIGHBOR            0.020           0.021         0.137%         92.669%             0.000                1       [fpn_cells/cell_0/fnode3/resample_1_7_8/ResizeNearestNeighbor]:78
                          Max Pooling (NHWC, S8)            0.004           0.004         0.058%         92.727%             0.000                2       Delegate/Max Pooling (NHWC, S8):3
                                   Add (ND, QS8)            0.004           0.004         0.052%         92.779%             0.000                2       Delegate/Add (ND, QS8):4
                  Convolution (NHWC, QC8) DWConv            0.013           0.028         0.543%         93.322%             0.000                3       Delegate/Convolution (NHWC, QC8) DWConv:5
                          Max Pooling (NHWC, S8)            0.001           0.001         0.015%         93.337%             0.000                2       Delegate/Max Pooling (NHWC, S8):7
                                   Add (ND, QS8)            0.001           0.001         0.013%         93.350%             0.000                2       Delegate/Add (ND, QS8):8
                  Convolution (NHWC, QC8) DWConv            0.005           0.021         0.407%         93.758%             0.000                3       Delegate/Convolution (NHWC, QC8) DWConv:9
                          Max Pooling (NHWC, S8)            0.000           0.000         0.000%         93.758%             0.000                2       Delegate/Max Pooling (NHWC, S8):11
                                   Add (ND, QS8)            0.000           0.000         0.000%         93.758%             0.000                2       Delegate/Add (ND, QS8):12
                  Convolution (NHWC, QC8) DWConv            0.001           0.019         0.378%         94.136%             0.000                3       Delegate/Convolution (NHWC, QC8) DWConv:13
                    Convolution (NHWC, QC8) GEMM            0.015           0.014         0.280%         94.416%             0.000                3       Delegate/Convolution (NHWC, QC8) GEMM:14
                          Max Pooling (NHWC, S8)            0.000           0.000         0.000%         94.416%             0.000                2       Delegate/Max Pooling (NHWC, S8):15
                  Convolution (NHWC, QC8) DWConv            0.001           0.019         0.364%         94.780%             0.000                3       Delegate/Convolution (NHWC, QC8) DWConv:17
                    Convolution (NHWC, QC8) GEMM            0.001           0.170         3.330%         98.110%             0.000                3       Delegate/Convolution (NHWC, QC8) GEMM:18
                         RESIZE_NEAREST_NEIGHBOR            0.001           0.001         0.006%         98.116%             0.000                1       [fpn_cells/cell_1/fnode0/resample_1_4_5/ResizeNearestNeighbor]:101
                         RESIZE_NEAREST_NEIGHBOR            0.002           0.002         0.011%         98.127%             0.000                1       [fpn_cells/cell_1/fnode1/resample_1_5_6/ResizeNearestNeighbor]:105
                         RESIZE_NEAREST_NEIGHBOR            0.006           0.005         0.035%         98.163%             0.000                1       [fpn_cells/cell_1/fnode2/resample_1_6_7/ResizeNearestNeighbor]:109
                         RESIZE_NEAREST_NEIGHBOR            0.022           0.021         0.135%         98.297%             0.000                1       [fpn_cells/cell_1/fnode3/resample_1_7_8/ResizeNearestNeighbor]:113
                         RESIZE_NEAREST_NEIGHBOR            0.001           0.001         0.006%         98.303%             0.000                1       [fpn_cells/cell_2/fnode0/resample_1_4_5/ResizeNearestNeighbor]:136
                         RESIZE_NEAREST_NEIGHBOR            0.002           0.002         0.011%         98.315%             0.000                1       [fpn_cells/cell_2/fnode1/resample_1_5_6/ResizeNearestNeighbor]:140
                         RESIZE_NEAREST_NEIGHBOR            0.006           0.006         0.037%         98.351%             0.000                1       [fpn_cells/cell_2/fnode2/resample_1_6_7/ResizeNearestNeighbor]:144
                         RESIZE_NEAREST_NEIGHBOR            0.024           0.022         0.141%         98.493%             0.000                1       [fpn_cells/cell_2/fnode3/resample_1_7_8/ResizeNearestNeighbor]:148
                  Convolution (NHWC, QC8) DWConv            0.055           0.056         0.365%         98.858%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:3
                    Convolution (NHWC, QC8) GEMM            0.043           0.041         0.268%         99.126%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:4
                  Convolution (NHWC, QC8) DWConv            0.013           0.014         0.090%         99.216%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:27
                  Convolution (NHWC, QC8) DWConv            0.013           0.013         0.088%         99.304%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:23
                                   Add (ND, QS8)            0.004           0.004         0.027%         99.331%             0.000                1       Delegate/Add (ND, QS8):20
                  Convolution (NHWC, QC8) DWConv            0.053           0.055         0.361%         99.693%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:15
                    Convolution (NHWC, QC8) GEMM            0.041           0.041         0.267%         99.960%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:16
                          Max Pooling (NHWC, S8)            0.009           0.006         0.040%        100.000%             0.000                1       Delegate/Max Pooling (NHWC, S8):19

============================== Top by Computation Time ==============================
                                     [node type]          [first]        [avg ms]            [%]          [cdf%]          [mem KB]        [times called]  [Name]
                    TFLite_Detection_PostProcess            3.894           3.653        23.862%         23.862%             0.000                1       [StatefulPartitionedCall:3, StatefulPartitionedCall:2, StatefulPartitionedCall:1, StatefulPartitionedCall:0]:266
                          Convert (NC, QS8, F32)            0.848           0.835         5.455%         29.317%             0.000                1       Delegate/Convert (NC, QS8, F32):110
                    Convolution (NHWC, QC8) GEMM            0.464           0.473         3.087%         32.404%             0.000                1       Delegate/Convolution (NHWC, QC8) GEMM:3
                  Convolution (NHWC, QC8) DWConv            0.437           0.462         3.020%         35.424%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:14
                   Convolution (NHWC, QC8) IGEMM            0.398           0.407         2.658%         38.082%             0.000                1       Delegate/Convolution (NHWC, QC8) IGEMM:0
                  Convolution (NHWC, QC8) DWConv            0.385           0.320         2.088%         40.170%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:4
                  Convolution (NHWC, QC8) DWConv            0.346           0.319         2.086%         42.256%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:32
                  Convolution (NHWC, QC8) DWConv            0.315           0.309         2.021%         44.276%             0.000                1       Delegate/Convolution (NHWC, QC8) DWConv:36
                  Convolution (NHWC, QC8) DWConv            0.455           0.258         3.376%         47.652%             0.000                2       Delegate/Convolution (NHWC, QC8) DWConv:7
                                        QUANTIZE            0.199           0.203         1.328%         48.980%             0.000                1       [tfl.quantize]:0

Number of nodes executed: 171
============================== Summary by node type ==============================
                                     [Node type]          [count]         [avg ms]          [avg %]         [cdf %]       [mem KB]        [times called]
                    Convolution (NHWC, QC8) GEMM               62            5.236          34.361%         34.361%          0.000              101
                  Convolution (NHWC, QC8) DWConv               51            4.460          29.269%         63.630%          0.000               80
                    TFLite_Detection_PostProcess                1            3.653          23.973%         87.603%          0.000                1
                          Convert (NC, QS8, F32)                2            0.862           5.657%         93.260%          0.000                2
                   Convolution (NHWC, QC8) IGEMM                1            0.406           2.664%         95.925%          0.000                1
                                        QUANTIZE                1            0.203           1.332%         97.257%          0.000                1
                                   Add (ND, QS8)               18            0.148           0.971%         98.228%          0.000               42
                                   Copy (NC, X8)               12            0.108           0.709%         98.937%          0.000               12
                         RESIZE_NEAREST_NEIGHBOR               12            0.081           0.532%         99.468%          0.000               12
                               Sigmoid (NC, QS8)                1            0.063           0.413%         99.882%          0.000                1
                          Max Pooling (NHWC, S8)               10            0.018           0.118%        100.000%          0.000               14

Timings (microseconds): count=64 first=15808 curr=14892 min=14470 max=17363 avg=15309.2 std=542
Memory (bytes): count=0
171 nodes observed

```