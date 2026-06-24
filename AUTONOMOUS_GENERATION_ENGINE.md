# Autonomous Generation Engine

## Purpose
Engine that converts input specifications into course configs, content skeletons, and repository changes.

## Responsibilities
- Validate input against schema
- Select templates based on domain and course type
- Render templates (markdown, YAML, code)
- Create config JSON files
- Commit and push changes to the course-repo
- Report results and errors

## Interfaces
- CLI: `create-course --input course.json`
- REST: `/api/create-course`
- Library: `generate_course(course_spec)`

## Core Steps
1. Validate input
2. Resolve taxonomy and template
3. Render course content
4. Write files to repo working tree
5. Git operations (add, commit, pull/merge, push)
6. Verification and reporting

## Template Engine
- Use Jinja2-style syntax
- Support partials and include
- Allow code snippet embedding

## Safety
- Dry-run mode
- Conflict detection
- Audit logging
