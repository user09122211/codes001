# IPTV Project

A comprehensive IPTV (Internet Protocol Television) solution for streaming live TV, video-on-demand, and time-shifted media over IP networks.

## Features

- 📺 **Live TV Streaming**: Broadcast live television channels over IP networks
- 🎬 **Video on Demand (VOD)**: On-demand content library with support for multiple formats
- ⏰ **Time-Shifted Media**: Catch-up TV and cloud DVR functionality
- 🌐 **Multi-Protocol Support**: HLS, DASH, RTSP streaming protocols
- 🔒 **Security**: DRM support, token authentication, and HTTPS encryption
- 📊 **EPG Integration**: Electronic Program Guide with XMLTV support
- 🚀 **Scalable Architecture**: Horizontal scaling with load balancing and CDN integration
- 📱 **Multi-Device**: Compatible with smart TVs, mobile devices, and web players

## Documentation

Complete documentation is available at [ReadTheDocs](https://iptv.readthedocs.io/) or can be built locally:

```bash
# Install documentation dependencies
pip install -r docs/requirements.txt

# Build documentation
cd docs
make html

# Open docs/_build/html/index.html in your browser
```

## Quick Start

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/iptv.git
cd iptv

# Install dependencies
pip install -r requirements.txt

# Configure
cp config.example.yaml config.yaml
# Edit config.yaml with your settings

# Run the server
python main.py --config config.yaml
```

### Usage

Once running, access the service at `http://localhost:8080`:

- **Web Interface**: `http://localhost:8080/web`
- **M3U Playlist**: `http://localhost:8080/playlist.m3u`
- **API**: `http://localhost:8080/api/v1`
- **EPG Guide**: `http://localhost:8080/epg.xml`

## Requirements

- Python 3.8+
- FFmpeg (for transcoding)
- PostgreSQL (database)
- Redis (caching)

## Project Structure

```
iptv/
├── docs/              # Documentation (Sphinx/ReadTheDocs)
├── src/               # Source code
├── tests/             # Test suite
├── config/            # Configuration files
└── scripts/           # Utility scripts
```

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

- 📖 [Documentation](https://iptv.readthedocs.io/)
- 🐛 [Issue Tracker](https://github.com/yourusername/iptv/issues)
- 💬 [Community Forum](https://github.com/yourusername/iptv/discussions)

## Acknowledgments

- Thanks to all contributors
- Built with open-source technologies
- Inspired by modern streaming platforms