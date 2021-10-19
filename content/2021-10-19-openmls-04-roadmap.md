---
title: "OpenMLS v0.4 Roadmap"
date: 2021-10-19
tags: ["mls", "openmls", "roadmap"]
notoc: true
author: "Franziskus Kiefer"
author_link: "https://www.franziskuskiefer.de"
---

It's time for another update on OpenMLS because many things are happening behind the scenes.

Today we are excited to announce a public roadmap for OpenMLS v0.4. This will not even be close to a v1.0 release because the [spec](https://datatracker.ietf.org/doc/draft-ietf-mls-protocol/) is still not finished and it's unclear how the library will be used. Nonetheless will v0.4 be a significant release with a mostly stable API and most functionality being implemented.

Over the next five months we will fix the most pressing issues and make OpenMLS a usable MLS library for consumers to use. We are well aware that there is almost no experience with using MLS in a messaging product. (Cisco's Webex is rolling out MLS for [end-to-end encrypted video calls](https://www.btconferencing.com/downloads-library/services/webex-versions/t41/Webex_Latest_Channel_Customer_Monthly_Update_41.7.pdf) as part of their [zero-trust initiative](https://www.cisco.com/c/en/us/solutions/collateral/collaboration/white-paper-c11-744553.html) right now.) The goal is therefore to offer a mostly stable API and complete feature set for consumers to start using it. However, we expect a significant feedback cycle to improve the APIs to make OpenMLS better suited for applications.

# 🛣 The road to v0.4

There are a number of high level goals we are tackling over the coming months.

You can follow the road to v0.4 on the [Github milestone](https://github.com/openmls/openmls/milestone/3).

## 💌 Validation & Authorization

This milestone tackles two issues that aren't very well specified in the MLS specification; Validation and Authorization.

Validation ensures that group and application messages are "valid". This includes a number of steps:

- Syntax validation to ensure that messages are well formed.
- Semantic validation makes sure that messages are valid in a
  given context. This includes signature verification, epoch number checks, etc.
- Group policy validation establishes that the group policy, defining things like handshake type etc, is being adhered to.
- The authentication service and policy validation checks to see whether syntactically and semantically correct messages should be adopted or dropped by answering questions such as: Is a member allowed to add another member? Is a member allowed to remove another member?

## ⚙️ Supported Platforms

The goal of OpenMLS is to support all relevant architectures and operating systems. This includes the major operating systems (Windows, macOS, Linux, Android, iOS) on all commonly used hardware architectures (x86, x86_64, arm64, arm32). Note that arm32 is a legacy platform and only supported on a best effort basis for old Android devices. Arm64 will be supported for all operating systems except Windows.

In addition OpenMLS can be used from JavaScript as a WebAssembly module. We don't have a JS API yet ([tracking issue #487](https://github.com/openmls/openmls/issues/487)). If you are interested in contributing, this would be a great starting point.

## 📜 Documentation & APIs

All high-level APIs that are interesting for consumers will be well documented and published.

Starting with v0.4 OpenMLS will adhere to [semantic versioning](https://semver.org/) guidelines and increase the minor version number on breaking changes. Note however that OpenMLS will still be pre-1.0 and see a significant number of changes.

### 🔐 Crypto backends

OpenMLS does not implement its own cryptographic primitives but uses other established libraries instead. In addition, MLS uses [HPKE](https://datatracker.ietf.org/doc/draft-irtf-cfrg-hpke/) for most of its asymmetric cryptography.

To allow flexible use cases OpenMLS will support the possibility for consumers to bring their own cryptographic primitives, random number generators, as well as a storage mechanisms for long term keys by implementing the respective trait.

## 👏🏻 Feature Complete

OpenMLS will support all features described in [draft-12](https://www.ietf.org/archive/id/draft-ietf-mls-protocol-12.html). At this point we expect draft-12 to be the last draft before the [WGLC](https://www.ietf.org/about/glossary/?query=wglc) such that the features implemented in v0.4 should be equivalent or very close to the final RFC.
