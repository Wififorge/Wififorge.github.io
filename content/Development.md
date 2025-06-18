---
title: Development Guide
---
**Contributing to WifiForge - Developer Documentation and Guidelines**

This guide covers how to contribute to WifiForge, understand its architecture, and participate in the project's development.

---

## Project Overview

### What is WifiForge?
WifiForge is an open-source Wi-Fi security education framework developed by **Black Hills InfoSec**. The project provides a safe, legal environment for learning wireless security techniques through virtual network simulation based on mininet-wifi.

### Development Philosophy
- **Safety First**: All development should maintain virtual environment isolation and prevent real-world network interaction
- **Educational Focus**: Features should enhance learning outcomes  
- **Community Driven**: Open collaboration with transparent development processes
- **Ethical Standards**: Commitment to responsible security education

---

## Development Environment Setup

### Prerequisites
```bash
# System requirements
- Ubuntu 20.04 LTS or newer (recommended)
- Python 3.7+ with development headers
- Git for version control
- Virtual machine environment (recommended for safety)

# Install development tools
sudo apt update
sudo apt install -y python3-dev python3-pip python3-venv
sudo apt install -y git build-essential
```

### Getting Started
```bash
# 1. Fork and clone the repository
git clone https://github.com/YOUR_USERNAME/WifiForge.git
cd WifiForge

# 2. Create development environment
python3 -m venv dev-env
source dev-env/bin/activate

# 3. Install dependencies
# Follow the installation guide for your development environment
# Docker method recommended for consistency
```

---

## Technology Stack

### Core Technologies
- **Python 3.7+**: Primary development language
- **Mininet-WiFi**: Virtual wireless network simulation engine
- **Shell Scripts**: Supporting automation and utilities

### Integrated Security Tools
WifiForge integrates with established wireless security tools:
- **Aircrack-ng Suite**: Wireless security tool integration
- **Bettercap**: Modern network attack and monitoring framework
- **Airgeddon**: Multi-use wireless security auditing tool
- **Wifiphisher**: Automated phishing attacks against Wi-Fi networks
- **John the Ripper & Hashcat**: Password cracking tools

---

## Contributing Guidelines

### Ways to Contribute
1. **Report Issues**: Found a bug? Report it on [GitHub Issues](https://github.com/blackhillsinfosec/WifiForge/issues)
2. **Improve Documentation**: Help make guides clearer and more comprehensive
3. **Test Features**: Test new features and provide feedback
4. **Contribute Code**: Submit improvements to the framework
5. **Share Knowledge**: Help other learners in discussions

### Development Workflow

**1. Before You Start**
- Check existing [GitHub Issues](https://github.com/blackhillsinfosec/WifiForge/issues) before creating new ones
- Discuss proposed changes in GitHub Issues
- Get feedback from maintainers before major changes
- Review the [Overview](Overview.md) to understand the framework's goals

**2. Development Process**
```bash
# Create feature branch
git checkout -b feature/your-feature-name

# Make your changes
# Test in isolated virtual environment

# Commit changes with clear messages
git add .
git commit -m "Add feature: clear description of what was added"

# Push to your fork
git push origin feature/your-feature-name

# Create pull request on GitHub
```

**3. Pull Request Guidelines**
- **Clear Description**: Explain what changes you made and why
- **Test Instructions**: Provide steps to test your changes
- **Documentation Updates**: Update documentation if needed
- **Focused Changes**: Keep PRs focused on single features/fixes

---

## Code Quality Standards

### Development Standards
- **Python Standards**: Follow PEP 8 style guidelines
- **Documentation**: Include clear docstrings and comments
- **Error Handling**: Implement proper error handling
- **Safety**: Ensure virtual environment isolation is maintained

### Safety Requirements
> **Development Safety Note**: Virtual environment development is recommended for safety. WifiForge is in active development and testing should occur in isolated environments to prevent any issues from affecting host systems.

**Code Safety Guidelines**
- Never implement features that interact with real wireless networks
- Maintain virtual environment isolation in all code
- Include safety checks and warnings in user-facing features
- Follow responsible disclosure practices for any security issues

---

## Current Development Focus

### v3.x.x (Current)
- **WPS Lab**: WPS Pixie Dust Attack lab currently does not work
- **Stability Improvements**: Framework refinements and bug fixes
- **Documentation Expansion**: Comprehensive guides and educational materials

### v4.0.0 (Planned)
- **WifiProbe**: Wireless landscape snapshot tool
- **WifiHound**: BloodHound integration for Access Point analytics
- **Drone Hacking**: Wireless drone hacking lab integration

---

## Project Communication

### GitHub Repository
**Main Repository**: https://github.com/blackhillsinfosec/WifiForge

- **Issues**: Bug reports and feature requests
- **Discussions**: Community questions and knowledge sharing
- **Pull Requests**: Code contributions and improvements

### Community Standards
- Follow the Code of Conduct for all interactions
- Respect the educational focus of the project
- Maintain ethical and legal standards in all contributions
- Support the project's mission of accessible wireless security education

---

## Resources for Contributors

### Learning Resources
- **Mininet-WiFi Documentation**: Understanding the underlying framework
- **Python Development**: Best practices for Python coding
- **Wireless Security**: Background knowledge for educational content

### Development Tools
- **Git**: Version control and collaboration
- **Python Virtual Environments**: Isolated development environments
- **Docker**: Consistent development and testing environments
- **VM Software**: For safe testing and development

---

**Join the Community**

WifiForge welcomes contributors of all skill levels. Whether you're fixing bugs, improving documentation, or adding new features, your contributions help make wireless security education more accessible.

**Remember**: All development activities should maintain the project's commitment to safe, legal, and ethical wireless security education.