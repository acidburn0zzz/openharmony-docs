# Quick Start

- Getting Started
  - [Before You Start](start-overview.md)
  - [Getting Started with ArkTS in Stage Model](start-with-ets-stage.md)
- Development Fundamentals
  - Application Package Fundamentals
    - [Application Package Overview](application-package-overview.md)
    - Application Package Structure
      - [Application Package Structure in Stage Model](application-package-structure-stage.md)
      - [Application Package Structure in FA Model](application-package-structure-fa.md)
    - Multi-HAP Mechanism
      - [Multi-HAP Design Objectives](multi-hap-objective.md)
      - [Multi-HAP Build View](multi-hap-build-view.md)
      - [Multi-HAP Development, Debugging, Release, and Deployment Process](multi-hap-release-deployment.md)
      - [Multi-HAP Usage Rules](multi-hap-rules.md)
      - [Multi-HAP Operation Mechanism and Data Communication Modes](multi-hap-principles.md)
    - [Application Installation and Uninstallation Process](application-package-install-uninstall.md)
    - [Application Package Update Process](application-package-update.md)
    - Shared Package
      - [Shared Package Overview](shared-guide.md)
      - [HAR](har-package.md)
      - HSP
        - [In-Application HSP Development](in-app-hsp.md)
        - [Inter-Application HSP Development](cross-app-hsp.md)
    - Atomic Service
      - [Atomic Service Development](atomicService.md)
      - [Atomic Service Space Management (for System Applications Only)](atomicService-aging.md)
    - Quick Fix
      - [Quick Fix Overview](quickfix-principles.md)
      - [CLI-based Quick Fix Development](quickfix-debug.md)
  - Application Configuration Files in Stage Model
    - [Application Configuration File Overview (Stage Model)](application-configuration-file-overview-stage.md)
    - [app.json5 Configuration File](app-configuration-file.md)
    - [module.json5 Configuration File](module-configuration-file.md)
  - Application Configuration Files in FA Model
    - [Application Configuration File Overview (FA Model)](application-configuration-file-overview-fa.md)
    - [Internal Structure of the app Tag](app-structure.md)
    - [Internal Structure of the deviceConfig Tag](deviceconfig-structure.md)
    - [Internal Structure of the module Tag](module-structure.md)
  - [Resource Categories and Access](resource-categories-and-access.md)
- Learning ArkTS
    - [Getting Started with ArkTS](arkts-get-started.md)
  - Basic Syntax
    - [Basic Syntax Overview](arkts-basic-syntax-overview.md)
    - [Declarative UI Description](arkts-declarative-ui-description.md)
    - Custom Component
      - [Creating a Custom Component](arkts-create-custom-components.md)
      - [Page and Custom Component Lifecycle](arkts-page-custom-components-lifecycle.md)
    - [\@Builder Decorator: Custom Builder Function](arkts-builder.md)
    - [\@BuilderParam Decorator: @Builder Function Reference](arkts-builderparam.md)
    - [\@Styles Decorator: Definition of Resusable Styles](arkts-style.md)
    - [\@Extend Decorator: Extension of Built-in Components](arkts-extend.md)
    - [stateStyles Decorator: Polymorphic Style](arkts-statestyles.md)
  - State Management
    - [State Management Overview](arkts-state-management-overview.md)
    - Component State Management
      - [\@State Decorator: State Owned by Component](arkts-state.md)
      - [\@Prop Decorator: One-Way Synchronization from Parent to Child Components](arkts-prop.md)
      - [\@Link Decorator: Two-Way Synchronization Between Parent and Child Components](arkts-link.md)
      - [\@Provide and \@Consume Decorators: Two-Way Synchronization with Descendant Components](arkts-provide-and-consume.md)
      - [\@Observed and \@ObjectLink Decorators: Observing Attribute Changes in Nested Class Objects](arkts-observed-and-objectlink.md)
    - Application State Management
      - [Application State Management Overview](arkts-application-state-management-overview.md)
      - [LocalStorage: UI State Storage](arkts-localstorage.md)
      - [AppStorage: Application-wide UI State Storage](arkts-appstorage.md)
      - [PersistentStorage: Application State Persistence](arkts-persiststorage.md)
      - [Environment: Device Environment Query](arkts-environment.md)
    - Other State Management Features
      - [Overview of Other State Management Features](arkts-other-state-mgmt-functions-overview.md)
      - [\@Watch: Getting Notified of State Variable Changes](arkts-watch.md)
      - [$$ Syntax: Two-Way Synchronization of Built-in Components](arkts-two-way-sync.md)
  - Rendering Control
    - [Rendering Control Overview](arkts-rendering-control-overview.md)
    - [if/else: Conditional Rendering](arkts-rendering-control-ifelse.md)
    - [ForEach: Rendering of Repeated Content](arkts-rendering-control-foreach.md)
    - [LazyForEach: Lazy Data Loading](arkts-rendering-control-lazyforeach.md)
