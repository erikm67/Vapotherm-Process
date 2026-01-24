# Vapotherm Embedded Software Development Process

## Overview

This document outlines an embedded software development process for medical devices that complies with IEC 62304 (Medical device software — Software life cycle processes) and FDA software functions regulations. The process incorporates design patterns and best practices from John Taylor's "Patterns in the Machine: A Software Engineering Guide to Embedded Development," which emphasizes safety, reliability, and maintainability in embedded systems.

## Regulatory Compliance Framework

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

## Development Process Phases

### 1. Software Development Planning
- Define software safety classification (A, B, or C)
- Establish development environment and tools
- Create software development plan with risk management
- Incorporate Taylor's patterns for system architecture planning

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

### 5. Software Implementation
- Code according to coding standards (MISRA C/C++ for safety)
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

### 6. Software Verification
- Unit testing of individual modules
- Integration testing of components
- Apply Taylor's testing patterns (e.g., fault injection testing)
- Static and dynamic analysis
- Code reviews and inspections

#### Pull Request Peer Code Review Checklist
Peer code reviews are critical for maintaining code quality, safety, and compliance in embedded software development. Use the following checklist during pull request reviews to ensure thorough evaluation:

- **Build Verification**: Confirm that the code builds successfully without errors in the CI/CD pipeline (e.g., Bitbucket Pipelines). Check for any build failures and ensure all dependencies are properly configured.
- **Compiler Errors and Warnings**: Verify that there are no compiler errors or warnings. Address any warnings that could indicate potential issues, especially in safety-critical code.
- **Doxygen Documentation**: Ensure that all new or modified files and functions include appropriate Doxygen comments. Check for completeness, accuracy, and adherence to documentation standards.
- **Unit Testing**: Confirm that unit tests are included for new functionality and that existing tests pass. Review test coverage and ensure tests validate the intended behavior.
- **Static Analysis**: Verify that static analysis tools (e.g., integrated with CI/CD) report no new issues. Address any introduced vulnerabilities, code issues, or compliance violations.
- **Target Execution**: Ensure that the new code runs properly on the target hardware. This may involve reviewing integration tests, hardware-in-the-loop testing, or deployment verification in the CI/CD process.

#### Unit Testing with Google Test
Unit testing is essential for verifying individual software components and ensuring code reliability in embedded systems. Google Test (gtest) is used as the primary framework for writing and executing unit tests, providing a robust set of assertions, test fixtures, and mocking capabilities suitable for C/C++ embedded development.

- **Code Coverage Requirements**: Aim for at least 75% code coverage for ordinary code and 85% for safety-critical code (as classified per IEC 62304). Lower coverage is acceptable for hardware-related sections that cannot be easily tested, such as direct register access or interrupt handlers, provided that alternative verification methods (e.g., integration testing) are employed.
- **Test Organization**: Structure tests using TEST and TEST_F macros. Group related tests into test suites and use test fixtures for shared setup/teardown code. Separate test files from production code and place them in dedicated test directories.
- **Writing Effective Tests**: Write tests that are independent, repeatable, and fast. Use descriptive test names, cover both normal and edge cases, and include assertions for expected behavior. Mock hardware dependencies using Google Mock to isolate unit under test.
- **Integration with Build System**: Compile and run tests as part of the CI/CD pipeline (e.g., Bitbucket Pipelines). Use tools like gcov or lcov for coverage analysis, and fail builds if coverage thresholds are not met.
- **Best Practices**: Run tests regularly during development, maintain test code quality, and update tests when refactoring code. Document test rationale in comments, especially for safety-critical functions, to support regulatory compliance.

#### Integration Testing
Integration testing is a relatively quick set of tests designed to verify that integrated software components work together correctly and ensure the essential functionality of the system. It bridges the gap between unit testing (individual components) and full software requirements verification, focusing on interfaces, data flow, and basic interactions without requiring the complete target environment.

- **Scope and Objectives**: Test the combination of modules or subsystems to detect interface defects, data inconsistencies, and integration issues. Prioritize essential functionality, such as core workflows, communication protocols, and critical paths, to provide rapid feedback on system cohesion.  Testing should be relatively quick and easy to run to ensure that it gets run frequently.
- **Test Design**: Develop manual or automated test suites that can run in a simulated or partial environment. Include basic positive and negative test cases, boundary conditions, and error handling scenarios.
- **Execution and Timing**: Perform integration tests frequently during development, ideally as part of the CI/CD pipeline, to catch issues early. Aim for quick execution (e.g., minutes rather than hours) to support agile development while ensuring reliability.
- **Tools and Environment**: Leverage tools like Google Test for C/C++ integration tests, or scripting frameworks for higher-level integrations. Run tests on development boards or emulators when possible to approximate real hardware behavior.
- **Compliance and Documentation**: Document test cases, results, and any deviations. Ensure traceability to requirements and include integration testing in the verification plan per IEC 62304 guidelines.

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