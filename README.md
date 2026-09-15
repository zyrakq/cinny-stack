# 🌐 Cinny Stack

Complete Docker-based Cinny deployment with SSL certificate management for production and development environments.

## 🧩 Components

### 🔐 SSL Automation

#### [🔒 Let's Encrypt Manager](modules/ssl-automation/letsencrypt-manager)

Automatic SSL certificate management from Let's Encrypt for production deployments. Provides seamless HTTPS integration for Docker containers using nginx-proxy and acme-companion.
[Learn more about Let's Encrypt Manager configuration](modules/ssl-automation/letsencrypt-manager/README.md).

#### [🏠 Step CA Manager](modules/ssl-automation/step-ca-manager)

Local domain stack with trusted self-signed certificates for virtual network deployments. Includes private CA management and local DNS resolution for development environments.
[Learn more about Step CA Manager configuration](modules/ssl-automation/step-ca-manager/README.md).

## 🌐 Services

### 🌐 [Cinny](app/)

Modular Docker Compose configuration system for Cinny client with support for multiple environments and simplified configuration. Provides complete Matrix web client deployment with lightweight, user-friendly interface for development and production.
[Learn more about Cinny configuration](app/README.md).

## 🚀 Quick Start

Each component has its own README with detailed setup instructions. Choose the certificate management solution that fits your deployment scenario.

### Basic Setup

1. **Choose SSL Management:**
   - Production: Use Let's Encrypt Manager
   - Development: Use Step CA Manager

2. **Deploy Matrix Backend:**
   - Set up Synapse homeserver (full-featured, PostgreSQL-based)
   - Or set up Conduit homeserver (lightweight, Rust-based)

3. **Deploy Cinny:**
   - Configure Cinny client to connect to your Matrix homeserver

## 🏗️ Architecture

```sh
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│      Cinny      │────│ Matrix Homeserver│────│    Database     │
│   (Frontend)    │    │ (Synapse/Conduit)│    │(PostgreSQL/     │
└─────────────────┘    └─────────────────┘    │ RocksDB)        │
                                │              └─────────────────┘
                                │
                       ┌─────────────────┐
                       │  SSL Manager    │
                       │ (Let's Encrypt/ │
                       │  Step CA)       │
                       └─────────────────┘
```

## 📋 Requirements

- Docker & Docker Compose
- Domain name (for production deployments)
- Email address (for Let's Encrypt)
- `yq` tool for configuration building

## 🔧 Configuration

All services use modular Docker Compose configurations with:

- **Base components**: Core service definitions
- **Environment components**: Development, production, SSL configurations
- **Build system**: Automatic generation of deployment combinations

## 🌍 Deployment Scenarios

### Development Environment

```bash
# Cinny with port forwarding
cd app/build/forwarding/base/
docker-compose up -d
```

### Production Environment

```bash
# Cinny with Let's Encrypt SSL
cd app/build/letsencrypt/base/
docker-compose up -d
```

## 🔐 Security Features

- **SSL/TLS Encryption**: Automatic certificate management
- **Matrix Authentication**: Built-in Matrix homeserver authentication
- **Network Isolation**: Docker network segmentation
- **Secret Management**: Environment-based configuration

## 🆘 Troubleshooting

### Common Issues

- **SSL Certificate Issues**: Check Let's Encrypt/Step CA configuration
- **Network Connectivity**: Ensure proper Docker network configuration
- **Database Connection**: Check PostgreSQL connectivity for Synapse

### Logs

```bash
# Cinny logs
docker logs cinny

# Synapse logs
docker logs matrix

# Conduit logs
docker logs conduit

# SSL automation logs
docker logs letsencrypt-manager  # or step-ca-manager
```

## 📚 Documentation

- [Cinny Configuration](app/README.md)
- [SSL Automation](modules/ssl-automation/)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test configurations
5. Submit a pull request

## 📄 License

This project is dual-licensed under:

- [Apache License 2.0](LICENSE-APACHE)
- [MIT License](LICENSE-MIT)

## 🔗 Related Projects

- [Matrix.org](https://matrix.org/) - Open network for secure, decentralized communication
- [Cinny](https://cinny.in/) - Simple, elegant and secure Matrix client
- [Synapse](https://github.com/matrix-org/synapse) - Matrix homeserver implementation
- [Conduit](https://conduit.rs/) - Lightweight Matrix homeserver written in Rust
