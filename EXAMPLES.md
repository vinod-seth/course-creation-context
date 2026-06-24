# Course Configuration Examples

This directory contains reference examples of course configurations used in the course-repo system.

## Example 1: DevOps Fundamentals Course

### File 1: `config/devops/devops.json`
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

**Purpose**: Category index file that lists subcategories within the DevOps category.

---

### File 2: `config/devops/devops-fundamentals.json`
```json
[
  {
    "id": "devops-fundamentals-course",
    "title": "DevOps Fundamentals",
    "type": "course",
    "description": "Master DevOps principles, CI/CD pipelines, infrastructure automation, and deployment strategies on Azure. Learn version control workflows, GitHub Actions, Azure Pipelines, environment management, secrets management, monitoring, and real-world scaling patterns.",
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

**Purpose**: Course entry file containing metadata for the DevOps Fundamentals course.

---

### File 3: `config/categories.json` (Updated)
```json
[
  {
    "id": "cloud",
    "title": "Cloud",
    "type": "category",
    "configFile": "config/cloud/cloud.json"
  },
  {
    "id": "data-science",
    "title": "Data Science",
    "type": "category",
    "configFile": "config/data-science/data-science.json"
  },
  {
    "id": "gen-ai-cat",
    "title": "GenAI",
    "type": "category",
    "configFile": "config/gen-ai/gen-ai.json"
  },
  {
    "id": "devops",
    "title": "DevOps",
    "type": "category",
    "configFile": "config/devops/devops.json"
  }
]
```

**Purpose**: Main categories list. New DevOps entry added to include the DevOps category.

---

## Example 2: Azure AI Course (Existing)

### File: `config/cloud/azure.json` (Excerpt)
```json
[
  {
    "id": "azure-ai-ml",
    "title": "AI + Machine Learning",
    "type": "subcategory",
    "children": [
      {
        "id": "cloud-azure-ai",
        "title": "Azure AI",
        "type": "course",
        "description": "Implement cognitive services, Azure OpenAI, and custom AI pipelines.",
        "author": "Sophia Lin",
        "thumbnail": "/genai_thumbnail.png",
        "tags": ["Azure", "AI", "Machine Learning"],
        "repository": {
          "owner": "vinod-seth",
          "name": "azure-ai-content",
          "branch": "main"
        }
      }
    ]
  }
]
```

**Note**: Some files use inline `children` array instead of separate `configFile` references.

---

## Example 3: Prompt Engineering Course (Existing)

### File: `config/gen-ai/prompt-engineering.json`
```json
[
  {
    "id": "prompt-engineering-mastery",
    "title": "Prompt Engineering Mastery",
    "type": "course",
    "description": "Master prompt engineering techniques, persona patterns, and anatomy of a perfect prompt.",
    "author": "Vinod Seth",
    "thumbnail": "/genai_thumbnail.png",
    "tags": ["GenAI", "Prompt Engineering", "LLM"],
    "repository": {
      "owner": "vinod-seth",
      "name": "Prompt-Engineering-Mastery",
      "branch": "main"
    }
  }
]
```

**Purpose**: Course entry file for Prompt Engineering Mastery.

---

## Key Patterns

### Pattern 1: New Category with Single Subcategory
Used for DevOps and GenAI:
1. Create `config/{category-id}/{category-id}.json` (index)
2. Create `config/{category-id}/{subcategory-id}.json` (courses)
3. Add entry to `config/categories.json`

### Pattern 2: Category with Multiple Subcategories
Used for Cloud:
1. Create `config/{category-id}/{category-id}.json` (index listing all subcategories)
2. Create `config/{category-id}/{subcategory-id}.json` for each (e.g., azure.json, aws.json)
3. Add entry to `config/categories.json`

### Pattern 3: Inline Children (Alternative)
Some files use inline `"children"` array instead of separate `configFile`:
```json
{
  "id": "subcategory-id",
  "title": "Title",
  "type": "subcategory",
  "children": [
    { "type": "course", ... }
  ]
}
```

---

## Field Reference

### Required Course Fields
| Field | Type | Length | Required |
|-------|------|--------|----------|
| `id` | string | 2-100 chars | Yes |
| `title` | string | 1-200 chars | Yes |
| `type` | string | Always "course" | Yes |
| `description` | string | 10-1000 chars | Yes |
| `author` | string | 1-100 chars | Yes |
| `thumbnail` | string | URL or path | Yes |
| `tags` | array | 1-20 tags | Yes |
| `repository.owner` | string | GitHub username | Yes |
| `repository.name` | string | GitHub repo name | Yes |
| `repository.branch` | string | Default "main" | Yes |

### ID Naming Rules
- Lowercase letters and hyphens only
- No spaces or special characters
- Start with letter
- Maximum 50 characters
- Descriptive and unique
- Examples: `devops-fundamentals-course`, `cloud-azure-ai`, `data-science-ml-basics`

### Tag Guidelines
- 1-20 tags per course
- Relevant to course content
- Capitalize first letter
- Examples: `["DevOps", "CI/CD", "Azure", "Infrastructure"]`

---

## Creation Workflow Summary

1. **Analyze Requirements**
   - Determine category (existing or new)
   - Identify subcategories if needed
   - Gather course metadata

2. **Create Config Files**
   - Category index (if new)
   - Course entry file
   - Follow JSON structure exactly

3. **Update categories.json** (if new category)
   - Add entry in alphabetical order
   - Verify configFile path

4. **Validate**
   - JSON syntax is valid
   - All required fields present
   - IDs are unique and follow naming convention
   - File paths are correct

5. **Git Operations**
   - Clone/sync course-repo
   - Create/modify files
   - Add changes to staging
   - Commit with descriptive message
   - Handle conflicts if needed
   - Push to main branch

6. **Verify**
   - Confirm files exist in repository
   - Verify course appears in listing
   - Check all links resolve correctly
