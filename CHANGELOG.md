# Change Log

All notable changes to this project will be documented in this file.

<a name="unreleased"></a>
## [Unreleased]

<a name="1.0.0"></a>
## [1.0.0] - 2021-11-29

- Stable version including dependent charts, and a little ability to customize to my personal needs.
- added k8s version constraints for >= 1.19 < 1.22 for reasons. 
- changed values.yaml to seed subcharts. 
- created values.standalone.patch.yaml to disable all sub charts when reusing this chart.
- changed README.md deploy notes to correctly seed subcharts.
- changed ingress host secretName to {issuer.metadata.name}. I believe this should alleviate issues deploying the chart twice.