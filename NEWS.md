<!--- Licensed to the Apache Software Foundation (ASF) under one -->
<!--- or more contributor license agreements.  See the NOTICE file -->
<!--- distributed with this work for additional information -->
<!--- regarding copyright ownership.  The ASF licenses this file -->
<!--- to you under the Apache License, Version 2.0 (the -->
<!--- "License"); you may not use this file except in compliance -->
<!--- with the License.  You may obtain a copy of the License at -->

<!---   http://www.apache.org/licenses/LICENSE-2.0 -->

<!--- Unless required by applicable law or agreed to in writing, -->
<!--- software distributed under the License is distributed on an -->
<!--- "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY -->
<!--- KIND, either express or implied.  See the License for the -->
<!--- specific language governing permissions and limitations -->
<!--- under the License. -->

TVM Change Log
==============

This file records the changes in TVM library in reverse chronological order.

## On-going version

Refer to the Roadmap issue for complete list on on-going version features.
If you check in something that is not reflected in Roadmap issue, please reply
to that issue so it can get added.


## 0.5
This release features several major improvements. Some of the highlights are: Arbitrary bits quantization algorithm; High-level auto-differentiable programming IR -- Relay.

- Fully featured 8-bit network support
  - 8bit quantizer
  - Arbitrary bits quantization algorithm
  - Intel cpu support
  - ARM cpu support
- NVidia GPU 8-bit kernel
  - int8 gemm recipe
  - int8 conv2d
  - Autotvm integration
- Automated tuning and scheduling
  - AutoTVM optimizations for mobile GPUs
  - AutoTVM optimizations for CUDA
  - AutoTVM optimizations for x86
- Initial release of the differentiable programming IR, Relay
  - Generic & informative Relay error reporting #2408
  - Relay IR text format support #1781
  - Support control flows
  - A Normal Form Canonicalization #2251
  - Type system support
  - End to end compilation
     * Frontend support: Caffe2 #2507 , CoreML #2476 , Keras #2376 , MXNet #2163 , ONNX, TFLite #2365
     * Operator coverage #1799 #2051
  - FoldScaleAxis #2020
  - SimplifyInference #2033
  - CombineParallelConv2D #2089
  - InstrumentBoundCheckers pass #2079
  - Bind & FoldConstant #2100
  - Alter Op Layout #2150
  - General OpFusion #2090
- CodeGen
  - Gcc / g++ compatible C code generator for TVM #2161
  - Device type annotation for heterogeneous compilation #2361
  - Cache packed func ptr, lift alloca #2070
  - Generalize compute to tensor region #1476
- Runtime
  - Relay interpreter and compiler #1954
  - Heterogeneous runtime #1695
  - Language bindings: Golang runtime #1470 , Rust runtime #1597
  - Add min_repeat_ms to time_evaluator #2200
  - Bundled interpreter demonstration #2297
  - Enable PlanMemory in the graph runtime #2120
- Language Binding
  - Rust frontend #2292
- VTA
  - Improved RPC for VTA #2043
- Hybrid python programming model
  - Support for scheduling #2416
  - Support for Inter-function call  #2287
  - Backend support  #2477
- TOPI
  - Initial support for sparse tensor computation
  - Improve ARM CPU depthwise convolution performance #2345
  - Port winograd ops to relay #2356
  - Add faster-rcnn proposal op #2420
- Tutorials and docs
  - Relay language docs #2232
  - Tutorials on how to use SGX backend
  - How to write a pass in python
  - General lowering flow of TVM
  - How to do tensorize
  - TFLite frontend tutorial #2508
  - Keras seq2seq model for translation tutorial #1815
  - Committer guide and tips #2468
  - Code review guideline on API designs #2459



## 0.4

This release features several major improvements. The high-level graph optimizer is now part of TVM repo. Some of the highlights are: Initial support of AutoTVM for automated optimization; customized accelerator backend VTA.

- Tensor operator primitives
  - Introduce attrs field to operator primitives(e.g. compute) to store additional metadata, the attrs can be used as hint for scheduling
- Enable embedding of asm micro-kernels
- Hybrid python programming model
   - python AST based IR builder interface
   - support GPU programs
- AutoTVM, Automated tuning, and scheduling
   - basic autotvm infra
    - GPU IR verifier
   - basic autotuning tutorial
   - topi integration
- ARM support
    - winograd support
   - initial support of ARM autotuning records
- TOPI Vision
   - Generic GPU sort support(useful for vision)
   - SSD operator support
- TOPI numpy consistency
   - Rename all binary operators for numpy consistecy: broadcast_add-> add, broadcast_sub -> substract, broadcast_mul -> multiply, broadcast_div->divide
   - New operators: slice, LRN, equal, not_equal, less, greater
   - tutorials on topi
- Initial low-bit operator support support
    - Optimized popcount generation on ARM
    - general bit-serial convolution and GEMM
    - optimized low bit kernels
    - parallel optimization
- New topi backend optimization for intel graphics
- Adapt AVX schedules for SSE target
- VTA: customized accelerator backend
  - custom hardware backend example
  - tutorials on how to use customized accelerator
