# 🚀 Dockploy Pro Dashboard

<div align="center">

![Dockploy Pro Dashboard](https://img.shields.io/badge/Docker-Management-blue?style=for-the-badge&logo=docker)
![Next.js](https://img.shields.io/badge/Next.js-14+-black?style=for-the-badge&logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue?style=for-the-badge&logo=typescript)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

**Modern Docker Container Management Dashboard with Beautiful Glassmorphism UI**

[🎮 Live Demo](#) • [📖 Documentation](./docs/) • [🗺️ Roadmap](./ROADMAP.md) • [🛠️ Setup Guide](./SETUP.md)

</div>

## ✨ Features

### 🎨 **Modern UI/UX**
- **Glassmorphism Design** - Beautiful frosted glass effects with smooth animations
- **Dark Theme** - Easy on the eyes with purple gradient backgrounds
- **Responsive Layout** - Perfect on desktop, tablet, and mobile devices
- **Micro-interactions** - Smooth hover effects and state transitions

### 🐳 **Docker Integration**
- **Real-time Container Discovery** - Automatically detects and displays Docker containers
- **Live Status Monitoring** - Real-time CPU, memory, and network usage
- **Label-based Configuration** - Uses `dockploy.*` labels for smart container management
- **Multi-host Support** - Connect to multiple Docker hosts (planned)

### 🚀 **Core Functionality**
- **Container Lifecycle Management** - Start, stop, restart containers with one click
- **Domain Management** - Clickable links to container web interfaces
- **Resource Monitoring** - Live charts and metrics visualization
- **Log Streaming** - Real-time container log viewing (planned)
- **Health Checking** - Automated container health monitoring

### 🔧 **Developer Experience**
- **TypeScript** - Full type safety and better developer experience
- **Hot Reload** - Instant updates during development
- **Docker API Integration** - Direct connection to Docker daemon
- **Modular Architecture** - Clean, maintainable code structure

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ 
- Docker Desktop or Docker Engine
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/AndersPier/dockploy-pro-dashboard.git
cd dockploy-pro-dashboard

# Install dependencies
npm install

# Copy environment template
cp .env.example .env.local

# Start development server
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000) to see your dashboard!

### Docker Setup

Add Dockploy labels to your containers to make them appear in the dashboard:

```yaml
# docker-compose.yml
version: '3.8'
services:
  web-app:
    image: nginx:alpine
    labels:
      - "dockploy.enable=true"
      - "dockploy.name=Web Application"
      - "dockploy.domains=app.example.com,www.app.example.com"
      - "dockploy.environment=production"
      - "dockploy.team=frontend"
    ports:
      - "80:80"
```

Or via command line:
```bash
docker run -d \
  -l "dockploy.enable=true" \
  -l "dockploy.name=My App" \
  -l "dockploy.domains=app.localhost" \
  -p 8080:80 \
  nginx:alpine
```

## 📊 Dashboard Overview

### Container Cards
Each container displays:
- **Status Indicator** - Visual status with health information
- **Resource Usage** - Real-time CPU and memory metrics
- **Domain Links** - Clickable links to web interfaces
- **Quick Actions** - Start, stop, restart, view logs
- **Uptime & Deployment Info** - Container lifecycle information

### Smart Features
- **Auto-refresh** - Updates every 30 seconds
- **Search & Filter** - Find containers by name, domain, or status
- **Responsive Design** - Works perfectly on all screen sizes
- **Error Recovery** - Graceful handling of Docker connection issues

## 🗺️ Roadmap

### ✅ Completed
- [x] Modern glassmorphism dashboard UI
- [x] Real-time Docker API integration
- [x] Container discovery and monitoring
- [x] Resource usage metrics
- [x] Domain management
- [x] Search and filtering

### 🚧 In Progress
- [ ] Container lifecycle controls (start/stop/restart)
- [ ] WebSocket real-time updates
- [ ] Log streaming viewer

### 📋 Planned Features
- [ ] Multi-server support
- [ ] Advanced monitoring & alerting
- [ ] Security scanning integration
- [ ] Backup management
- [ ] CI/CD pipeline integration
- [ ] Performance optimization recommendations

[View Full Roadmap →](./ROADMAP.md)

## 🏗️ Architecture

```
dockploy-pro-dashboard/
├── app/                    # Next.js 14 App Router
│   ├── api/               # API endpoints
│   ├── dashboard/         # Dashboard pages
│   └── globals.css        # Global styles
├── components/            # React components
│   ├── Dashboard.tsx      # Main dashboard
│   ├── DeploymentCard.tsx # Container cards
│   └── ui/               # Reusable UI components
├── lib/                   # Utilities
│   ├── docker.ts         # Docker API wrapper
│   ├── types.ts          # TypeScript types
│   └── utils.ts          # Helper functions
├── hooks/                 # Custom React hooks
└── docs/                  # Documentation
```

## 🔧 Configuration

### Environment Variables

```env
# Docker Configuration
DOCKER_SOCKET_PATH=/var/run/docker.sock
DOCKER_API_VERSION=1.41

# Security (for production)
JWT_SECRET=your-secret-key
NEXTAUTH_SECRET=your-nextauth-secret

# Database (optional)
DATABASE_URL=postgresql://user:pass@localhost:5432/dockploy

# Monitoring
ENABLE_METRICS=true
METRICS_INTERVAL=5000
```

### Docker Labels Reference

| Label | Description | Example |
|-------|-------------|---------|
| `dockploy.enable` | Enable container in dashboard | `true` |
| `dockploy.name` | Display name | `"Web Application"` |
| `dockploy.domains` | Comma-separated domains | `"app.com,www.app.com"` |
| `dockploy.environment` | Environment name | `"production"` |
| `dockploy.team` | Team/owner | `"frontend"` |
| `dockploy.health_check` | Health check endpoint | `"/health"` |

[View Complete Label Reference →](./docs/LABELS.md)

## 🛠️ Development

### Local Development Setup

```bash
# Install dependencies
npm install

# Start Docker (required for API integration)
docker info

# Run development server with hot reload
npm run dev

# Run type checking
npm run type-check

# Run linting
npm run lint
```

### Building for Production

```bash
# Build the application
npm run build

# Start production server
npm start

# Or build Docker image
docker build -t dockploy-dashboard .
docker run -p 3000:3000 -v /var/run/docker.sock:/var/run/docker.sock:ro dockploy-dashboard
```

## 🐳 Docker Deployment

### Using Docker Compose

```yaml
version: '3.8'
services:
  dockploy-dashboard:
    image: dockploy/dashboard:latest
    ports:
      - "3000:3000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
    environment:
      - NODE_ENV=production
      - DOCKER_SOCKET_PATH=/var/run/docker.sock
    labels:
      - "dockploy.enable=true"
      - "dockploy.name=Dockploy Dashboard"
      - "dockploy.domains=dashboard.example.com"
```

### Security Considerations

- **Read-only Docker socket** - Mount with `:ro` flag
- **Network isolation** - Use Docker networks for security
- **Authentication** - Enable auth for production deployments
- **HTTPS** - Use reverse proxy with SSL termination

## 🤝 Contributing

We welcome contributions! Here's how to get started:

### Quick Contribution Guide

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Development Workflow

```bash
# Setup development environment
git clone https://github.com/AndersPier/dockploy-pro-dashboard.git
cd dockploy-pro-dashboard
npm install

# Create feature branch
git checkout -b feature/new-feature

# Make changes and test
npm run dev
npm run type-check
npm run lint

# Commit and push
git add .
git commit -m "feat: add new feature"
git push origin feature/new-feature
```

### Code Style Guidelines

- Use **TypeScript** for type safety
- Follow **React best practices**
- Implement **proper error handling**
- Add **loading states** for async operations
- Write **responsive CSS** with Tailwind
- Include **proper accessibility** features

## 📄 License

MIT License - see the [LICENSE](LICENSE) file for details.

## 🌟 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=AndersPier/dockploy-pro-dashboard&type=Date)](https://star-history.com/#AndersPier/dockploy-pro-dashboard&Date)

## 📞 Support

- 📧 **Email**: [support@dockploy.com](mailto:support@dockploy.com)
- 💬 **Discord**: [Join our community](https://discord.gg/dockploy)
- 🐛 **Issues**: [GitHub Issues](https://github.com/AndersPier/dockploy-pro-dashboard/issues)
- 📖 **Docs**: [Documentation](./docs/)

## 🙏 Acknowledgments

- [Docker](https://docker.com) for the amazing containerization platform
- [Next.js](https://nextjs.org) for the fantastic React framework
- [Tailwind CSS](https://tailwindcss.com) for the utility-first CSS framework
- [Lucide Icons](https://lucide.dev) for the beautiful icon set

---

<div align="center">

**Built with ❤️ by the Dockploy team**

[⭐ Star us on GitHub](https://github.com/AndersPier/dockploy-pro-dashboard) • [🐳 Deploy with Docker](./docs/DEPLOYMENT.md) • [🚀 Get Started](./SETUP.md)

</div>
