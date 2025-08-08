# 🌐 Cinny Service

A modular Docker Compose configuration system for Cinny client with support for multiple environments and simplified configuration.

## 🏗️ Project Structure

```sh
src/cinny/
├── components/                              # Source compose components
│   ├── base/                               # Base components
│   │   ├── docker-compose.yml              # Main Cinny service
│   │   └── .env.example                    # Base environment variables
│   ├── environments/                       # Environment components
│   │   ├── devcontainer/
│   │   │   └── docker-compose.yml          # DevContainer environment
│   │   ├── forwarding/
│   │   │   └── docker-compose.yml          # Development with port forwarding
│   │   ├── letsencrypt/
│   │   │   ├── docker-compose.yml          # Let's Encrypt SSL
│   │   │   └── .env.example                # Let's Encrypt variables
│   │   └── step-ca/
│   │       ├── docker-compose.yml          # Step CA SSL
│   │       └── .env.example                # Step CA variables
│   └── extensions/                         # Extension components (currently empty)
│       └── .gitkeep                        # Placeholder for future extensions
├── build/                        # Generated configurations (auto-generated)
│   ├── devcontainer/
│   │   └── base/                 # DevContainer + base
│   ├── forwarding/
│   │   └── base/                 # Development + base
│   ├── letsencrypt/
│   │   └── base/                 # Let's Encrypt + base
│   └── step-ca/
│       └── base/                 # Step CA + base
├── build.sh                      # Build script
└── README.md                     # This file
```

## 🚀 Quick Start

### 1. Build Configurations

Run the build script to generate all possible combinations:

```bash
./build.sh
```

This will create all combinations in the `build/` directory.

### 2. Choose Your Configuration

Navigate to the desired configuration directory:

```bash
# For development with port forwarding
cd build/forwarding/base/

# For DevContainer environment
cd build/devcontainer/base/

# For production with Let's Encrypt SSL
cd build/letsencrypt/base/

# For production with Step CA SSL
cd build/step-ca/base/
```

### 3. Configure Environment

Copy and edit the environment file:

```bash
cp .env.example .env
# Edit .env with your values
```

### 4. Deploy

Start the services:

```bash
docker-compose up -d
```

Access: `http://localhost:3000` (for forwarding mode)

## 🔧 Available Configurations

### Environments

- **devcontainer**: Development environment with workspace network
- **forwarding**: Development environment with port forwarding (3000:80)
- **letsencrypt**: Production with Let's Encrypt SSL certificates
- **step-ca**: Production with Step CA SSL certificates

### Extensions

Currently no extensions are configured. Cinny provides a simple, lightweight Matrix client experience without complex integrations.

### Available Configurations

**Base configurations:**

- `devcontainer/base` - DevContainer development setup
- `forwarding/base` - Development with port forwarding
- `letsencrypt/base` - Production with Let's Encrypt SSL
- `step-ca/base` - Production with Step CA SSL

## 🔧 Environment Variables

### Base Configuration

- `MATRIX_TZ`: Timezone for Cinny services
- `MATRIX_DOMAIN`: Matrix homeserver domain (e.g., matrix.example.com)

### Let's Encrypt Configuration

- `SYNAPSE_SERVER_NAME`: Server name for Cinny (e.g., cinny.example.com)
- `VIRTUAL_PORT`: Port for nginx-proxy (default: 80)
- `VIRTUAL_HOST`: Domain for nginx-proxy
- `LETSENCRYPT_HOST`: Domain for SSL certificate
- `LETSENCRYPT_EMAIL`: Email for certificate registration

### Step CA Configuration

- `SYNAPSE_SERVER_NAME`: Server name for Cinny (e.g., cinny.local)
- `VIRTUAL_PORT`: Port for nginx-proxy (default: 80)
- `VIRTUAL_HOST`: Domain for nginx-proxy
- `LETSENCRYPT_HOST`: Domain for SSL certificate
- `LETSENCRYPT_EMAIL`: Email for certificate registration

## 🔐 Authentication

Cinny uses the Matrix homeserver's built-in authentication. For advanced authentication features, configure your Matrix homeserver (Synapse) with OIDC or other identity providers.

