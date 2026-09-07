# Fuuz MES Accelerator

A packaged shop-floor production execution application built on the [FUUZ](https://fuuz.app) platform — Work Order dispatch, Control Panel-driven production runs, quality checks, genealogy/traceability, and Kanban replenishment, ready to import into a Fuuz tenant.

## The Scenario

A discrete manufacturer needs to dispatch Work Orders to the floor, execute them against specific Workunits (equipment/machines/stations) through operator-facing Control Panels, run quality checks at the point of production, and keep a full genealogy trail — without custom development. The MES Accelerator packages that entire flow, from Work Order creation through Production Run execution to Quality and Genealogy, as a single importable Fuuz package.

## One Application, One Platform

**Package:** `Accelerator Package@1.0.6.fuuz`

| Component | Count |
|---|---|
| Data Models | 93 |
| Screens | 66 |
| Data Flows | 29 |
| Document Designs | 4 |
| Seeded Reference Data Sets | 25 |

Built against **platform version 2026.8.0**.

## 93 Data Models

| Category | Models | What They Track |
|---|---|---|
| **Work Order Management** | ApprovedWorkunit, WorkOrder, WorkOrderProcess, WorkOrderProcessBom, WorkOrderProcessDistribution, WorkOrderProcessDistributionDependency, WorkOrderStatus | The unit of demand dispatched to production and its distribution onto specific Workunits |
| **Production Execution** | Area, ConsumptionType, Container, ContainerBomPattern, ContainerContent, ContainerHandoffStatus, ContainerHistory, ContainerStatus, Defect, DefectSeverity, DefectType, Deviation, DeviationType, ProductionHistory, ProductionHistoryData, ProductionHistoryDataType, ProductionHistoryInput, ProductionHistoryOperator, ProductionRun, ProductionSetupReplenishmentRequests, ProductionStepHistory, ScheduleConfiguration, VinElementValue, Workcenter, Workunit, WorkunitDefect | The physical/logical site hierarchy, the Workunit resource model, and full production run history |
| **Work Units, States & Events** | Event, EventCategory, EventList, EventListEvent, Mode, State, StateCategory, StateList, StateListState, WorkunitDevice, WorkunitHistory, WorkunitScrapReason, WorkunitStateHistory | The state/mode machine each Workunit progresses through, and devices attached to it |
| **Product & Process Data** | ContainerType, Process, ProcessRoute, ProcessStep, Product, ProductCategory, ProductStage, ProductStrategy, ProductStrategyProcess, ProductStrategyProcessBom, ProductStrategyProcessProduct, ProductStrategyProcessStep, ProductVinConfiguration | How a product is built — process routes, steps, and strategy, including VIN-rule support for vehicle assembly |
| **Quality** | QualityCheck, QualityInterval, QualityReport, QualitySpecification, QualitySpecificationCategory, QualitySpecificationProcess, QualitySpecificationProduct, QualitySpecificationProductStep, QualitySpecificationType | Checks presented at the Control Panel and the reports captured from them |
| **Control Panels & Production Setup** | ProductionSetupBom, ProductionSetupMaterial, ProductionSetupOperator, ProductionSetupOutput, ProductionSetupOutputStep | BOM, material, operator, and output configuration for a Workunit's active production setup |
| **Scheduling** | Kanban, KanbanStatus, KanbanType | Kanban replenishment card lifecycle and classification |
| **Employees & Operators** | Employee, EmployeeCertification, EmployeeGroup, OperatorActivity | Operator master data, certifications, and the activities operators perform on production |
| **Genealogy & Traceability** | HistoryStatus, OperatorHistory, ScrapReason | Full operator and history-record traceability |
| **Storage & Inventory Movement** | Location, LocationStatus, WorkunitInput | Storage locations and the source material inputs to a Workunit |
| **Resources & Site Management** | AndonReason, AndonRequest | Andon request lifecycle and reason codes |
| **Configuration** | ProductStrategyProcessStepType, ProductionSetupOutputStepStatus | Process step type and output step status classification |
| **Product Configuration** | ContainerKitConfiguration | Required pack pattern for kit-configured container types |

## 66 Screens

- **10 Quality Screens** — Quality Specification Management, Quality Reports, Quality Intervals, Specification Categories and Products
- **9 Control Panel Screens** — Andon Requests, Control Panel variants (IP SubAssy, No Badge, Released Start), Defect/Scrap Select Modals, Mode Management, Production Setup Material Management
- **12 Production Execution Screens** — Production Homepage - All Control Panels, Container/Defect Management, Mode/State Change Modals, Distribution Modals, Scrap Reasons
- **7 Product & Process Data Screens** — Process Route, Product Category, Product Details/Edit, Product Group, Product Stage Management
- **6 Product Configuration Screens** — Container BOM Patterns, Container Kit Configuration, Container Status/Type Management, Picklist Template, Process Management
- **6 Work Units, States & Events Screens** — State Category/Management/Modal, Workunit Defects, Workunit Device Map, Workunit Management
- **4 Work Order Management Screens** — Build Distribution Modal, Work Order Details Form, Work Order Management, Work Order Status Management
- **2 Genealogy Screens** — Production History, Production History Data Types
- **2 Employee Screens**, **2 Configuration Screens**, **1 Kanban Management**, **1 Site Management**, **1 Control Panel Access** (WIP Dashboard)
- **3 Testing & Utility Screens** — placeholder/test screens not intended for production use

## 29 Data Flows

- **Production Execution** — Control Panel Load Flow, Distribution Listener, Production Functions, Production Run Functions, Parse 2D Barcode - Supplier Label
- **Control Panels & Production Setup** — Control Panel Step Functions, Control Panel Web Flow, Data Changes - Andon Request, Pack Functions
- **Work Order Management** — Dispatch Functions, Work Order Functions, Work Order Management Web Flow
- **Quality** — Create Quality Reports, Get Quality Specifications, Quality Specification Management Webflow
- **Work Units, States & Events** — Back Fill End Dates of Workunit History, Scrap & Defect - Workunit Mapping Web Flow, Workunit Functions
- **Product & Process Data** — Product Details Web Flow, Container Functions, Container Debug Cleanup, Product Strategy Management Functions
- **Integration** — MES_CMMS_Request, MES_WMS Inventory, MES_WMS Material Replenishment
- **Resources & Site Management** — Workunit Schedule Assignment Functions, Site Management Web Flow
- **Configuration** — Reset Work Order, Web Flow Log

## Document Designs

Build Manifest, Sub Assembly Label, Work Order Report, Inventory Label.

## Seeded Reference Data

This build ships seeded values for `WorkOrderStatus`, `ContainerStatus`, `KanbanStatus`, `KanbanType`, `Process`, `Mode`, `ProductStage`, `TransactionType`, `ConsumptionType`, `QualitySpecificationType`, and related state/event/access-control lookups, in addition to the standard `ApplicationConfiguration`, `AccessControlPolicy`, and `AccessControlPolicyGroup` sets.

## Packaged Integrations

Ships flows for connecting to adjacent Fuuz accelerators: `MES_WMS Inventory`, `MES_WMS Material Replenishment`, and `MES_CMMS_Request`.

## Getting Started

### Import into FUUZ

1. Request a [free trial of FUUZ](https://forms.zohopublic.com/mfgxonlinesaas/form/TrialNotificationForm/formperma/syUyoccvUH7Ef5DaReDpfM48vuKiZtaGfYN18JPPu9k)
2. Navigate to **Fuuz Packages**
3. Upload `Accelerator Package@1.0.6.fuuz`
4. Review the import preview and confirm
5. Configure your site structure (Area → Workcenter → Workunit → Location) and Product/Process data, then create your first Work Order

### Explore the Package

Each `.fuuz` file is a gzipped tarball containing three JSON files:

```bash
mkdir extracted && cd extracted
tar -xzf "../Accelerator Package@1.0.6.fuuz"

ls -lh
# manifest.json      - Package metadata (name, version, dependencies)
# definition.json    - Module groups, modules, and enum seed data
# package-data.json  - Data models, screens, flows, and seed data
```

## Requirements

- A Fuuz Industrial Intelligence Platform tenant, platform version 2026.8.0 or later
- The Fuuz WMS and/or CMMS Accelerators, if you plan to use the packaged integration flows

## Resources

| Resource | Link | Description |
|---|---|---|
| **Free Trial** | [fuuz.app](https://forms.zohopublic.com/mfgxonlinesaas/form/TrialNotificationForm/formperma/syUyoccvUH7Ef5DaReDpfM48vuKiZtaGfYN18JPPu9k) | Request your free trial of FUUZ |
| **Get Started** | [getstarted.fuuz.com](https://getstarted.fuuz.com) | Introductory videos and walkthroughs |
| **FUUZ Academy** | [academy.fuuz.com](https://academy.fuuz.com) | Online LMS with structured courses and certifications |
| **Support & Community** | [support.fuuz.com](https://support.fuuz.com) | Knowledge base, documentation, and customer community |

## License

© Fuuz. All rights reserved. This package is proprietary software provided for use with the Fuuz Industrial Intelligence Platform. Redistribution or use outside of a licensed Fuuz tenant is not permitted without express written permission.

## Service levels

No service level agreement applies to anything published here. It becomes a supported
deliverable only once it has been implemented by a Fuuz services professional or an
approved Fuuz partner.
