# Course Creation Guide

## Overview

This guide provides a complete specification for autonomously creating and registering courses in the course-repo. It covers the entire workflow from understanding the repository structure to pushing course configurations to GitHub.

## Course Repository Architecture

### Directory Structure
```
course-repo/
├── config/
│   ├── courses.json                 # Main navigation entries
│   ├── categories.json              # Top-level categories
│   ├── pocs.json                    # POC (Proof of Concept) entries
│   ├── blogs.json                   # Blog entries
│   ├── cloud/
│   │   ├── cloud.json               # Cloud category index
│   │   ├── azure.json               # Azure courses
│   │   ├── aws.json                 # AWS courses
│   │   └── gcp.json                 # GCP courses
│   ├── data-science/
│   │   └── data-science.json        # Data Science courses
│   ├── gen-ai/
│   │   ├── gen-ai.json              # GenAI category index
│   │   └── prompt-engineering.json  # Prompt Engineering courses
│   └── devops/
│       ├── devops.json              # DevOps category index
│       └── devops-fundamentals.json # DevOps Fundamentals course
```

## Configuration File Hierarchy

### 1. courses.json (Navigation Level)
Defines main navigation items pointing to configuration files.

```json
[
  {
    "id": "all-courses",
    "title": "All Courses",
    "type": "navigation",
    "configFile": "config/categories.json"
  },
  {
    "id": "poc",
    "title": "POC",
    "type": "navigation",
    "configFile": "config/pocs.json"
  }
]
```

### 2. categories.json (Category Level)
Lists all top-level course categories.

```json
[
  {
    "id": "cloud",
    "title": "Cloud",
    "type": "category",
    "configFile": "config/cloud/cloud.json"
  },
  {
    "id": "devops",
    "title": "DevOps",
    "type": "category",
    "configFile": "config/devops/devops.json"
  }
]
```

### 3. Category Index File (e.g., devops.json)
Lists subcategories within a category, pointing to their config files.

```json
[
  {
    "id": "devops-fundamentals",
    "title": "DevOps Fundamentals",
    "type": "subcategory",
    "configFile": "config/devops/devops-fundamentals.json"
  }
]
```

### 4. Course Entry File (e.g., devops-fundamentals.json)
Defines individual courses with full metadata.

```json
[
  {
    "id": "devops-fundamentals-course",
    "title": "DevOps Fundamentals",
    "type": "course",
    "description": "Master DevOps principles, CI/CD pipelines, and infrastructure automation.",
    "author": "Vinod Seth",
    "thumbnail": "/devops_thumbnail.png",
    "tags": ["DevOps", "CI/CD", "Azure", "Infrastructure"],
    "repository": {
      "owner": "vinod-seth",
      "name": "devops-fundamentals",
      "branch": "main"
    }
  }
]
```

## Course Entry Specification

### Required Fields
| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `id` | string | Unique course identifier (lowercase with hyphens) | `"devops-fundamentals-course"` |
| `title` | string | Course display title | `"DevOps Fundamentals"` |
| `type` | string | Must be `"course"` | `"course"` |
| `description` | string | Detailed course description | `"Master DevOps principles..."` |
| `author` | string | Course author name | `"Vinod Seth"` |
| `thumbnail` | string | Path or URL to course thumbnail | `"/devops_thumbnail.png"` |
| `tags` | array | Course topics/keywords | `["DevOps", "CI/CD", "Azure"]` |
| `repository` | object | GitHub repository details | See below |

### Repository Object
```json
{
  "owner": "vinod-seth",
  "name": "course-repo-name",
  "branch": "main"
}
```

## Course Creation Workflow

### Step 1: Determine Course Category
- Check if category exists in `config/categories.json`
- If new category needed, create `config/{category-id}/{category-id}.json`
- Add entry to `categories.json`

### Step 2: Create Category Index (if new category)
Create `config/{category-id}/{category-id}.json`:
```json
[
  {
    "id": "{subcategory-id}",
    "title": "Subcategory Title",
    "type": "subcategory",
    "configFile": "config/{category-id}/{subcategory-id}.json"
  }
]
```

### Step 3: Create Course Entry File
Create `config/{category-id}/{course-id}.json`:
```json
[
  {
    "id": "{course-id}-course",
    "title": "Course Title",
    "type": "course",
    "description": "Detailed course description",
    "author": "Author Name",
    "thumbnail": "/thumbnail.png",
    "tags": ["tag1", "tag2"],
    "repository": {
      "owner": "github-username",
      "name": "course-repo-name",
      "branch": "main"
    }
  }
]
```

### Step 4: Update categories.json (if new category)
Add new category entry:
```json
{
  "id": "{category-id}",
  "title": "Category Title",
  "type": "category",
  "configFile": "config/{category-id}/{category-id}.json"
}
```

