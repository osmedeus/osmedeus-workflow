# Community Workflow for Osmedeus

<p align="center">
  <a href="https://github.com/j3ssie/osmedeus"><img alt="Osmedeus" src="https://raw.githubusercontent.com/osmedeus/assets/main/osm-logo-with-white-border.png" height="120" /></a>
  <br />
  <strong>A basic reconnaissance methodology workflow for the <a href="https://github.com/j3ssie/osmedeus">Osmedeus Engine</a></strong>
</p>

This repository provides a reference workflow implementation demonstrating basic reconnaissance methodology. Use it as a starting point to understand Osmedeus workflows and build your own custom automation pipelines.

## Installation

```bash
osmedeus install workflow https://github.com/osmedeus/osmedeus-workflow.git
```

See [Osmedeus documentation](https://docs.osmedeus.org/workflows/overview) for more details.

## Reconnaissance Methodology

The workflow follows a phased approach to reconnaissance:

```
┌─────────────────┐
│   Subdomain     │  Phase 1: Discover subdomains using multiple sources
│   Enumeration   │  (subfinder, findomain, assetfinder, amass)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│    Probing      │  Phase 2: DNS resolution and HTTP probing
│  (DNS + HTTP)   │  (puredns, massdns, httpx, dnsx)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Fingerprint    │  Phase 3: Technology detection and fingerprinting
└────────┬────────┘
         │
    ┌────┴────┬──────────┬──────────┐
    ▼         ▼          ▼          ▼
┌───────┐ ┌───────┐ ┌─────────┐ ┌─────────┐
│Screen │ │Archive│ │IP Space │ │Portscan │  Phase 4+: Parallel analysis
│ shot  │ │       │ │  Enum   │ │         │
└───┬───┘ └───┬───┘ └────┬────┘ └────┬────┘
    │         │          │           │
    └─────────┴──────────┴───────────┘
              │
    ┌─────────┴───────────────┐
    ▼                         ▼
┌─────────────────┐      ┌───────────┐
│Vulnerability    │      │ Content   │  Final: Vulnerability and content discovery
│ Scanning        │      │ Discovery │
└─────────────────┘      └───────────┘
```

## Available Workflows

### Flow Workflows

| Workflow | Description |
|----------|-------------|
| `general.yaml` | Full reconnaissance pipeline with all phases |
| `fast.yaml` | Quick reconnaissance with essential phases only |

### Module Workflows (common/)

| Module | Description |
|--------|-------------|
| `subdomain.yaml` | Subdomain enumeration (subfinder, findomain, assetfinder) |
| `probing.yaml` | DNS resolution and HTTP probing |
| `fingerprint.yaml` | Technology fingerprinting |
| `screenshot.yaml` | Visual screenshots of discovered assets |
| `archive.yaml` | Archive/wayback machine data collection |
| `ipspace.yaml` | IP space enumeration |
| `portscan.yaml` | Port scanning |
| `vulnscan.yaml` | Vulnerability scanning |
| `content-discovery.yaml` | Directory and content bruteforcing |
| `spider.yaml` | Web spidering/crawling |

## Usage

```bash
# Run the general reconnaissance flow
osmedeus run -f general -t example.com

# Run the fast reconnaissance flow
osmedeus run -f fast -t example.com

# Run a specific module
osmedeus run -m subdomain -t example.com

# Dry-run to preview execution
osmedeus run -f general -t example.com --dry-run
```

## Building Your Own Workflow

1. **Study the common modules** - Each module in `common/` demonstrates a specific recon phase
2. **Understand the flow structure** - See `general.yaml` for how modules are orchestrated with dependencies
3. **Customize parameters** - Modules accept params for threads, wordlists, and toggles
4. **Chain modules** - Use `depends_on` to create execution dependencies

Example module structure:

```yaml
kind: module
name: my-module
description: Description of what this module does

params:
  - name: customParam
    default: "value"

dependencies:
  commands:
    - tool1
    - tool2

steps:
  - name: step-one
    type: bash
    command: 'tool1 -t {{Target}} -o {{Output}}/results.txt'
```

## More Examples

For additional workflow examples and patterns, see the [test workflows](https://github.com/j3ssie/osmedeus/tree/main/test/testdata/workflows) in the main Osmedeus repository.

## Documentation

- [Osmedeus Documentation](https://docs.osmedeus.org/)
- [Workflow Overview](https://docs.osmedeus.org/workflows/overview)
- [CLI Reference](https://docs.osmedeus.org/getting-started/cli)

## License

Osmedeus is made with ♥ by [@j3ssie](https://twitter.com/j3ssie) and it is released under the MIT license.
