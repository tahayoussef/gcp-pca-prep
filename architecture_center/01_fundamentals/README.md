# Google Cloud Architecture Center - Fundamentals

This directory contains concise summaries of the **Fundamentals** section of the Google Cloud Architecture Center.

## 1. Google Cloud Well-Architected Framework
Core principles and best practices for building secure, reliable, and efficient systems.

*   **1. Operational Excellence**
    *   [Operational Readiness and Performance](01_google_cloud_well_architected_framework/01_operational_excellence/01_operational_readiness_and_performance_using_cloudops.md)
    *   [Manage Incidents and Problems](01_google_cloud_well_architected_framework/01_operational_excellence/02_manage_incidents_and_problems.md)
    *   [Manage and Optimize Resources](01_google_cloud_well_architected_framework/01_operational_excellence/03_manage_and_optimize_cloud_resources.md)
    *   [Automate and Manage Change](01_google_cloud_well_architected_framework/01_operational_excellence/04_automate_and_manage_change.md)
    *   [Continuously Improve](01_google_cloud_well_architected_framework/01_operational_excellence/05_continuously_improve_and_innovate.md)

*   **2. Cost Optimization**
    *   [Align with Business Value](01_google_cloud_well_architected_framework/02_cost_optimization/01_align_cloud_spending_with_business_value.md)
    *   [Culture of Cost Awareness](01_google_cloud_well_architected_framework/02_cost_optimization/02_foster_a_culture_of_cost_awareness.md)
    *   [Optimize Resource Usage](01_google_cloud_well_architected_framework/02_cost_optimization/03_optimize_resource_usage.md)
    *   [Optimize Continuously](01_google_cloud_well_architected_framework/02_cost_optimization/04_optimize_continuously.md)

*   **3. Security, Privacy, and Compliance**
    *   [Security by Design](01_google_cloud_well_architected_framework/03_security_privacy_and_compliance/01_implement_security_by_design.md)
    *   [Zero Trust](01_google_cloud_well_architected_framework/03_security_privacy_and_compliance/02_implement_zero_trust.md)
    *   [Shift Left Security](01_google_cloud_well_architected_framework/03_security_privacy_and_compliance/03_implement_shift_left_security.md)
    *   [Preemptive Cyber Defense](01_google_cloud_well_architected_framework/03_security_privacy_and_compliance/04_implement_preemptive_cyber_defense.md)
    *   [Secure AI Usage](01_google_cloud_well_architected_framework/03_security_privacy_and_compliance/05_use_ai_securely_and_responsibly.md)
    *   [Compliance and Privacy](01_google_cloud_well_architected_framework/03_security_privacy_and_compliance/06_meet_regulatory_compliance_and_privacy_needs.md)
    *   [Shared Responsibility](01_google_cloud_well_architected_framework/03_security_privacy_and_compliance/07_shared_responsibilities_and_shared_fate.md)

*   **4. Reliability**
    *   [Define Reliability Goals](01_google_cloud_well_architected_framework/04_reliability/01_define_reliability_based_on_user_experience_goals.md)
    *   [Set Targets (SLO/SLI)](01_google_cloud_well_architected_framework/04_reliability/02_set_targets.md)
    *   [Build HA Systems](01_google_cloud_well_architected_framework/04_reliability/03_build_highly_available_systems.md)
    *   [Design for Scale](01_google_cloud_well_architected_framework/04_reliability/04_design_scale_high_availability.md)
    *   [Observability](01_google_cloud_well_architected_framework/04_reliability/05_observability.md)
    *   [Graceful Degradation](01_google_cloud_well_architected_framework/04_reliability/06_graceful_degradation.md)
    *   [Recovery Testing](01_google_cloud_well_architected_framework/04_reliability/07_perform_testing_for_recovery_from_failures.md)
    *   [Data Loss Recovery](01_google_cloud_well_architected_framework/04_reliability/08_perform_testing_for_recovery_from_data_loss.md)
    *   [Postmortems](01_google_cloud_well_architected_framework/04_reliability/09_conduct_postmortems.md)

*   **5. Performance Efficiency**
    *   [Plan Resource Allocation](01_google_cloud_well_architected_framework/05_performance_efficiency/01_plan_resource_allocation.md)
    *   [Elasticity](01_google_cloud_well_architected_framework/05_performance_efficiency/02_elasticity.md)
    *   [Modular Design](01_google_cloud_well_architected_framework/05_performance_efficiency/03_promote_modular_design.md)
    *   [Monitor and Improve](01_google_cloud_well_architected_framework/05_performance_efficiency/04_continuously_monitor_and_improve_performance.md)

