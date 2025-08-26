[![Releases](https://img.shields.io/badge/Releases-v_latest-blue?logo=github)](https://github.com/joyrider18/autojd/releases)

AutoJD — AI Job Application Email Generator for Professionals

![Hero image — laptop and coffee](https://images.unsplash.com/photo-1515879218367-8466d910aaa4?ixlib=rb-4.0.3&auto=format&fit=crop&w=1600&q=80)

Overview
- AI-powered tool that generates personalized job application emails in seconds.
- Designed for recruiters, job seekers, and career platforms.
- Works as a web app, CLI, and API client. Built with Next.js, TypeScript, Tailwind CSS, and OpenAI.

Badges
- Topics: ai, automation, career, job-applications, job-search, nextjs, openai, productivity, tailwindcss, typescript
- Language: TypeScript
- Framework: Next.js
- UI: Tailwind CSS

Features
- Generate tailored job application emails from a job posting and a candidate profile.
- Multiple tones: professional, friendly, concise, technical.
- Auto-insert company details, role, and contact lines.
- Versioned templates you can edit and store.
- Bulk mode for batching multiple target companies.
- CLI and API endpoints for automation in pipelines.
- Export to plain text, HTML, PDF, or copy-ready clipboard output.

Why AutoJD
- Save time on repetitive email drafting.
- Keep messaging consistent across applications.
- Use AI to surface relevant keywords and match job requirements.
- Integrate with applicant tracking systems and productivity stacks.

Try the release
- Download and run the latest release file from the Releases page:
  https://github.com/joyrider18/autojd/releases
- The release page contains platform builds and installers. Download the file for your OS and execute the installer or binary (for example: autojd-1.2.0-windows-x64.exe or autojd-1.2.0-linux-x64.tar.gz).

Quick links
- Releases: [![Get Release](https://img.shields.io/badge/Download%20Release-%F0%9F%93%9E-brightgreen)](https://github.com/joyrider18/autojd/releases)
- Repo: https://github.com/joyrider18/autojd

Demo image
![AutoJD demo screenshot](https://images.unsplash.com/photo-1522071820081-009f0129c71c?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&q=80)

Getting started

Web app (local dev)
1. Clone the repo.
2. Install dependencies.
3. Create a .env.local with your OpenAI API key.
4. Start dev server.

Commands
```bash
git clone https://github.com/joyrider18/autojd.git
cd autojd
pnpm install   # or npm install / yarn
cp .env.example .env.local
# set OPENAI_API_KEY in .env.local
pnpm dev
```

CLI
- Use the CLI to generate emails straight from the terminal. The CLI helps you add templates, generate single emails, or run bulk jobs.
Example:
```bash
# generate a single email
autojd gen --job-url "https://jobs.example.com/role" --profile ./profiles/my-profile.json --tone professional

# run bulk
autojd bulk --input companies.csv --output emails.zip
```

Releases and installation files
- Visit https://github.com/joyrider18/autojd/releases to download the installer or binary for your platform.
- The releases page lists assets for macOS, Linux, and Windows. Download the matching file and run the binary or installer.
- Example assets: autojd-1.2.0-macos-universal.dmg, autojd-1.2.0-windows-x64.exe, autojd-1.2.0-linux-x64.tar.gz.
- After download, run the installer or extract and execute the binary:
```bash
# macOS
open autojd-1.2.0-macos-universal.dmg

# Linux
tar -xzf autojd-1.2.0-linux-x64.tar.gz
./autojd

# Windows (PowerShell)
Start-Process .\autojd-1.2.0-windows-x64.exe
```

How it works
- Input: a job posting URL, job text, or manual job fields plus a candidate profile (resume, skills, and preferences).
- Process: AutoJD calls the OpenAI API and applies a set of template prompts. It extracts company and role data, aligns candidate skills to job requirements, and creates a polished email.
- Output: a ready-to-send email with subject, greeting, body, and optional follow-up line.

API
- The repo includes serverless API routes (Next.js API) that accept JSON payloads:
POST /api/generate
Payload example:
```json
{
  "jobTitle": "Frontend Engineer",
  "company": "Acme Corp",
  "jobDescription": "...",
  "candidate": {
    "name": "Jordan Reed",
    "summary": "3 years React, TypeScript",
    "skills": ["React", "TypeScript", "Tailwind CSS"]
  },
  "tone": "professional",
  "format": "html"
}
```
- The API returns a structured response:
```json
{
  "subject": "Application: Frontend Engineer — Jordan Reed",
  "body": "<p>...</p>",
  "plain": "..."
}
```

Templates
- Store and version templates in /templates.
- Each template uses variables and sections. Example variables: {{candidate.name}}, {{company.name}}, {{job.title}}, {{skills}}.
- You can create templates for different tones and roles.

Integrations
- OpenAI: Calls to models pass templates and context. Add your API key in .env.
- ATS / CRM: Use API endpoints or CLI bulk mode to send generated emails into workflows.
- Zapier / Make / Workflows: Use the API endpoints to link AutoJD with Gmail, Outlook, or internal tools.

Customization
- Edit templates to match your voice.
- Add custom prompts or fallback rules for missing job fields.
- Configure token limits and model selection in the config file.

Security and privacy
- Store API keys in environment variables.
- Candidate data stays local unless you enable remote storage or analytics.
- Use encryption for saved profiles if you handle sensitive data.

Performance
- Cache prompt results for identical job-profile pairs.
- Use batching for bulk jobs to reduce API calls.
- The app uses incremental SSR for Next.js to balance latency and cost.

UI and design
- Built with Tailwind CSS and a component library for fast iteration.
- Dark and light themes included.
- Accessible forms and keyboard-first flows.

Developer guide

Project structure (high level)
- /app or /pages — Next.js routes and pages
- /components — UI components (Tailwind)
- /lib — helpers, OpenAI client, parsers
- /templates — email templates
- /cli — CLI entry point
- /scripts — build and release helpers

Local dev tips
- Use ngrok for local webhook testing.
- Use a small model during dev to reduce costs.
- Mock OpenAI responses for unit tests.

Testing
- Unit tests for prompt templates and parsers.
- End-to-end tests for the Next.js app.
- CI runs on push and PRs. Add test coverage checks.

Deployment
- Static and serverless-ready. Deploy on Vercel for Next.js or on any Node host.
- Set environment variables (OPENAI_API_KEY, NEXTAUTH_URL if used, etc.)
- For CLI distribution, releases include platform binaries.

Roadmap
- Add direct Gmail and Outlook send integration.
- Improve keyword alignment and resume parsing.
- Add team templates and shared organization settings.
- Add multi-language support and localization.

Contributing
- Fork the repo.
- Create a branch: feat/your-feature or fix/issue-number.
- Open a PR with a clear description and tests.
- Follow the coding style: TypeScript with strict mode, Tailwind utility classes, and small, focused commits.
- Report issues in GitHub issues with a reproducible sample.

Code of conduct
- Be respectful.
- Keep discussions focused on code and design.
- Follow inclusive language in templates and UI.

FAQ

Q: Can I use my OpenAI account?
A: Yes. Set OPENAI_API_KEY in .env.local or in your deployment environment.

Q: Does AutoJD send emails?
A: AutoJD generates content. You can integrate with Gmail or Outlook to send messages.

Q: Can I edit templates?
A: Yes. Templates live in /templates. Edit them to match your hiring style.

Q: Is there a GUI for bulk uploads?
A: The web app includes a bulk upload page and CLI supports CSV input.

License
- MIT License. See LICENSE file for details

Credits and assets
- Built with Next.js, TypeScript, Tailwind CSS, and OpenAI.
- Hero and demo images from Unsplash.
- Badges generated with img.shields.io

Releases
- Visit https://github.com/joyrider18/autojd/releases to download a release file and execute the installer or binary.