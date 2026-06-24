# Template Library

## Purpose
Central repository of templates used to generate course content and assessments.

## Template Types
- Course README template
- Module overview template
- Lesson markdown template
- Quiz (markdown) template
- Lab instructions (step-by-step)
- Code sample templates per language

## Template Structure
- `templates/{domain}/{course-type}/{template-name}.md.j2`
- Support variables: `{{title}}`, `{{learning_objectives}}`, `{{prereqs}}`, `{{code_samples}}`

## Example: Lesson Template

````
# {{lesson.title}}

## Objective

{{lesson.objective}}

## Content

{{lesson.content}}

## Exercise

{{lesson.exercise}}
````

## Versioning
- Template semver
- Changelog for breaking changes

## Contribution Guidelines
- PRs for new templates
- Lint templates before merge
