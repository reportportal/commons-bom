# commons-bom
BOM descriptor for JVM-based projects

## Publishing to Maven Central

This project includes GitHub Actions workflows for publishing artifacts to Maven Central.

### Workflows

#### `publish-maven.yml`
Publishes the BOM to Maven Central using the new Sonatype Central service.

**Usage:**
1. Go to the Actions tab in GitHub
2. Select "Publish to Maven Central" workflow
3. Click "Run workflow"
4. Enter the version to publish
5. Optionally enable dry run mode

**Required Secrets:**
- `SONATYPE_USER`: Your Sonatype username
- `SONATYPE_PASSWORD`: Your Sonatype password/token
- `GPG_PRIVATE_KEY`: Your GPG private key for signing artifacts
- `GPG_PASSPHRASE`: Passphrase for your GPG key

**Note:** The workflow uses the new Sonatype Central service (`central.sonatype.com`) instead of the deprecated OSSRH service.

#### `promote.yml`
Legacy workflow for promoting artifacts from GitHub Packages to Maven Central (deprecated).

### Setup Instructions

1. **Sonatype Account**: Ensure you have a Sonatype account and access to publish to Maven Central
2. **GPG Key**: Generate and configure a GPG key for signing artifacts
3. **Secrets**: Add the required secrets to your GitHub repository settings
4. **Distribution Management**: The `pom.xml` is configured with both Maven Central and GitHub Packages distribution management

### Version Management

The workflow automatically updates the version in `pom.xml` based on the input parameter. Make sure the version follows semantic versioning conventions.
