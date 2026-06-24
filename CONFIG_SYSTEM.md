# Flexible Config System

## Goals
- Represent hierarchical course catalog
- Support multiple config patterns (indexed files, inline children)
- Easy to read and update by humans and tools

## File Patterns
- `config/courses.json` - navigation
- `config/categories.json` - top categories
- `config/{category}/{index}.json` - category index
- `config/{category}/{subcategory}.json` - subcategory or course lists

## Best Practices
- Keep arrays of objects, avoid deeply nested anonymous arrays
- Use `configFile` pointers where lists are long
- Use consistent keys: `id`, `title`, `type`, `description`, `author`, `thumbnail`, `tags`, `repository`

## JSON Schema
Include `course-schema.json` in repo root for validation.

## Migration Strategy
- Backwards-compatible additions only
- Provide validation tool that can auto-fix common issues
