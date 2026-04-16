# Hardening Report: jlumbroso--free-disk-space/v1.3.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `c40cfe5fa14e08549b1b988e7e5a26da4816abf0`

**Test Policy SHA:** `f2e7d85641cde4267138117189b8eba7ba2bfbde`

Action **jlumbroso--free-disk-space/v1.3.1** was hardened automatically. 8 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

In action.yml, all seven action inputs are interpolated directly inside the `run:` shell block using `${{ inputs.* }}` expressions instead of being first assigned to environment variables and then referenced as shell variables. This allows an attacker who controls input values (e.g., via a calling workflow or workflow_dispatch) to inject arbitrary shell commands. The affected expressions are:
- `if [[ ${{ inputs.android }} == 'true' ]]` (line ~116)
- `if [[ ${{ inputs.dotnet }} == 'true' ]]` (line ~124)
- `if [[ ${{ inputs.haskell }} == 'true' ]]` (line ~133)
- `if [[ ${{ inputs.large-packages }} == 'true' ]]` (line ~143)
- `if [[ ${{ inputs.docker-images }} == 'true' ]]` (line ~158)
- `if [[ ${{ inputs.tool-cache }} == 'true' ]]` (line ~167)
- `if [[ ${{ inputs.swap-storage }} == 'true' ]]` (line ~176)
Fix: assign each input to an env var (e.g., `INPUT_ANDROID: ${{ inputs.android }}`) and reference `$INPUT_ANDROID` in the shell script instead.

Locations:

- `action.yml:116`
- `action.yml:124`
- `action.yml:133`
- `action.yml:143`
- `action.yml:158`
- `action.yml:167`
- `action.yml:176`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.android }}" appears directly in run: block of step ""; move to env: map

Locations:

- `action.yml:133`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.dotnet }}" appears directly in run: block of step ""; move to env: map

Locations:

- `action.yml:145`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.haskell }}" appears directly in run: block of step ""; move to env: map

Locations:

- `action.yml:158`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.large-packages }}" appears directly in run: block of step ""; move to env: map

Locations:

- `action.yml:172`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.docker-images }}" appears directly in run: block of step ""; move to env: map

Locations:

- `action.yml:194`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.tool-cache }}" appears directly in run: block of step ""; move to env: map

Locations:

- `action.yml:207`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.swap-storage }}" appears directly in run: block of step ""; move to env: map

Locations:

- `action.yml:219`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection

**Notes:**

Fixed all 7 script injection vulnerabilities in hardened/jlumbroso--free-disk-space/v1.3.1/action.yml. Added an `env:` block to the composite action step with INPUT_ANDROID, INPUT_DOTNET, INPUT_HASKELL, INPUT_LARGE_PACKAGES, INPUT_DOCKER_IMAGES, INPUT_TOOL_CACHE, and INPUT_SWAP_STORAGE mapped from their respective `${{ inputs.* }}` expressions. Replaced all 7 inline `${{ inputs.* }}` expressions in the `run:` shell block with the corresponding plain environment variable references ($INPUT_ANDROID, $INPUT_DOTNET, $INPUT_HASKELL, $INPUT_LARGE_PACKAGES, $INPUT_DOCKER_IMAGES, $INPUT_TOOL_CACHE, $INPUT_SWAP_STORAGE). This prevents attacker-controlled input values from being interpreted as shell commands.

