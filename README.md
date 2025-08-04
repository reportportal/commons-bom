# commons-bom
BOM descriptor for JVM-based projects

## Publishing to Maven Central

This project includes automated workflows for publishing to Maven Central using the new Sonatype Central API.

### Available Workflows

#### 1. Maven Publish to Central (`maven-publish.yml`)

**Purpose**: Publishes artifacts directly to Maven Central using the new Sonatype Central API.

**Features**:
- Downloads artifacts from GitHub Packages
- Creates deployment bundles
- Uploads to Sonatype Central with automatic publishing
- Monitors deployment status
- Provides detailed logging and error handling

**Usage**:
1. Go to the Actions tab in GitHub
2. Select "Maven Publish to Central" workflow
3. Click "Run workflow"
4. Enter the version to publish (e.g., `5.14.4`)
5. Click "Run workflow"

**Required Secrets**:
- `SONATYPE_USER`: Your Sonatype Central username
- `SONATYPE_PASSWORD`: Your Sonatype Central password/token
- `GITHUB_TOKEN`: Automatically provided by GitHub Actions

**Artifacts Downloaded**:
- `commons-bom-{version}.pom`
- `commons-bom-{version}.pom.asc` (GPG signature)
- `commons-bom-{version}.pom.md5` (MD5 checksum)
- `commons-bom-{version}.pom.sha1` (SHA1 checksum)

#### 2. Legacy Promote Workflow (`promote.yml`)

**Purpose**: Legacy workflow using the old OSSRH staging repository API.

**Note**: This workflow is maintained for backward compatibility but the new `maven-publish.yml` is recommended for new releases.

### API References

- [Sonatype Central API Documentation](https://central.sonatype.com/api-doc)
- [Central Publisher API Guide](https://central.sonatype.org/publish/publish-portal-api/)

### Authentication

The workflows use token-based authentication with Sonatype Central:
- Username and password are base64 encoded
- Bearer token authentication is used for API requests
- Automatic publishing is enabled by default

### Deployment States

The workflow monitors these deployment states:
- `PENDING`: Uploaded and waiting for processing
- `VALIDATING`: Being processed by validation service
- `VALIDATED`: Passed validation, waiting for manual publish (if not automatic)
- `PUBLISHING`: Being uploaded to Maven Central
- `PUBLISHED`: Successfully published to Maven Central
- `FAILED`: Encountered an error during processing
