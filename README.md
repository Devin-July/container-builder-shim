# container-builder-shim

**container-builder-shim** is a lightweight bridge that connects BuildKit's session protocol with containerization's Build API. It enables compatibility between BuildKit (the build engine behind Docker) and containerization by translating messages and file transfers between their respective APIs.

## What It Does

- **Protocol Translation:**
  - Translates session protocol messages from BuildKit into requests understood by containerization.

- **Session Management:**
  - Handles file synchronization, image resolution, build output streaming, and caching.

## Key Components

- **FSSync:** Transfers local files required for builds.
- **Resolver:** Resolves image references and tags.
- **ContentStore:** Retrieves and caches build dependencies like base images and layers.
- **Exporter:** Provides the final built image, including metadata and manifests.
- **IO Stream:** Streams real-time build logs and progress updates.

## How It Works

![922e463d-d2cb-4e27-bf22-96ed54770305](https://github.com/user-attachments/assets/461930a4-cfab-4b91-ae3b-dee225cdc461)

1. BuildKit initiates a session via gRPC.
2. container-builder-shim intercepts session requests (file sync, image resolution, etc.).
3. Requests are translated to containerization's Build API format.
4. containerization processes the build.
5. Build output and metadata flow back through container-builder-shim to BuildKit.

## Development

### Code Quality

This project uses [GolangCI-Lint](https://golangci-lint.run/) for code quality checks. To run the linter locally:

1. **Install golangci-lint:**
   ```bash
   # macOS (using Homebrew)
   brew install golangci-lint
   
   # Linux/macOS (using install script)
   curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin v1.55.2
   
   # Or follow the installation guide: https://golangci-lint.run/welcome/install/
   ```

2. **Run the linter:**
   ```bash
   make lint
   ```

The linter configuration is defined in `.golangci.yml` and is integrated into the CI pipeline.

## Contributing

Contributions to Containerization are welcomed and encouraged. Please see our [main contributing guide](https://github.com/apple/containerization/blob/main/CONTRIBUTING.md) for more information.

