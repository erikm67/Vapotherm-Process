# Vapotherm Embedded Software Development Process

## Table of Contents

- [Overview](#overview)
- [Why Are We Doing This and Why Do We Want to Improve Process?](#why-are-we-doing-this-and-why-do-we-want-to-improve-process)
- [Regulatory Compliance Framework](#regulatory-compliance-framework)
- [Key Principles from "Patterns in the Machine"](#key-principles-from-patterns-in-the-machine)
- [Measuring Progress](#measuring-progress)
- [Development Process Phases](#development-process-phases)
  - [1. Software Development Planning](#1-software-development-planning)
  - [2. Software Requirements Specification](#2-software-requirements-specification)
  - [3. Software Architectural Design](#3-software-architectural-design)
  - [4. Software Detailed Design](#4-software-detailed-design)
  - [5. Software Implementation](#5-software-implementation)
  - [6. Software Verification](#6-software-verification)
  - [7. Software Validation](#7-software-validation)
  - [8. Software Maintenance and Configuration Management](#8-software-maintenance-and-configuration-management)
- [Risk Management Integration](#risk-management-integration)
- [Documentation Requirements](#documentation-requirements)
- [Continuous Improvement](#continuous-improvement)
- [Bibliography](#bibliography)

## Overview

These are only initial ideas made without much understanding current practices at Vapotherm.  These ideas may be completely reworked through discussions with leadership (Soundharya, Alvin), peers (Sila, Oskar) and team (Leo, Tianwei, Niall, David and Brian)

This document outlines the initial ideas for Vapotherm's embedded software development process for medical devices that complies with IEC 62304 (Medical device software — Software life cycle processes) and FDA software functions regulations. The process incorporates design patterns and best practices from John Taylor's "Patterns in the Machine: A Software Engineering Guide to Embedded Development," which emphasizes safety, reliability, and maintainability in embedded systems.

The point of these ideas is not that there is anything wrong with the current Vaportherm way of working.  A key idea of agile process is that teams are self governed and are constantly evaluating what works and what can be improved.

## Why Are We Doing This and Why Do We Want to Improve Process?

   1. We want to make great medical devices for our patients and customers.  
   1. Our devices help people who are sick and want to live the most normal life possible.  My wife's mother had a lung fibrosis.  She was able to use a high flow device in the acute setting so she could talk to visitors and at home and to be able to get out of the hospital.  It made a big difference.
   1. We want these devices to be easy to use with few bugs (high quality) so that they can deliver great therapy and provide useful information.
   1. We want to understand the software process so we can continually make it better in quality and speed.
   1. We want to deliver the software for these medical devices in a reproducible way that automates as much of the mundane as possible so we as software developers can focus on the innovative parts.
   1. As corny as it sounds, improving process improves our fun as devlopers in creating the software.  If we understand where the bottlenecks are we can fix them and get stuff done quickly and efficiently.  This maximizes our fun.

## Regulatory Compliance Framework

A good process is much more than this but at the core, our software process has to meet the regulatory standards and guidance.

### IEC 62304 Requirements

IEC 62304 classifies software based on safety risk:

- **Class A**: No injury or damage to health possible
- **Class B**: Non-serious injury possible
- **Class C**: Death or serious injury possible

The process addresses all lifecycle phases: development planning, requirements, architectural design, detailed design, implementation, verification, validation, and maintenance.

### FDA Software Functions

FDA regulations require:

- Risk-based approach to software development
- Verification and validation activities
- Traceability from requirements to testing
- Documentation of software design and testing
- Post-market surveillance and updates

## Key Principles from "Patterns in the Machine"

John Taylor's book provides patterns for embedded systems that enhance safety and reliability:

- **Safe State Machines**: Ensure system always in a valid state
- **Watchdog Patterns**: Monitor system health and recover from failures
- **Resource Management Patterns**: Prevent resource leaks and ensure deterministic behavior
- **Error Handling Patterns**: Graceful degradation and error recovery
- **Communication Patterns**: Reliable data exchange in distributed systems

These patterns are integrated throughout the development process to build robust, safety-critical software.

## Measuring Progress

> Lord Kelvin said "When you can measure what you are speaking about, and express it in
> numbers, you know something about it; but when you cannot measure it, when you cannot
> express it in numbers, your knowledge is of a meagre and unsatisfactory kind."

As we implement this process we need to measure our progress in delivering finished pieces of the software.  Using the words "we" and "our" is intentional.  We are not measuring individual progress because that does not matter.  What matters is what the team accomplishes.  Thinking about team progress fosters cooperation and sharing information.  This progress measure is for us to be able to see the positive effects of our development process improvements.  If we make things easier and more automated then our metrics will improve.

The scrum software development literature promotes the use of story points as a way for teams to measure progress.  As the development team we define what the story points measure.  Software developers (and other humans) are bad at measuring time.  We are better at measuring relative things, i.e. this is twice as hard as that.  If we define say 1 story point to be the effort (accomplishing the full definition of done) to deliver a trivial code change like say fixing a typo in a UI string then we can scale more complicated changes relative to that.  Typically we then do a Fibonacci sequence to avoid getting into splitting hairs like "is this 8 points or 9 points".  Fibonacci refresher: 1-2-3-5-8-13-21.  We will break up tasks if they get too big.  Sometimes it is helpful to think about real things like dogs "Is this a chihuahua effort or a great dane?"

The kanban literature prefers to focus more on cycle time, flow and throughput of work items through the system.  One possible problem with these metrics is if we are adding to our definition of done then it will falsely look like our throughput declines.

Also, there is power in each team member estimating the effort of a work item individually and then talking out the differences as a team.  If one person says it is a 1 and someone else says it is a 13 we probably have a problem with story definition or hidden surprises in the work.

A possible approach is to measure the combined story points or throughput of the whole embedded team, acute and home.  There will be two separate backlogs since there are two code bases.  For consistency, the Singapore team will primarily focus on home and vice versa but this will likely blend as we move forward.  It would be ideal to do backlog refinement and point estimation together (acute and home) but we will have to see if the logistics work.  Since we are a small group, the thought is that we will follow a kanban style workflow rather than full scrum but we can see what works best.

### Kanban Agile Workflow

- **Principles:** Visualize work, limit work-in-progress (WIP), manage flow, make policies explicit, and continuously improve.
- **Practices:** Use a shared Kanban board (Backlog → Ready → In Progress → Review → Done), set WIP limits per column, pull work when capacity allows, and track cycle time to identify bottlenecks.  From personal experience, this is a key.  We cannot get to a point where we have many WIP stories that are hanging.
- **Cadence:** Keep lightweight routines — short daily syncs and regular retrospectives to refine policies and process.
- **Benefits:** Improves flow, reduces context switching, increases predictability, and supports continuous delivery with minimal overhead.
- **Meetings:** Daily standup (one or two?), backlog refinement (weekly?), retrospective to improve process

### Definition of Done

As we progress in refining our process the definition of done will change.  We will need to increase the story points associated with a task accordingly.  If at first we are just doing: create branch, make code changes, debug manually, push branch to code review, code review and merge branch that will be fewer story points than if we add in automated unit testing later.

## Development Process Phases

### 1. Software Development Planning

- Define software safety classification (A, B, or C)
- Establish development environment and tools
- Create software development plan per project with risk management

### 2. Software Requirements Specification

- Capture functional and non-functional requirements
- Include safety requirements based on risk analysis
- Use patterns for requirement modeling (e.g., state-based requirements)
- Ensure traceability to system requirements

### 3. Software Architectural Design

- Design high-level software architecture
- Apply Taylor's architectural patterns (e.g., layered architecture for embedded systems)
- Define interfaces and data flows
- Consider hardware-software partitioning
- Identify safety classification (A, B, C) for each architectural element based on risk analysis, ensuring that safety-critical components are appropriately designed and verified

#### Hardware and Operating System Abstraction

Abstraction layers are crucial in embedded software architecture to ensure portability, maintainability, and testability across different hardware platforms and operating systems.

- **Hardware Abstraction Layer (HAL)**: Implement a HAL to abstract low-level hardware interactions, such as GPIO, timers, and communication interfaces. This layer provides a consistent API for higher-level software, allowing code to be hardware-independent and facilitating easier testing with mocks or simulators. Define clear interfaces for hardware drivers, ensuring that changes in hardware do not affect application logic.
- **Operating System Abstraction**: Create an abstraction layer for OS-specific services, such as task scheduling, synchronization primitives (e.g., semaphores, mutexes), and inter-process communication. This enables portability across different OS versions or even different OS types (e.g., from bare-metal to RTOS). Use wrapper functions or interfaces to encapsulate OS calls, promoting modular design and simplifying unit testing.
- **Benefits and Best Practices**: These abstractions support compliance with safety standards by isolating platform-specific code, reducing the risk of errors during porting. Ensure abstractions are well-documented, tested, and include error handling. Regularly review and update abstractions as hardware or OS evolves to maintain compatibility and performance.

#### Architectural Diagrams and Views

Include diagrams for different views of the software architecture to provide comprehensive documentation and facilitate understanding, review, and maintenance. Per best embedded practices, the following views should be represented:

- **Logical View**: Diagrams showing the functional decomposition of the system into modules, components, and their relationships, focusing on the software's logical structure and interfaces.
- **Process View**: Illustrations of concurrency aspects, including tasks, threads, processes, and inter-process communication mechanisms, highlighting real-time and synchronization requirements.
- **Physical View**: Diagrams depicting the mapping of software components to hardware elements, including deployment on processors, memory allocation, and hardware-software partitioning.
- **Development View**: Representations of the code organization, including directory structures, libraries, build configurations, and dependencies, aiding developers in navigation and maintenance.
- **Data Flow View**: Diagrams showing how data flows through the system, including inputs, processing, storage, and outputs, which is particularly important for embedded systems with real-time data handling.

#### Traceability of Software Items to Requirements

Per IEC 62304 clause 5.3.2, the software architectural design shall be traceable to the software requirements. Establish and document bidirectional traceability between software requirements and architectural elements (software items), ensuring that each component, module, interface, and design decision can be linked back to specific requirements.

- **Software Items Identification**: Identify key software items in the architecture, such as modules, classes, functions, data structures, and interfaces.
- **Traceability Matrix**: Maintain a traceability matrix or use tools to link each software item to its originating requirements, demonstrating how the architecture fulfills the specified needs.
- **Rationale Documentation**: For each architectural element, provide rationale explaining how it addresses the traced requirements, including any safety considerations.
- **Verification of Traceability**: During reviews and audits, verify that all requirements are covered by architectural elements and that no orphan items exist without requirement links.

### 4. Software Detailed Design

- Create detailed design specifications
- Implement Taylor's design patterns:
  - Safe State Machine for control logic
  - Watchdog for fault detection
  - Resource Pool for memory management
- Design for testability and maintainability
- Document the design of each work item in the design document prior to code implementation
- Do not focus on capturing the details of variables, function names or function parameters in the design document.  These details will be captured using Doxygen tags in the code.
- Do focus on what the software is doing and how it is doing it before jumping into writing the code.
  - *"Software engineering is about thinking, not typing."*
  - *"Weeks of coding can save you hours of planning."*

### 5. Software Implementation

- Code according to coding standards (MISRA C/C++ for safety or whatever the Vapotherm standard is or if one does not exist we can create our own)
- Implement patterns from Taylor's book
- Use static analysis tools
- Maintain code traceability to design
- **CI/CD Integration**: Utilize Bitbucket Pipelines for continuous integration and deployment of the embedded Linux Yocto platform and Qt applications. This includes automated building, testing, and deployment processes to ensure consistent and reliable software releases.

#### Documentation with Doxygen

Doxygen is a documentation generator tool that extracts documentation from source code comments, creating comprehensive HTML, PDF, or other format documentation. It is essential for maintaining clear, up-to-date documentation in embedded software development, supporting traceability and compliance requirements.

- **Setup and Configuration**: Install Doxygen and configure a Doxyfile for the project. Specify input directories, output formats, and extraction options. Enable features like class diagrams, call graphs, and cross-references.
- **Documenting Files**: Use file-level comments at the top of each source file (e.g., `/** @file filename.c \brief Brief description of the file's purpose. \details Detailed explanation of the file's contents, including any important notes or dependencies. */`). Include author, date, and version information where applicable.
- **Documenting Functions**: Add function comments using the format `/** \brief Brief description of the function. \param[in] param1 Description of input parameter. \param[out] param2 Description of output parameter. \return Description of return value. \note Any additional notes, such as preconditions or side effects. */`. Ensure all parameters, return values, and exceptions are documented.
- **Best Practices**: Use consistent comment styles, keep documentation concise yet comprehensive, and update comments during code changes. Integrate Doxygen generation into the build process or CI/CD pipeline to ensure documentation is always current.
- **Integration with CI/CD**: Automate Doxygen documentation generation in Bitbucket Pipelines to produce and publish documentation artifacts with each build, facilitating easy access for the development team and regulatory reviews.

#### Test Driven Development (TDD) Principles

Test Driven Development is a software development approach where tests are written before the code they are intended to validate. The templates for the tests are the software requirements and design documentaion.  This methodology promotes high-quality, reliable code by ensuring that functionality is thoroughly tested from the outset, aligning with safety-critical embedded software requirements.

- **Red-Green-Refactor Cycle**: Follow the core TDD cycle: (1) Write a failing test (Red), (2) Implement the minimal code to make the test pass (Green), (3) Refactor the code for improvement while keeping tests passing. This iterative process ensures incremental development and prevents regressions.
- **Test-First Approach**: Define the expected behavior through tests before writing production code. This clarifies requirements and drives design decisions, leading to more modular and testable code.
- **Incremental Development**: Develop features in small, testable increments. Each test represents a specific requirement or behavior, promoting focused development and early detection of issues.
- **Test Quality and Coverage**: Write clear, concise tests that cover normal, edge, and error cases. Aim for high test coverage (75% for ordinary code, 85% for safety-critical) using tools like Google Test. Ensure tests are independent, fast, and repeatable.
- **Integration with Embedded Constraints**: Adapt TDD for embedded systems by using mocks and stubs for hardware dependencies. Run tests on host machines or simulators when possible, and integrate TDD practices into the CI/CD pipeline for continuous validation.
- **Benefits for Safety-Critical Software**: TDD enhances code reliability, supports traceability to requirements, and facilitates compliance with standards like IEC 62304 by providing a robust testing foundation from the start.

#### Git-Flow Branching Structure

Git-Flow is a branching model that defines a strict branching structure to support parallel development, release management, and hotfixes in a collaborative environment. It is particularly useful for embedded software projects requiring stable releases and rigorous version control.

- **Main Branch**: The production-ready branch containing only stable, release-quality code. All releases are tagged from this branch.
- **Develop Branch**: The integration branch for ongoing development. Features are merged here once completed and tested.
- **Feature Branches**: Created from develop for implementing new features. Named as `feature/feature-name`, merged back to develop via pull requests after completion.
- **Release Branches**: Created from develop when preparing for a release. Named as `release/version`, used for final testing and bug fixes before merging to main and develop.
- **Hotfix Branches**: Created from main for urgent fixes to production issues. Named as `hotfix/hotfix-name`, merged back to both main and develop.

This structure ensures clean separation of concerns, supports CI/CD integration, and maintains traceability for regulatory compliance. For detailed guidance, refer to [Atlassian Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow).

#### Automated Build - Yocto

The Yocto Project is a powerful build framework and set of collaborative open-source projects for creating custom Linux distributions for embedded systems. It enables reproducible, automated builds of embedded Linux platforms with complete control over components, dependencies, and configurations. Yocto is essential for Vapotherm embedded Linux systems, providing a systematic approach to building tailored, lightweight Linux images for medical devices.

- **Overview and Purpose**: Yocto Project enables creation of custom Linux distributions optimized for specific hardware and application requirements. It automates the compilation of the Linux kernel, device drivers, system libraries, and applications into a complete, minimal filesystem image. This automated build process eliminates manual compilation steps, reduces human error, ensures consistency across builds, and supports reproducible releases for regulatory compliance.

- **Key Yocto Concepts**:
  - **Bitbake**: The core task execution engine and scheduler used by Yocto Project. Bitbake processes recipes (build instructions) and manages dependencies, compilation, and artifact generation. It enables parallel task execution and supports incremental builds.
  - **Recipes**: Build instructions for individual components (e.g., `meta-qt/recipes-qt/qt5/qt5-core_5.x.bb`). Recipes define how to fetch, patch, compile, and package software. They include variables for version control, dependencies, and build flags.
  - **Layers**: Modular collections of related recipes, configurations, and metadata. Layers allow customization without modifying core Yocto files. Example layers include `meta-core` (essential components), `meta-bsp` (board support packages), and custom layers for application-specific components.
  - **Images**: Collections of recipes that define a complete Linux filesystem image for a target. Images specify which components, packages, and applications are included. Example: a `core-image-minimal` image (minimal base system) vs. a custom image with Qt and application software.

- **Yocto Build Workflow**:
  1. **Setup and Configuration**: Initialize the build environment by sourcing the Yocto setup script (e.g., `source poky/oe-init-build-env`). Configure the build parameters in `conf/local.conf` (e.g., target architecture, machine type, optimization flags). Set up custom layers for application code and device-specific configurations.
  2. **Dependency Resolution**: Bitbake analyzes recipe dependencies and creates a task graph, ensuring that components are built in the correct order. This includes kernel builds, device drivers, system libraries, and applications.
  3. **Compilation and Staging**: Compile each recipe's source code with appropriate flags and cross-compiler toolchain for the target architecture. Compilation output (binaries, libraries) is placed in the staging directory for subsequent dependencies.
  4. **Packaging**: Generate binary packages (e.g., `.rpm`, `.deb`, `.ipk`) from compiled artifacts. Packaging respects dependencies and allows selective installation or removal of components.
  5. **Image Creation**: Assemble selected packages into a complete Linux filesystem image, configure boot loaders, and generate deployment artifacts (e.g., kernel image, device tree binary, root filesystem tarball or filesystem image).
  6. **Output Generation**: Produce final artifacts for deployment: kernel binaries, root filesystem images, device tree binaries, and supporting files suitable for flashing to target hardware.

- **Integration with CI/CD Pipeline**: Automate Yocto builds within Bitbucket Pipelines to ensure consistent, reproducible builds on every commit or pull request.
  - **Build Container**: Use a Docker container with Yocto build dependencies pre-installed to ensure consistent build environments across different development machines and CI runners.
  - **Incremental Builds**: Leverage Yocto's sstate (shared state) cache to speed up builds by reusing previously compiled artifacts. Store the sstate cache in a shared location accessible to all CI runners (e.g., shared storage or S3-compatible object storage).
  - **Build Triggers**: Trigger builds on commits to the develop and release branches, as well as on pull requests to validate changes before merging.
  - **Artifact Storage**: Archive build artifacts (kernel images, filesystem images, device trees, packages) in a repository or artifact storage system (e.g., Bitbucket artifact repository, Artifactory, or S3). Tag artifacts with build metadata (build number, commit hash, date) for traceability.
  - **Build Status and Notifications**: Report build success or failure to developers through Bitbucket pipeline status checks and notifications. Include build logs and artifacts in notifications for quick access to results.

- **Customization and Versioning**:
  - **Custom Layers for Applications**: Create custom layers (e.g., `meta-vapotherm`) to host recipes for Vapotherm-specific applications, libraries, and configurations. This separates application code from upstream Yocto layers and facilitates maintenance.
  - **Version Pinning**: Use specific versions or tags for key dependencies (Yocto release version, kernel version, Qt version) in the build configuration. This ensures reproducible builds and allows controlled upgrades. Document version choices in a bill of materials (BOM) or manifest file.
  - **Device Tree Customization**: Modify device tree binaries (DTB) for target hardware to specify hardware configuration, interrupt routing, and device properties. Include device tree sources in custom layers and generate DTBs as part of the build.
  - **Kernel Configuration**: Customize the Linux kernel through Yocto recipes, specifying kernel version, enabled features, device drivers, and build flags. Store kernel configuration fragments in custom layers for version control and reproducibility.

- **Best Practices for Medical Device Builds**:
  - **Reproducible Builds**: Ensure that builds produce identical artifacts when given the same source code and build parameters. This requires careful management of timestamps, dependencies, and random elements. Document the exact Yocto version and configuration used for each release.
  - **Security and Integrity**: Include security updates in custom recipes. Configure the build to generate checksums or signatures for critical components, enabling verification during deployment. Use secure protocols for fetching source code and dependencies.
  - **Testing and Validation**: Integrate boot testing and basic system validation into the CI/CD pipeline (e.g., verify kernel boots, filesystem mounts correctly, critical services start). Use emulation (QEMU) or hardware test benches for regression testing on critical builds.
  - **Documentation**: Maintain detailed documentation of the Yocto configuration, custom layers, and build procedures. Document any patches applied, kernel configurations, and deviations from upstream Yocto. This supports regulatory audits and knowledge transfer.
  - **Build Metrics and Traceability**: Capture build metadata (duration, image size, component versions, build number, commit hash) and store in a build database. This enables tracking of build trends, identification of regressions, and traceability for released products.

#### Automated Build - Apps

Proprietary Qt applications are critical components of the Vapotherm embedded Linux platform, providing the user interface and application-level functionality. Integrating Qt app builds into the Yocto/Bitbake system and CI/CD pipeline ensures consistent, automated compilation and packaging of these applications alongside the Linux kernel and system libraries, resulting in complete, deployable device images.

- **Overview and Integration Strategy**: Qt applications can be built within the Yocto environment through custom recipes in the application layer (e.g., `meta-vapotherm`). This approach guarantees that the Qt framework version, dependencies, and build environment are consistent with the embedded Linux image. The application source code is fetched from a git repository (internal Bitbucket), compiled with the cross-compiler toolchain, and packaged into the final system image or as installable packages.

- **Creating Qt Application Recipes**:
  - **Recipe Structure**: Create a recipe file (e.g., `meta-vapotherm/recipes-qt/apps/vapotherm-ui_1.0.bb`) that defines the build process for the Qt application. The recipe specifies source location, dependencies (Qt modules, custom libraries), build flags, and installation rules.
  - **Source Fetching**: Configure the recipe to fetch source code from Bitbucket using git. Example: `SRC_URI = "git://bitbucket.org/vapotherm/qt-app.git;branch=main;protocol=https"`. Use branch names for development builds and tags for released versions to ensure traceability.
  - **Qt Dependencies**: Declare required Qt modules as dependencies in the recipe (e.g., `DEPENDS = "qt5-core qt5-gui qt5-qml qt5-quick"`). Yocto will ensure these are built and available before compiling the application.
  - **Cross-Compilation Configuration**: Configure the recipe to use the Yocto-provided cross-compiler toolchain and Qt build tools. Set environment variables for Qt paths and use qmake or CMake as appropriate for the application's build system.
  - **Build and Install Steps**: Define the build steps in the recipe. For qmake-based projects: `do_configure() { qmake ... }` and `do_compile() { make }`. For CMake: use the cmake Yocto class. Specify installation rules to place binaries, libraries, and resources in appropriate directories (e.g., `/usr/bin`, `/usr/lib`).

- **Example Qt Recipe (qmake-based)**:

  ```text
  DESCRIPTION = "Vapotherm UI Application"
  LICENSE = "PROPRIETARY"
  HOMEPAGE = "https://bitbucket.org/vapotherm/qt-app"
  
  DEPENDS = "qt5-core qt5-gui qt5-qml qt5-quick qtbase-native qtbase-nativesdk"
  RDEPENDS:${PN} = "qt5-core qt5-gui qt5-qml qt5-quick"
  
  SRC_URI = "git://bitbucket.org/vapotherm/qt-app.git;branch=develop;protocol=https"
  SRCREV = "${AUTOREV}"
  
  S = "${WORKDIR}/git"
  
  inherit qmake5
  
  do_install:append() {
      install -d ${D}/usr/share/vapotherm-ui
      install -m 0755 ${B}/vapotherm-ui ${D}/usr/bin/
      install -m 0644 ${S}/resources/* ${D}/usr/share/vapotherm-ui/
  }
  
  FILES:${PN} = "/usr/bin/vapotherm-ui /usr/share/vapotherm-ui"
  ```

- **Integrating with the Root Filesystem Image**:
  - **Custom Image Recipe**: Create a custom image recipe (e.g., `meta-vapotherm/recipes-core/images/vapotherm-image.bb`) that specifies which packages and applications should be included in the final root filesystem. Include the Qt application package and any required runtime dependencies.
  - **Package Selection**: List the Qt application package and its dependencies in the image recipe. Example: `IMAGE_INSTALL = "packagegroup-core-boot qt5-core qt5-gui qt5-quick vapotherm-ui vapotherm-libs"`.
  - **Image Customization**: Configure image-specific settings such as timezone, locale, hostname, and service startup. Install system libraries, device drivers, and tools required for device operation and maintenance.

- **Application Development Workflow**:
  - **Local Development**: Developers write and test Qt applications locally on their workstations using the full Qt Creator IDE and development toolchain.
  - **Git Repository**: Store application source code in a dedicated Bitbucket repository (e.g., `vapotherm/qt-app`) with git-flow branching structure. Implement code review processes and automated testing (unit tests, UI tests if applicable).
  - **Build Artifacts**: During local development, developers produce build artifacts (binaries, libraries) for their development boards. For rapid iteration, artifacts can be deployed directly to devices via SSH or other mechanisms without rebuilding the full system image.
  - **CI/CD Integration**: On commits to the develop branch and pull requests, trigger automated builds in Bitbucket Pipelines that compile the Qt application using the embedded build environment. Run unit tests and static analysis as part of the pipeline.

- **CI/CD Pipeline for Qt Apps**:
  - **Standalone App Build**: In the CI/CD pipeline, set up a separate build job that compiles the Qt application using the Yocto cross-compiler without requiring a full Yocto/Bitbake image build. This enables rapid feedback (minutes) to developers on whether the code compiles and passes tests.
    - **Build Container**: Use a Docker container with Qt build tools and cross-compiler pre-installed (consistent with Yocto toolchain).
    - **Compilation**: Fetch the application source, compile with qmake or CMake targeting the embedded architecture, and generate binaries.
    - **Unit Testing**: Run unit tests within the container environment. Use test frameworks like Google Test for C++ backend code and Qt Test for Qt-specific code.
    - **Static Analysis**: Run static analysis tools (Cppcheck, Coverity) on the application source to detect issues before integration.
    - **Artifact Archival**: Archive compiled binaries and test results for later inspection or manual testing on hardware.
  
  - **Full System Image Build**: Periodically (e.g., on merges to develop or main, nightly builds), trigger a complete Yocto build that includes the Qt application as a package. This validates that the application integrates correctly with the full system image and all dependencies resolve properly.
    - **Build Trigger**: Schedule nightly builds or trigger on commits to the develop branch.
    - **Yocto Build**: Execute the full Yocto build, which fetches and compiles the Qt application recipe along with all system components.
    - **Image Generation**: Generate the final system image (kernel, root filesystem, device tree).
    - **System Testing**: Flash the image to a hardware device or emulator (QEMU) and run system-level tests to verify the application starts, responds to user input, and integrates properly with the system.
    - **Artifact Storage**: Archive the complete system image, kernel, device tree, and manifests with metadata (Yocto versions, component versions, build timestamp, commit hash) for reproducibility and traceability.

- **Dependency Management**:
  - **Qt Version Pinning**: Specify a particular Qt version in the Yocto layer to ensure consistency. Document any patches or customizations applied to Qt for the embedded platform.
  - **Third-Party Libraries**: If the Qt application depends on external libraries (e.g., protocol libraries, databases), create Yocto recipes for these as well. Place them in the custom layer alongside the application recipe.
  - **Version Control**: Use Git tags for released versions of both the application source and the Yocto layer configuration. This enables reproducing builds for specific product releases.

- **Performance and Size Optimization**:
  - **Binary Stripping**: Configure Yocto recipes to strip unnecessary debug symbols from production binaries to reduce image size and improve startup time.
  - **Qt Module Reduction**: Include only required Qt modules in the build. Avoid unnecessary features or plugins that would increase binary size and startup time.
  - **Incremental Updates**: For field updates, package only the modified application binaries separately from the system image. This enables faster, smaller update packages.
  - **Resource Bundling**: For resources like images, QML files, or configuration files, consider embedding them in the application binary or including them in optimized, compressed archives.

- **Security Considerations**:
  - **Code Signing**: If required by the security policy, digitally sign application binaries using a key management system. Include signature verification in the boot process or application launcher.
  - **Secure Source Fetching**: Use HTTPS for all git repository access. Implement authentication (SSH keys or personal access tokens) for private repositories, securely managed in CI/CD credentials.
  - **Dependency Scanning**: Regularly scan Qt and third-party library dependencies for known vulnerabilities using tools like OWASP Dependency-Check or Black Duck. Address vulnerabilities through updates or patches.
  - **Build Environment Isolation**: Isolate the build environment (Docker containers in CI/CD) to prevent cross-contamination between builds and unauthorized access to source code or credentials.

### 6. Software Verification

A wise engineer once told me *"Problems are our friends until we release the product."*  It should be (but sometimes isn't) obvious that the purpose of testing is to find problems.

- Unit testing of individual modules
- Static and dynamic analysis
- Code reviews and inspections
- Integration testing of components
- Apply Taylor's testing patterns (e.g., fault injection testing)
- Software Requirements Verification aka Software System Testing
- Cybersecurity Testing

#### Unit Testing with Google Test

Unit testing is essential for verifying individual software components and ensuring code reliability in embedded systems. Google Test (gtest) is used as the primary framework for writing and executing unit tests, providing a robust set of assertions, test fixtures, and mocking capabilities suitable for C/C++ embedded development.

- **Code Coverage Requirements**: Aim for at least 75% code coverage for ordinary code and 85% for safety-critical code (as classified per IEC 62304). Lower coverage is acceptable for hardware-related sections that cannot be easily tested, such as direct register access or interrupt handlers, provided that alternative verification methods (e.g., integration testing) are employed.
- **Test Organization**: Structure tests using TEST and TEST_F macros. Group related tests into test suites and use test fixtures for shared setup/teardown code. Separate test files from production code and place them in dedicated test directories.
- **Writing Effective Tests**: Write tests that are independent, repeatable, and fast. Use descriptive test names, cover both normal and edge cases, and include assertions for expected behavior. Mock hardware dependencies using Google Mock to isolate unit under test.
- **Integration with Build System**: Compile and run tests as part of the CI/CD pipeline (e.g., Bitbucket Pipelines). Use tools like gcov or lcov for coverage analysis, and fail builds if coverage thresholds are not met.
- **Best Practices**: Run tests regularly during development, maintain test code quality, and update tests when refactoring code. Document test rationale in comments, especially for safety-critical functions, to support regulatory compliance.

#### Static Analysis

Static analysis tools are essential for detecting potential bugs, security vulnerabilities, and code quality issues early in the development process. They analyze source code without executing it, complementing dynamic testing and code reviews.

- **Local Developer Machine Tools**: Developers should run lightweight, open-source static analysis tools locally to catch issues before committing code.
  - **Cppcheck**: A free, open-source tool for C/C++ code that detects bugs, undefined behavior, and performance issues. It supports MISRA C/C++ rules and can be integrated into IDEs. Reference: [Cppcheck](https://cppcheck.sourceforge.io/)
  - **Flawfinder**: A tool that scans C/C++ source code for potential security vulnerabilities, such as buffer overflows and format string issues. It's simple to use and provides severity ratings. Reference: [Flawfinder](https://dwheeler.com/flawfinder/)
- **CI/CD Integration**: For deeper analysis, integrate a commercial static analysis tool into the CI/CD pipeline (e.g., Bitbucket Pipelines) to automatically scan code on commits and pull requests.
  - **Coverity**: A comprehensive static analysis tool that identifies defects, security vulnerabilities, and compliance issues in C/C++ code. It provides detailed reports and integrates with CI/CD systems. Reference: [Synopsys Coverity](https://www.synopsys.com/software-integrity/security-testing/static-analysis-tools.html)
  - Alternatives include PVS-Studio ([PVS-Studio](https://pvs-studio.com/)), Klocwork ([Perforce Klocwork](https://www.perforce.com/products/klocwork)), or CodeSonar ([GrammaTech CodeSonar](https://www.grammatech.com/products/codesonar)). Choose based on project needs and licensing.

Run static analysis regularly, address findings promptly, and document results for regulatory compliance.

#### Pull Request Peer Code Review Checklist

Peer code reviews are critical for maintaining code quality, safety, and compliance in embedded software development. Use the following checklist during pull request reviews to ensure thorough evaluation:

- **Build Verification**: Confirm that the code builds successfully without errors in the CI/CD pipeline (e.g., Bitbucket Pipelines). Check for any build failures and ensure all dependencies are properly configured.
- **Compiler Errors and Warnings**: Verify that there are no compiler errors or warnings. Address any warnings that could indicate potential issues, especially in safety-critical code.
- **Doxygen Documentation**: Ensure that all new or modified files and functions include appropriate Doxygen comments. Check for completeness, accuracy, and adherence to documentation standards.
- **Unit Testing**: Confirm that unit tests are included for new functionality and that existing tests pass. Review test coverage and ensure tests validate the intended behavior.
- **Static Analysis**: Verify that static analysis tools (e.g., integrated with CI/CD) report no new issues. Address any introduced vulnerabilities, code issues, or compliance violations.
- **Target Execution**: Ensure that the new code runs properly on the target hardware. This may involve reviewing integration tests, hardware-in-the-loop testing, or deployment verification in the CI/CD process.

#### Integration Testing

Integration testing is a relatively quick set of tests designed to verify that integrated software components work together correctly and ensure the essential functionality of the system. It bridges the gap between unit testing (individual components) and full software requirements verification, focusing on interfaces, data flow, and basic interactions without requiring the complete target environment.

- **Scope and Objectives**: Test the combination of modules or subsystems to detect interface defects, data inconsistencies, and integration issues. Prioritize essential functionality, such as core workflows, communication protocols, and critical paths, to provide rapid feedback on system cohesion.  Testing should be relatively quick and easy to run to ensure that it gets run frequently.
- **Test Design**: Develop manual or automated test suites that can run in a simulated or partial environment. Include basic positive and negative test cases, boundary conditions, and error handling scenarios.
- **Execution and Timing**: Perform integration tests frequently during development, ideally as part of the CI/CD pipeline, to catch issues early. Aim for quick execution (e.g., minutes rather than hours) to support agile development while ensuring reliability.
- **Tools and Environment**: Leverage tools like Google Test for C/C++ integration tests, or scripting frameworks for higher-level integrations. Run tests on development boards or emulators when possible to approximate real hardware behavior.
- **Compliance and Documentation**: Document test cases, results, and any deviations. Ensure traceability to requirements and include integration testing in the verification plan per IEC 62304 guidelines.

#### Cybersecurity Testing

Cybersecurity testing is critical for medical devices to ensure protection against threats that could compromise patient safety, data integrity, and system functionality. This includes direct testing of security controls and third-party penetration testing, aligned with FDA Premarket Cybersecurity Guidance.

- **Direct Positive and Negative Tests for Cybersecurity Controls**: Perform targeted testing to verify the effectiveness of implemented security controls.
  - **Positive Tests**: Validate that security controls function correctly under expected conditions. For example, test that authentication mechanisms allow access with valid credentials, encryption properly secures data transmission, and access controls enforce proper permissions. Use automated test suites to simulate normal operations and confirm controls prevent unauthorized actions.
  - **Negative Tests**: Verify that controls appropriately reject invalid inputs or malicious attempts. For instance, test authentication failure with incorrect credentials, rejection of malformed data that could exploit vulnerabilities, and proper handling of denial-of-service attempts. Include boundary testing for edge cases, such as buffer overflows or injection attacks, to ensure robust error handling.
  - **Test Coverage**: Ensure tests cover all identified cybersecurity controls from the risk assessment, including input validation, secure communication, and data protection mechanisms. Document test cases, results, and any deviations in the verification records for regulatory compliance.

- **Third-Party Penetration Testing**: Engage external cybersecurity experts to conduct penetration testing (pentesting) to simulate real-world attacks and identify vulnerabilities not caught by internal testing.
  - **Scope and Methodology**: Define the testing scope based on asset identification and threat modeling, focusing on critical components like network interfaces, user interfaces, and data storage. Use methodologies such as OWASP for web-based components or industry-standard frameworks for embedded systems.
  - **Execution**: Conduct testing in a controlled environment that mimics production systems, including both black-box (no prior knowledge) and white-box (with source code access) approaches. Test for common vulnerabilities like SQL injection, cross-site scripting, and firmware exploits.
  - **Reporting and Remediation**: Document findings in detailed reports, including severity ratings, exploitability, and remediation recommendations. Address identified vulnerabilities through code fixes, configuration changes, or additional controls, and retest to confirm resolution.
  - **Frequency and Integration**: Perform penetration testing at key milestones (e.g., before releases) and integrate results into the risk management file. Ensure third-party testers are qualified and follow ethical guidelines.

These cybersecurity verification activities support compliance with IEC 62304 and FDA requirements by demonstrating that security risks are adequately controlled and monitored.

### 7. Software Validation

- System-level testing in target environment
- Validation against user requirements
- Risk-based testing for safety-critical functions
- Performance and reliability testing

### 8. Software Maintenance and Configuration Management

- Version control and change management
- Problem reporting and corrective actions
- Software updates and patches
- Continuous monitoring of field performance

## Risk Management Integration

Throughout the process, risk management follows IEC 62304 and FDA requirements, incorporating cybersecurity considerations from the FDA Premarket Cybersecurity Guidance:

### General Risk Management

- Conduct hazard analysis and risk assessment for safety risks
- Implement risk controls through design patterns and safety mechanisms
- Verify risk mitigation effectiveness through testing and analysis
- Maintain comprehensive risk management file

### Cybersecurity Risk Management (FDA Guidance)

- **Asset Identification**: Identify critical system assets, data, and components that could be affected by cybersecurity threats
- **Threat Modeling**: Analyze potential cybersecurity threats, including unauthorized access, data breaches, and malware
- **Vulnerability Assessment**: Evaluate system vulnerabilities through security testing and code analysis
- **Risk Assessment**: Assess cybersecurity risks using frameworks like STRIDE or OCTAVE, considering likelihood and impact
- **Security Controls Implementation**: Develop and implement security controls such as encryption, access controls, and secure communication protocols
- **Security Testing and Validation**: Perform penetration testing, fuzzing, and other security validation activities
- **Post-Market Considerations**: Plan for ongoing cybersecurity monitoring, patch management, and incident response
- **Documentation**: Include cybersecurity risk management information in the risk management file and premarket submissions

Cybersecurity risks are integrated with overall product risk management, ensuring that security vulnerabilities are addressed alongside safety hazards.

## Documentation Requirements

- Software development plan
- Requirements specifications
- Design documents
- Verification and validation reports
- Risk management file
- User manuals and maintenance guides

## Continuous Improvement

- Post-market surveillance
- Incident analysis and learning
- Process metrics and KPIs
- Regular audits and reviews

This process ensures compliance with regulatory requirements while leveraging proven patterns for building safe, reliable embedded software for medical devices.

## Bibliography

- Taylor, John. *Patterns in the Machine: A Software Engineering Guide to Embedded Development*. Amazon: [https://www.amazon.com/Patterns-Machine-Software-Engineering-Embedded/dp/1543901803](https://www.amazon.com/Patterns-Machine-Software-Engineering-Embedded/dp/1543901803)
- Taylor, John. *The Embedded Project Cookbook: Practical Techniques for Embedded Systems Development*. Amazon: [https://www.amazon.com/Embedded-Project-Cookbook-Practical-Techniques/dp/012817932X](https://www.amazon.com/Embedded-Project-Cookbook-Practical-Techniques/dp/012817932X)
- Grenning, James W. *Test Driven Development for Embedded C*. Amazon: [https://www.amazon.com/Test-Driven-Development-Embedded-Pragmatic-Programmers/dp/193435662X](https://www.amazon.com/Test-Driven-Development-Embedded-Pragmatic-Programmers/dp/193435662X)
- FDA. *Premarket Cybersecurity Guidance*. [https://www.fda.gov/medical-devices/digital-health-center-excellence/premarket-cybersecurity-guidance](https://www.fda.gov/medical-devices/digital-health-center-excellence/premarket-cybersecurity-guidance)
- FDA. *Guidance for the Content of Premarket Submissions for Software Contained in Medical Devices*. [https://www.fda.gov/regulatory-information/search-fda-guidance-documents/guidance-content-premarket-submissions-software-contained-medical-devices](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/guidance-content-premarket-submissions-software-contained-medical-devices)

### Other References

- Sonmez, John. *Soft Skills: The Software Developer's Life Manual*. Amazon: [https://www.amazon.com/Soft-Skills-software-developers-manual/dp/1617292397](https://www.amazon.com/Soft-Skills-software-developers-manual/dp/1617292397)
