# IPTV Documentation

Comprehensive documentation for the IPTV project, designed for hosting on ReadTheDocs.io.

## Quick Start

### Local Development

1. Install dependencies:
   ```bash
   pip install -r docs/requirements.txt
   ```

2. Build the documentation:
   ```bash
   cd docs
   make html
   ```

3. View the documentation:
   ```bash
   # Open docs/_build/html/index.html in your browser
   ```

### Live Reload (Optional)

For automatic rebuilding during development:
```bash
pip install sphinx-autobuild
sphinx-autobuild docs docs/_build/html
```

## Documentation Structure

```
docs/
├── conf.py              # Sphinx configuration
├── index.rst            # Main documentation page
├── introduction.rst     # What is IPTV
├── getting_started.rst  # Installation and setup guide
├── architecture.rst     # System architecture details
├── api_reference.rst    # REST API documentation
├── troubleshooting.rst  # Common issues and solutions
├── faq.rst              # Frequently asked questions
├── requirements.txt     # Python dependencies
└── robots.txt           # Search engine crawler rules
```

## ReadTheDocs Configuration

This documentation is configured for automatic building on ReadTheDocs.io.

### Setup Instructions

1. Connect your GitHub repository to ReadTheDocs
2. Configure the build settings:
   - Python version: 3.8+
   - Requirements file: `docs/requirements.txt`
   - Documentation directory: `docs/`

3. Enable automatic builds on push

### Custom Domain (Optional)

To use a custom domain:
1. Go to ReadTheDocs project settings
2. Navigate to "Domains"
3. Add your custom domain
4. Configure DNS records as instructed

## Contributing

When adding new documentation:

1. Create a new `.rst` file in the `docs/` directory
2. Add it to the `toctree` in `index.rst`
3. Use proper reStructuredText formatting
4. Build locally to verify changes
5. Submit a pull request

### Style Guide

- Use clear, concise language
- Include code examples where applicable
- Add cross-references between related documents
- Keep sections well-organized with proper hierarchy
- Use consistent formatting for similar content types

## Building for Production

```bash
cd docs
make clean
make html
```

The built documentation will be in `docs/_build/html/`.

## License

Documentation is licensed under the same license as the main project.

## Support

For issues or questions about the documentation:
- Open an issue on GitHub
- Check the FAQ section
- Contact the maintainers
