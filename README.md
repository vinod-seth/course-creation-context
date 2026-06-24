# Course Creation Context

A comprehensive guide and specification for autonomously creating and registering courses in the [course-repo](https://github.com/vinod-seth/course-repo).

## Overview

This repository contains all the knowledge and specifications needed to develop an application that can autonomously:
- Create course configuration files
- Register courses in the course-repo
- Manage course metadata and repository links
- Handle Git workflows for course registration

## Contents

- **[COURSE_CREATION_GUIDE.md](COURSE_CREATION_GUIDE.md)** - Complete course creation specification including:
  - Repository architecture and structure
  - Configuration file hierarchy
  - Course entry specifications
  - Step-by-step workflow
  - Naming conventions
  - Validation checklist
  - Git workflow
  - Error handling
  - Example implementations

## Key Features

### Course Structure
- Hierarchical organization: Navigation → Categories → Subcategories → Courses
- JSON-based configuration system
- Flexible metadata storage
- GitHub repository integration

### Supported Categories
- Cloud (Azure, AWS, GCP)
- Data Science
- GenAI
- DevOps
- Extensible for new categories

### Course Entry Fields
- Course ID and title
- Detailed description
- Author information
- Tags and keywords
- Thumbnail/media
- GitHub repository details (owner, repo name, branch)

## Quick Start

To create a new course:

1. **Determine Category**: Check if course fits in existing category or needs new one
2. **Create Config Files**: 
   - Category index file (if new category)
   - Course entry file with metadata
3. **Update categories.json**: Add new category entry if needed
4. **Git Operations**: Stage, commit, and push to main branch

See [COURSE_CREATION_GUIDE.md](COURSE_CREATION_GUIDE.md) for detailed instructions.

## Example Use Case

Creating "DevOps Fundamentals" course:

```
Files Created:
- config/devops/devops.json
- config/devops/devops-fundamentals.json

Files Updated:
- config/categories.json (added DevOps category)

Result:
DevOps category with "DevOps Fundamentals" course registered in course-repo
```

## Application Development

This context is designed for developers building autonomous course creation applications. Use this guide to:
- Understand the course registration system
- Implement file generation logic
- Automate Git workflows
- Validate course metadata
- Handle errors and edge cases

## Course-Repo Integration

All configurations reference the main [course-repo](https://github.com/vinod-seth/course-repo):
- Owner: `vinod-seth`
- Repository: `course-repo`
- Main branch: `main`

Individual courses reference their own repositories with author/name/branch information.

## License

MIT - Use freely for course creation and development applications

## Author

Created by: Vinod Seth
Date: 2026-06-24
