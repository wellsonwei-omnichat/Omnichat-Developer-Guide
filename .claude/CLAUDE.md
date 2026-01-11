# CLAUDE.md - Omnichat Developer Guide

This file provides guidance to Claude Code when working with the Omnichat Developer Guide documentation repository.

## Project Overview

This is the **Omnichat Developer Guide** documentation repository, designed for use with [ReadMe.io](https://readme.com/) - a developer hub platform that provides interactive API documentation.

The repository uses **ReadMe's bi-directional sync** feature, allowing documentation to be maintained in Git and automatically synced to the ReadMe platform.

**ReadMe Project URL**: https://omnichat.readme.io/ (public documentation site)

## Repository Structure

```
Omnichat-Developer-Guide/
├── .claude/
│   └── CLAUDE.md              # This file - AI assistant guidance
├── .gitignore                 # Git ignore rules
├── docs/                      # Guide documentation (tutorials, concepts)
│   ├── _order.yaml            # Controls section ordering
│   ├── documentation/         # Getting started guides
│   ├── open API/              # Open API documentation
│   ├── webhook/               # Webhook integration docs
│   ├── 3rd-party AI Agent Integration/  # AI agent integration
│   └── self-built ec platform (deprecated)/  # Legacy EC integration
├── reference/                 # API Reference documentation
│   ├── _order.yaml            # Controls section ordering
│   ├── chatbot.json           # OpenAPI spec for Chatbot API
│   ├── Chatbot/               # Chatbot API supplementary docs
│   ├── Chatbot Dynamic Response API/  # Dynamic response docs
│   ├── Conversion API/        # Conversion tracking API docs
│   └── ReadMeConfig/          # ReadMe platform configuration
└── custom_pages/              # Custom landing/marketing pages
    ├── _order.yaml            # Controls page ordering
    └── 網站用戶行為追蹤.md    # Website behavior tracking
```

## Content Types

### 1. Guide Documentation (`docs/`)

Tutorial and conceptual documentation. These are freeform Markdown pages that explain concepts, workflows, and integration guides.

**Sections:**
- **documentation/** - Getting started guide
- **open API/** - Omnichat Open API documentation (Authorization, Contacts, Broadcast, Channels, Rooms, LINE Rich Menu, Notification Messages, Bulk Orders)
- **webhook/** - Webhook subscription and event topics
- **3rd-party AI Agent Integration/** - Integration guide for third-party AI agents
- **self-built ec platform (deprecated)/** - Legacy e-commerce integration (deprecated)

### 2. API Reference (`reference/`)

API specifications and reference documentation.

**Sections:**
- **chatbot.json** - OpenAPI 3.1.0 specification for Chatbot API
- **Chatbot/** - Supplementary documentation for Chatbot API
- **Chatbot Dynamic Response API/** - Dynamic response configuration
- **Conversion API/** - Conversion tracking API
- **ReadMeConfig/** - ReadMe platform configuration (authentication, getting started, my-requests)

### 3. Custom Pages (`custom_pages/`)

Custom landing pages or special content pages.

## File Conventions

### Markdown Files (.md)

All Markdown files use **YAML frontmatter** for metadata:

```yaml
---
title: Page Title
excerpt: Short description of the page
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
```

**Frontmatter Fields:**
| Field | Description |
|-------|-------------|
| `title` | Page title displayed in ReadMe |
| `excerpt` | Short description/subtitle |
| `deprecated` | Mark page as deprecated (boolean) |
| `hidden` | Hide from navigation but accessible via URL (boolean) |
| `metadata.robots` | SEO robots directive (`index` or `noindex`) |
| `next.description` | Description for "next page" navigation |
| `fullscreen` | Enable fullscreen mode for custom pages |
| `api_config` | Link to API configuration (for reference pages) |

### Order Files (`_order.yaml`)

Each folder contains an `_order.yaml` file that controls the display order of pages/sections:

```yaml
- authorization
- send-notification-messages-to-contacts
- bulk-upsert-orders-api
- line-rich-menu-api
```

**Note:** The order is defined by the **slug** (filename without .md extension), not the full filename.

### OpenAPI Specifications (.json)

API specifications follow the **OpenAPI 3.1.0** format:

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "API Title",
    "version": "1.0"
  },
  "servers": [...],
  "paths": {...},
  "components": {...}
}
```

**ReadMe-specific Extensions:**
- `x-readme.code-samples` - Custom code samples for API endpoints
- `x-readme.samples-languages` - Supported languages for code samples
- `x-readme.explorer-enabled` - Enable API explorer
- `x-readme.proxy-enabled` - Enable request proxy

## ReadMe-Specific Features

### Custom Components

ReadMe supports special JSX-like components in Markdown:

```markdown
<!-- Glossary term with hover tooltip -->
<Glossary>term</Glossary>

<!-- Custom table with alignment -->
<Table align={["left","left"]}>
  <thead>...</thead>
  <tbody>...</tbody>
</Table>
```

### Callouts

Use standard Markdown blockquotes with emoji prefixes:

```markdown
> 📘 Info callout
> This is an informational note.

> ⚠️ Warning callout
> This is a warning.

> 🚧 Under construction
> This feature is in development.
```

### Images

Images can be referenced from external URLs or Owlbert (ReadMe's mascot):
```markdown
![Alt text](https://owlbert.io/images/popper.gif)
```

## API Documentation

### Base URLs

| API | Base URL |
|-----|----------|
| Chatbot API | `https://open-api.omnichat.ai/v1/chatbots` |
| Open API | `https://open-api.omnichat.ai/v1` |

### Authentication

All APIs use **Bearer Token** authentication:
```
Authorization: Bearer <API_TOKEN>
```

## Documented APIs

### Open API (`docs/open API/`)
- **Authorization** - API authentication guide
- **Contacts API** - Customer/contact management
- **Channels API** - Social channel management
- **Rooms API** - Conversation room operations
- **Broadcast API** - Bulk messaging
- **LINE Rich Menu API** - LINE rich menu management
- **Send Notification Messages** - Push notifications to contacts
- **Bulk Upsert Orders API** - Order data import

### Webhook Topics (`docs/webhook/`)
- **customer/create** - New customer created
- **customer/update** - Customer data updated
- **conversation/create** - New conversation started
- **conversation/update** - Conversation updated
- **message/create** - New message received/sent

### Chatbot API (`reference/chatbot.json`)
- `GET /` - Get chatbot list
- `GET /{chatbotId}/message-blocks` - Get chatbot message blocks

### 3rd-Party AI Agent Integration
- Agent message API for receiving and sending messages
- Webhook integration for AI agent responses

## Development Workflow

### Local Development

1. Clone the repository
2. Edit Markdown files or OpenAPI specs
3. Commit and push changes
4. ReadMe automatically syncs via GitHub integration

### Adding New Documentation

1. Create a new `.md` file in the appropriate folder
2. Add YAML frontmatter with required fields
3. Update `_order.yaml` to include the new page slug
4. Commit and push

### Updating API Specifications

1. Edit the relevant `.json` file in `reference/`
2. Ensure OpenAPI 3.1.0 compliance
3. Add `x-readme` extensions for enhanced documentation
4. Commit and push

## Related Services

This documentation covers APIs provided by the following backend services:

| API/Feature | Backend Service |
|-------------|-----------------|
| Open API | camelot |
| Contacts API | nexus |
| Chatbot API | camelot |
| Webhook | webhook-sending-service |
| AI Agent Integration | gemini, omni-ai |
| Broadcast | broadcast-service |

## Best Practices

### Writing Documentation

1. **Keep titles concise** - Use clear, descriptive titles
2. **Add excerpts** - Provide helpful page descriptions
3. **Use tables** - For structured data like field descriptions
4. **Include code samples** - Show practical examples
5. **Mark deprecated content** - Set `deprecated: true` for outdated pages
6. **Hide work-in-progress** - Set `hidden: true` until ready

### Maintaining Order

1. Place most important/common pages first in `_order.yaml`
2. Group related content in subfolders
3. Use clear, URL-friendly slugs (kebab-case)

### API Documentation

1. Provide complete request/response examples
2. Document all possible error codes
3. Include authentication requirements
4. Add curl examples for quick testing

## Troubleshooting

### Common Issues

1. **Page not showing in ReadMe** - Check `hidden: false` in frontmatter
2. **Wrong page order** - Update `_order.yaml` file
3. **API not rendering** - Validate OpenAPI spec format
4. **Sync issues** - Check GitHub integration in ReadMe dashboard

## Resources

- [ReadMe Documentation](https://docs.readme.com/)
- [OpenAPI 3.1.0 Specification](https://spec.openapis.org/oas/v3.1.0)
- [ReadMe GitHub Sync](https://docs.readme.com/main/docs/github-sync)
