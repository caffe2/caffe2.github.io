---
title: Caffe2 and PyTorch join forces to create a Research + Production platform PyTorch 1.0
layout: post
author: Caffe2 Team
category: blog
---
We'd like to share the plans for future Caffe2 evolution. Publicly open-sourced over a year ago, Caffe2 is a light-weight and modular framework that comes production-ready with ultimate scaling capabilities for training and deployment. Its mobile capabilities (Caffe2go) support all major generations of hardware and power one of the largest deployments of mobile deep learning with more than 1 billion devices. Over the past year, we worked with many industry partners to add Caffe2 support for their platform and guaranteed the best possible performance regardless of the platform you run on.

At Facebook, where Caffe2 originates, we support both PyTorch and Caffe2 for the wide range of AI use cases.  The main focus of Caffe2 development has been performance and cross-platform deployment whereas PyTorch has focused on flexibility for rapid prototyping and research.

In practice, any deep learning framework is a stack of multiple libraries and technologies operating at different abstraction layers (from data reading and visualization to high-performant compute kernels). Over the past year we saw more components of Caffe2 and PyTorch being shared (e.g. gloo, NNPACK, etc). Also, with our investment into interoperability, we built deep integration between frameworks using the shared [ONNX model format](http://onnx.ai/).

We realized that in order to deliver the best user experience, it makes sense to combine the beneficial traits of Caffe2 and PyTorch into a single package and enable a smooth transition from fast prototyping to fast execution. It'd also improve our developer efficiency by more easily utilizing a shared set of tools.

**Caffe2 and PyTorch projects are merging**. Over the next few months, we're planning to deeply integrate components of the frameworks and effectively unite them as a single package. It will combine the flexible user experience of the PyTorch frontend with scaling, deployment and embedding capabilities of the Caffe2 backend. Following is the high-level outline of the plan.

<!--truncate-->

## What's going to happen?

We've already merged [code repositories a month ago](https://github.com/pytorch/pytorch/issues/2439) to streamline some of the developer infrastructure tooling.  The following is an outline of our plans of the next months.

### Builds and packages

* In one of the next releases, python packages (in pip and conda) for Caffe2 and PyTorch will be merged into a single package providing union of the functionalities.
* We will continue to provide native library and python extensions as separate install options (which is the case for both Caffe2 and PyTorch today)
* All cross-compilation build modes and support for platforms of Caffe2 (iOS, Android, Raspbian, Tegra, etc) will remain intact and we will continue to expand various platforms support.

### Model authoring (frontend)

* Caffe2's graph construction APIs ([`brew`](https://caffe2.ai/docs/brew.html), `core.Net`) will continue to work and we'd provide backward compatibility for existing serialized model NetDefs for the changing functionalities during the refactoring.
* Going forward, [nn.Module-like](http://pytorch.org/docs/master/nn.html) abstractions would be preferred for constructing networks. We're augmenting PyTorch frontend abstractions with a so-called “hybrid frontend” that utilizes tracing and compilation capabilities to extract fully serialized model in graph format (compatible with Caffe2's NetDef and ONNX) that can be used for efficient deployment. Also, all of Caffe2 current and upcoming backend bindings and functionalities are going to be exposed through the unified hybrid frontend soon. Check out the [corresponding PyTorch blog](http://pytorch.org/2018/05/02/road-to-1.0.html) for more details on how hybrid frontend is going to look.
* The set of operator implementations of Caffe2 and PyTorch will be merged over time thus expanding functionality of both.
* ONNX model format is natively supported for both export and import in Caffe2 and PyTorch today. As we unify the codebases we're using ONNX as a common model representation and the means to express dynamic model nature suitable for optimization. Thus PyTorch 1.0 will be able to support ONNX natively and interface with other framework or accelerated libraries both for ingesting and emitting models.

### Scaling and deployment

* Caffe2's highly scalable execution engine (various accelerated backends and libraries integration and scalable graph executor) remain mostly intact and will gain ability to interoperate smoothly with Python program segments for rapid prototyping.
* Caffe2's existing predictor support will be the primary means of scalable native-only model deployment with accelerated hardware support both in datacenter and on mobile.

### Hardware integrations and accelerated libraries support

* We're going to make Caffe2's diverse devices support and runtime integrations available directly from the prototyping environment of the unified PyTorch 1.0 package.
* Integration interface for the libraries targeting accelerated hardware or complete graph runtimes would stay mostly **similar to the current Caffe2 code and existing integrations will continue to work**. Furthermore, for graph runtimes, we're working on formalizing the interaction interface with community initiatives like [ONNXIFI](https://github.com/onnx/onnx/pull/551/files).

## Timeline and further information

We're hoping to get to a production-ready first release this summer. However, as always, all of the development happens openly [on GitHub](https://github.com/pytorch/pytorch/) so you're welcome to follow along and contribute.

Given the ongoing merge of the projects, going forward we're going to unify announcements on [pytorch.org](http://pytorch.org/) and cross-reference them on [caffe2.ai](http://caffe2.ai).

Check out more details on the hybrid frontend and what benefits unification brings to the pytorch community [in the corresponding blog](http://pytorch.org/2018/05/02/road-to-1.0.html).