- Initial experimental support for  HLS backend
- Bugfix in SPIRV code generator for vulkan
- libdevice support, enable NVPTX backend
- Introduce NDArrayContainer for managed NDarray
- RPC and Device API
   - Support communication between big/small endian machines.
   - RPC and device API protocol upgrade (this is a non-backward compatible change) to support big-small endian communication. This is a non-backward compatible change, need to use the latest version of TVM runtime with the RPC
   - graduate rpc from contrib, tvm.contrib.rpc->tvm.rpc
   -Support tracker in Android RPC, add fault tolerance for AutoTVM
- BIG.LITTLE aware threadpool
- tvm4j graph runtime that runs end to end workload in java
- DLPack support
   - Support from_dlpack and to_dlpack
   - Enables bridges to pytorch
- Enable link of stackvm in runtime
- Tensorflow graphdef frontend
- Keras frontend
   - improved to support reuse layers, add activations
- ONNX
   - gather,  LRN
- CoreML frontend
   - Support C-RNN and activation functions
- Fix grads for sum and expand_like
- Enhanced operator fusion for multiple elemwise branches
- Separate nnvm fusion and compilation pass
- Unified build system to cmake, customizable cmake path for vulkan, rocm, cuda


## 0.3

This release features numerous improvements in TOPI and backends. We make the first step toward object detection support in TOPI, featuring operators necessary for YOLO and SSDs. The topi now supports numpy-style API and operator overloading. RPC is significantly improved to support resource allocation and using a pool of devices. We are adding two new backends: WebGL for running GPUs on the browser, and Vulkan for running on next-generation graphics API.

- TOPI Vision operators
   - SSD support
   - YOLO support
   - NMS operator support in vision
- TOPI general numpy-style operators
   - numpy style operator overload in topi
   - more operators: flip, take
   - dilation support on conv2d and depthwise
- 8bit support
    - ARM 8bit gemm
    - ARM 8bit conv
- Low bit operator support
    - popcount intrinsics
    - 1-bit fully connected
- Contrib: MPSDNN fully-connected and conv2d support
- Better RPC support
   - RPC Tracker support to allow centralized resource management
   - RPC protocol upgrade (this is a non-backward compatible change) to support timeout in the proxy
     - This is a breaking change, need to use the latest version of TVM runtime with the RPC
   - Fault-tolerant to early server termination with correct exception propagated
   - RPC support enabled for ROCm AMDGPUs
- Tutorials and docs
  - How to deploy to android devices.
- Optimizations for hardware backends
  - intel CPU (AVX and AVX512)
- Schedule Primitives
   - rfactor now support factor_axis to specify the factored dimension in the result
   - cache_write now support multiple output operators
   - enable warp memory which generates shuffle instructions
- Framework bridge
  - MXNet bridge supported
- C++ compiler API support
   - build migration
   - topi migration to c++
   - Target system in c++
- WebGL backend
   - runtime and codegen
   - topi integration
   - end to end pipeline on the browser
- Vulkan backend
   - vulkan runtime
   - spirv code generator
- Security
    - intel SGX runtime support
    - multi-threaded SGX runtime
- LLVM 7.0 support
- Robustness
   - VerifyMemory to verify incorrect GPU schedules that writes into GPU memory from cpu
   - Verify compute formulas
- Better CPU parallel runtime

## 0.2

This release comes with a complete set of TOPI support for NNVM compiler, which allows compilation of end to end workloads.
We also make major improvements in supporting new backends: ROCm for AMDGPUs and ARM GPU.

- Backend support
   - Support LLVM mainline(4.0, 5.0, 6.0)
   - Support ROCM stack for AMD GPUs
   - More robust OpenCL support for ARM GPUs
- Android RPC runtime
- Multi-threading optimization for ARM
   - multi-threaded depthwise
   - multi-threaded conv2d
- New schedule primitives
   - storage_align for shared memory alignment
   - double_buffer
- UnrollLoop : more robust version of unroll loop, count maximum steps that can be unrolled.
- Full set of TOPI operators
   - Introduce tvm.target to specify target options for compilation better.
   - broadcast/ reduction operators
   - pooling and global pooling
   - Generic target support for topi
   - schedule with external libraries
- End to end deep learning pipelines for CPU, GPU, ARM GPU
- Tutorials
  - How to load compiled module in any language runtime
  -  How to use java runtime
- Contrib library: MIOpen, CuDNN
- Ongoing items that contains functioning pieces
  - WebGL backend
  - C++ compiler support
  - MPS DNN
  - low bit support, introduced popcount


## 0.1

- Language runtime
    - python
    - javascript
    - java
    - c++
- Backend
    - arm, x86
    - javascript, wasm
    - CUDA
    - opencl
    - Metal
- DNN Library integration
- RPC  runtime
- TOPI operator pipeline python
- TOPI operator pipeline in C++
- Rough perf of the TOPI GPU pipeline
- Rough pref of TOPI CPU pipeline
- End to end graph executors


## Initial version

- Pack libary into shared library.
- External function and contrib libraries
- DLPack integration support
- AOT and module system
- Basic code structure ready.