## 🛠️ Development

### Adding New Environments

1. Create directory in `components/environments/` with `docker-compose.yml` and optional `.env.example` file
2. Run `./build.sh` to generate new combinations

### Adding New Extensions

1. Create directory in `components/extensions/` with `docker-compose.yml` and optional `.env.example` file
2. Run `./build.sh` to generate new combinations with all environments
3. Extensions are automatically combined with all available environments

### File Naming Convention

All component files follow the standard Docker Compose naming convention (`docker-compose.yml`) for:

- **VS Code compatibility**: Full support for Docker Compose language features and IntelliSense
- **IDE integration**: Proper syntax highlighting and validation in all major editors
- **Tool compatibility**: Works with Docker Compose plugins and extensions
- **Standard compliance**: Follows official Docker Compose file naming patterns

### Modifying Existing Components

1. Edit the component files in `components/`
2. Run `./build.sh` to regenerate configurations
3. The `build/` directory will be completely recreated

## 🌐 Networks

- **Development**: `cinny-network` (internal)
- **DevContainer**: `cinny-workspace-network` (external)
- **Let's Encrypt**: `letsencrypt-network` (external)
- **Step CA**: `step-ca-network` (external)

## 🔒 Security

⚠️ **Production Checklist:**

- Configure proper Matrix homeserver URL
- Set up proper firewall rules
- Regular security updates
- Configure rate limiting
- Set up proper logging
- Validate SSL certificates

## 🆘 Troubleshooting

**Build Issues:**

- Ensure `yq` is installed: <https://github.com/mikefarah/yq#install>
- Check component file syntax
- Verify all required files exist

**Cinny Issues:**

- Check config.json syntax
- Verify Matrix homeserver connection
- Review container logs: `docker logs cinny`
- Check network connectivity

**SSL Issues:**

- **Let's Encrypt**: Verify domain DNS and letsencrypt-manager
- **Step CA**: Check step-ca-manager and virtual network config

**Matrix Connection Issues:**

- Verify Matrix homeserver is accessible
- Check CORS configuration on homeserver
- Validate SSL certificates
- Check network connectivity between Cinny and Matrix

## 📝 Notes

- The `build/` directory is automatically generated and should not be edited manually
- Environment variables in generated files use `$VARIABLE_NAME` format for proper interpolation
- Each generated configuration includes a complete `docker-compose.yml` and `.env.example`
- Missing `.env.*` files for components are handled gracefully by the build script
- Cinny requires proper Matrix homeserver configuration for functionality

## 🔄 Configuration Management

The build system automatically:

- Merges base and environment configurations
- Copies additional files and configurations
- Generates complete deployment configurations
- Preserves user `.env` files during rebuilds

**Build approach:**

```bash
./build.sh
cd build/forwarding/base/
cp .env.example .env
# Edit .env with your values
docker-compose up -d
```

## 🎨 Cinny Features

The Cinny configuration includes:

- **Clean UI**: Simple, elegant and intuitive interface
- **Lightweight**: Minimal resource usage and fast loading
- **Secure**: End-to-end encryption support
- **Customizable**: Theme and appearance customization
- **Cross-platform**: Works on desktop and mobile browsers
- **Matrix Native**: Full Matrix protocol support
- **Spaces Support**: Organize rooms with Matrix Spaces
- **Media Support**: Image, video, and file sharing

## ⚙️ Advanced Configuration

For detailed configuration options of the Cinny client, including customization and theming, see the official Cinny documentation:

📖 **[Cinny Configuration Guide](https://github.com/cinnyapp/cinny)**

This guide covers:

- Homeserver configuration options
- Theme and appearance customization
- Featured communities and rooms setup
- Hash router configuration
- Custom homeserver settings

## 🔗 Integration

Cinny works seamlessly with:

- **Matrix Synapse**: Primary Matrix homeserver
- **Dendrite**: Lightweight Matrix homeserver
- **Conduit**: Fast Matrix homeserver written in Rust
- **Custom Homeservers**: Any Matrix-compatible server
- **Matrix Bridges**: Connect to other chat platforms