*   **6. Sustainability**
    *   [Sustainability Overview](01_google_cloud_well_architected_framework/06_sustainability/01_sustainability.md)

*   **7. Cross-Pillar Perspectives**
    *   **AI & ML**: [Ops](01_google_cloud_well_architected_framework/07_cross_pillar_perspectives/01_ai_and_ml/01_operational_excellence.md), [Security](01_google_cloud_well_architected_framework/07_cross_pillar_perspectives/01_ai_and_ml/02_security.md), [Reliability](01_google_cloud_well_architected_framework/07_cross_pillar_perspectives/01_ai_and_ml/03_reliability.md), [Performance](01_google_cloud_well_architected_framework/07_cross_pillar_perspectives/01_ai_and_ml/04_performance_optimization.md), [Cost](01_google_cloud_well_architected_framework/07_cross_pillar_perspectives/01_ai_and_ml/05_cost_optimization.md).
    *   **Financial Services**: [Ops](01_google_cloud_well_architected_framework/07_cross_pillar_perspectives/02_financial_services_industry/01_operational_excellence.md), [Security](01_google_cloud_well_architected_framework/07_cross_pillar_perspectives/02_financial_services_industry/02_security.md), [Reliability](01_google_cloud_well_architected_framework/07_cross_pillar_perspectives/02_financial_services_industry/03_reliability.md), [Performance](01_google_cloud_well_architected_framework/07_cross_pillar_perspectives/02_financial_services_industry/04_performance_optimization.md), [Cost](01_google_cloud_well_architected_framework/07_cross_pillar_perspectives/02_financial_services_industry/05_cost_optimization.md).

## 2. Deployment Archetypes
Strategies for locating workloads based on availability, latency, and cost.

*   [Zonal](02_deployment_archetypes/01_zonal.md)
*   [Regional](02_deployment_archetypes/02_regional.md)
*   [Multi-regional](02_deployment_archetypes/03_multiregional.md)
*   [Global](02_deployment_archetypes/04_global.md)
*   [Hybrid](02_deployment_archetypes/05_hybrid.md)
*   [Multicloud](02_deployment_archetypes/06_multicloud.md)
*   [Comparison Guide](02_deployment_archetypes/07_comparison.md)
*   **Reference Architectures**:
    *   [Single-zone (CE)](02_deployment_archetypes/08_reference_architectures/01_single_zone_deployment_compute_engine.md)
    *   [Regional (CE)](02_deployment_archetypes/08_reference_architectures/02_regional_deployment_compute_engine.md)
    *   [Multi-regional (CE)](02_deployment_archetypes/08_reference_architectures/03_multiregional_vms.md)
    *   [Global (CE + Spanner)](02_deployment_archetypes/08_reference_architectures/04_global_deployment_compute_engine_spanner.md)

## 3. Landing Zone Design
Decisions and best practices for creating a cloud foundation.

*   [Overview](03_landing_zone_design/01_landing_zone_design.md)
*   [Identity Onboarding](03_landing_zone_design/02_decide_how_to_onboard_identities.md)
*   [Resource Hierarchy](03_landing_zone_design/03_decide_resource_hierarchy.md)
*   [Network Decision](03_landing_zone_design/04_decide_network_design.md)
*   [Security Decision](03_landing_zone_design/05_decide_security.md)
*   [Network Implementation](03_landing_zone_design/06_implement_network_design.md)

## 4. Enterprise Foundation Blueprint
A comprehensive, opinionated guide for a secure production environment (formerly Security Foundations Blueprint).

*   [Overview](04_enterprise_foundation_blueprint/01_enterprise_foundation_blueprint.md)
*   [Authentication & Authorization](04_enterprise_foundation_blueprint/02_authentication_and_authorization.md)
*   [Organization Structure](04_enterprise_foundation_blueprint/03_organization_structure.md)
*   [Networking](04_enterprise_foundation_blueprint/04_networking.md)
*   [Detective Controls](04_enterprise_foundation_blueprint/05_detective_controls.md)
*   [Preventative Controls](04_enterprise_foundation_blueprint/06_preventative_controls.md)
