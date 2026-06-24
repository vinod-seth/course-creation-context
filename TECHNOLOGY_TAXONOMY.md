# Technology Taxonomy

## Purpose
A canonical taxonomy to categorize technologies and support consistent course generation.

## Levels
1. Domain (e.g., DevOps, Cloud, AI)
2. Technology (e.g., Azure, AWS, Kubernetes)
3. Sub-technology (e.g., Azure App Service, EKS)
4. Topic (e.g., Deployment, Monitoring)
5. Course (final product)

## Example
- Domain: Cloud
  - Technology: Azure
    - Sub-tech: App Services
      - Topic: CI/CD
        - Course: "Azure CI/CD with GitHub Actions"

## Taxonomy File Format
Use JSON files under `config/taxonomy/` describing nodes and allowed children.

{
  "id": "cloud",
  "title": "Cloud",
  "children": [
    { "id": "azure", "title": "Azure", "children": [...] }
  ]
}

## Governance
- IDs must be stable and kebab-case
- Owners assigned per domain
- Periodic review process for taxonomy growth
