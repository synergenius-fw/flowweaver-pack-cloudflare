# @synergenius/flow-weaver-pack-cloudflare

Cloudflare Workers export target for [Flow Weaver](https://github.com/synergenius-fw/flow-weaver).

Generates Cloudflare Workers with Wrangler configuration from Flow Weaver workflows.

## Installation

```bash
npm install @synergenius/flow-weaver-pack-cloudflare
```

This package is a **marketplace pack** — once installed, Flow Weaver automatically discovers it via `createTargetRegistry()`.

## Usage

### CLI

```bash
# Export a workflow as a Cloudflare Worker
npx flow-weaver export my-workflow.ts --target cloudflare

# With options
npx flow-weaver export my-workflow.ts --target cloudflare --production --docs
```

### Programmatic

```typescript
import { createTargetRegistry } from '@synergenius/flow-weaver/deployment';

const registry = await createTargetRegistry(process.cwd());
const cf = registry.get('cloudflare');

const artifacts = await cf.generate({
  sourceFile: 'my-workflow.ts',
  workflowName: 'myWorkflow',
  displayName: 'my-workflow',
  outputDir: './dist/cloudflare',
  production: true,
});
```

## What it generates

- `src/worker.ts` — Cloudflare Worker handler
- `wrangler.toml` — Wrangler configuration
- `package.json` — Dependencies and scripts
- Optional: Swagger UI docs at `/docs`

Supports single workflow, multi-workflow (router), node type services, and bundle exports.

## Requirements

- `@synergenius/flow-weaver` >= 0.14.0

## License

See [LICENSE](./LICENSE).