### Step 5: Git Operations
```bash
# Navigate to course-repo
cd course-repo

# Stage all config changes
git add config/

# Commit changes
git commit -m "Add {CourseTitle} course config"

# Push to main branch
git push origin main
```

## Naming Conventions

### ID Format
- Use lowercase letters and hyphens
- Pattern: `{category}-{subcategory}-{course-name}`
- Examples:
  - `cloud-azure-ai`
  - `devops-fundamentals-course`
  - `data-science-ml-basics`

### File Paths
- Category: `config/{category-id}/`
- Files: `{category-id}.json` or `{subcategory-id}.json`

### Repository Names
- Use descriptive, kebab-case names
- Examples:
  - `devops-fundamentals`
  - `azure-ai-content`
  - `prompt-engineering-mastery`

## Validation Checklist

Before pushing to repository:
- [ ] All JSON files are valid (no syntax errors)
- [ ] Course entry has all required fields
- [ ] IDs follow naming convention (lowercase, hyphens)
- [ ] `configFile` paths match actual file locations
- [ ] Repository information is accurate
- [ ] Tags are relevant and descriptive
- [ ] Description is clear and informative
- [ ] Author field is populated
- [ ] Thumbnail is accessible (local path or valid URL)

## Git Workflow

### Initial Setup
```bash
# Clone or initialize repository
git clone https://github.com/vinod-seth/course-repo.git
cd course-repo

# Or if initializing fresh:
git init
git remote add origin https://github.com/vinod-seth/course-repo.git
```

### Adding Course Configs
```bash
# Create/update config files
# config/categories.json (add entry if new category)
# config/{category-id}/{category-id}.json (if new category)
# config/{category-id}/{course-id}.json (course entry)

# Stage changes
git add config/

# Commit with descriptive message
git commit -m "Add {CourseName} course config"

# Handle merge conflicts if pulling from remote
git pull origin main --allow-unrelated-histories

# Push to main
git push origin main
```

## Example: Adding DevOps Fundamentals Course

### Files Created
1. `config/devops/devops.json`
2. `config/devops/devops-fundamentals.json`

### Changes to Existing Files
- Updated `config/categories.json` to add DevOps entry

### devops.json Content
```json
[
  {
    "id": "devops-fundamentals",
    "title": "DevOps Fundamentals",
    "type": "subcategory",
    "configFile": "config/devops/devops-fundamentals.json"
  }
]
```

### devops-fundamentals.json Content
```json
[
  {
    "id": "devops-fundamentals-course",
    "title": "DevOps Fundamentals",
    "type": "course",
    "description": "Master DevOps principles, CI/CD pipelines, infrastructure automation, and deployment strategies on Azure.",
    "author": "Vinod Seth",
    "thumbnail": "/devops_thumbnail.png",
    "tags": ["DevOps", "CI/CD", "Azure", "Infrastructure", "Automation"],
    "repository": {
      "owner": "vinod-seth",
      "name": "devops-fundamentals",
      "branch": "main"
    }
  }
]
```

### categories.json Update
```json
{
  "id": "devops",
  "title": "DevOps",
  "type": "category",
  "configFile": "config/devops/devops.json"
}
```

## Autonomous Course Creation Requirements

For developing an application to autonomously create courses:

### Input Parameters
1. **Course Information**
   - Course name/title
   - Description
   - Author name
   - Tags/topics
   - Thumbnail URL or path

2. **Repository Information**
   - GitHub owner (default: "vinod-seth")
   - Repository name
   - Branch (default: "main")

3. **Category Information**
   - Category ID (existing or new)
   - Category title
   - Subcategory ID (if new)
   - Subcategory title

### Processing Steps
1. Validate all inputs against specifications
2. Check if category exists
3. Generate appropriate config files (JSON)
4. Clone or sync course-repo
5. Create/update configuration files
6. Handle git operations (add, commit, push)
7. Resolve any merge conflicts
8. Verify successful push to main branch

### Output
- Confirmation of course registration
- Links to configuration files
- Course URL path

## Error Handling

### Common Issues & Solutions

**JSON Syntax Errors**
- Validate JSON before pushing
- Check for missing commas, quotes, brackets
- Use JSON linter if available

**Git Merge Conflicts**
- Use `--allow-unrelated-histories` flag if needed
- Manually resolve conflicts in configuration files
- Keep remote version as base, merge in new entries

**Repository Permission Issues**
- Ensure GitHub credentials are configured
- Verify write access to course-repo
- Check SSH keys or personal access tokens

**File Path Errors**
- Verify all `configFile` paths exist
- Use consistent path format: `config/{category}/{file}.json`
- Test file accessibility before pushing

## References

- **Course Repo**: https://github.com/vinod-seth/course-repo
- **Repository Structure**: Nested JSON configuration system
- **Supported Categories**: Cloud, Data Science, GenAI, DevOps
- **Git Workflow**: Standard fork/PR or direct push to main
