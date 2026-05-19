System Architecture
===================

This document describes the architecture of our IPTV system, including its components, data flow, and design principles.

Overview
--------

The IPTV system is built on a modular architecture that separates concerns between different components, making it scalable, maintainable, and extensible.

.. code-block:: text

   ┌─────────────────────────────────────────────────────────┐
   │                    Content Sources                       │
   │  ┌──────────┐  ┌──────────┐  ┌──────────────────────┐  │
   │  │ Live TV  │  │   VOD    │  │  External Streams    │  │
   │  └──────────┘  └──────────┘  └──────────────────────┘  │
   └─────────────────────────────────────────────────────────┘
                            │
                            ▼
   ┌─────────────────────────────────────────────────────────┐
   │                   Ingestion Layer                        │
   │  ┌──────────────────────────────────────────────────┐   │
   │  │  Stream Capturer / Download Manager              │   │
   │  └──────────────────────────────────────────────────┘   │
   └─────────────────────────────────────────────────────────┘
                            │
                            ▼
   ┌─────────────────────────────────────────────────────────┐
   │                  Processing Layer                        │
   │  ┌──────────┐  ┌──────────┐  ┌──────────────────────┐  │
   │  │ Transcoder│  │ Encryptor│  │  Metadata Extractor  │  │
   │  └──────────┘  └──────────┘  └──────────────────────┘  │
   └─────────────────────────────────────────────────────────┘
                            │
                            ▼
   ┌─────────────────────────────────────────────────────────┐
   │                   Delivery Layer                         │
   │  ┌──────────┐  ┌──────────┐  ┌──────────────────────┐  │
   │  │ HLS Pack │  │ DASH Pack│  │  CDN Integration     │  │
   │  └──────────┘  └──────────┘  └──────────────────────┘  │
   └─────────────────────────────────────────────────────────┘
                            │
                            ▼
   ┌─────────────────────────────────────────────────────────┐
   │                   Client Applications                    │
   │  ┌──────────┐  ┌──────────┐  ┌──────────────────────┐  │
   │  │Web Player│  │Mobile App│  │  Smart TV Apps       │  │
   │  └──────────┘  └──────────┘  └──────────────────────┘  │
   └─────────────────────────────────────────────────────────┘

Core Components
---------------

Stream Ingestion Module
~~~~~~~~~~~~~~~~~~~~~~~

Responsible for acquiring content from various sources:

* **Live Stream Capturer**: Captures live TV streams via satellite, cable, or IP
* **VOD Importer**: Imports video-on-demand content from local storage or external sources
* **Schedule Manager**: Manages recording schedules for time-shifted content

Key Features:
- Support for multiple input protocols (HTTP, RTSP, UDP, SRT)
- Automatic reconnection on stream failure
- Quality monitoring and adaptive source switching

Transcoding Engine
~~~~~~~~~~~~~~~~~~

Converts incoming streams into multiple formats and bitrates:

* **Format Conversion**: H.264, H.265/HEVC, VP9, AV1
* **Adaptive Bitrate**: Multiple quality levels (480p, 720p, 1080p, 4K)
* **Audio Transcoding**: AAC, MP3, Opus, AC3

Configuration Example:

.. code-block:: yaml

   transcoding:
     profiles:
       - name: low
         resolution: 640x360
         bitrate: 800k
         codec: h264
       - name: medium
         resolution: 1280x720
         bitrate: 2500k
         codec: h264
       - name: high
         resolution: 1920x1080
         bitrate: 5000k
         codec: h265

Streaming Server
~~~~~~~~~~~~~~~~

Delivers content to end-users using various protocols:

* **HLS (HTTP Live Streaming)**: Apple's adaptive streaming protocol
* **DASH (Dynamic Adaptive Streaming over HTTP)**: MPEG-DASH standard
* **RTMP**: For low-latency streaming (deprecated but still supported)

Features:
- Segment-based delivery for efficient caching
- Dynamic playlist generation
- DRM support (Widevine, FairPlay, PlayReady)

EPG (Electronic Program Guide) Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Provides program information and scheduling data:

* **EPG Grabber**: Collects EPG data from various sources
* **XMLTV Parser**: Parses XMLTV format EPG data
* **Schedule API**: RESTful API for program schedule access

Data Flow
---------

Live Streaming Flow
~~~~~~~~~~~~~~~~~~~

1. **Source Acquisition**: Live stream is captured from broadcaster
2. **Pre-processing**: Stream is demultiplexed and analyzed
3. **Transcoding**: Multiple bitrate versions are created
4. **Packaging**: Segments are created for HLS/DASH
5. **Distribution**: Segments are served via HTTP/CDN
6. **Playback**: Client requests and plays segments adaptively

VOD Streaming Flow
~~~~~~~~~~~~~~~~~~

1. **Content Import**: Video file is ingested into the system
2. **Transcoding**: Multiple renditions are generated
3. **Storage**: Processed files are stored in object storage
4. **Metadata**: Program information is indexed
5. **Delivery**: Content is streamed on-demand
6. **Analytics**: Viewing statistics are collected

Scalability Considerations
--------------------------

Horizontal Scaling
~~~~~~~~~~~~~~~~~~

The system supports horizontal scaling through:

* **Load Balancing**: Distribute requests across multiple server instances
* **Stateless Design**: Any server can handle any request
* **Session Persistence**: Optional sticky sessions for live streams

Caching Strategy
~~~~~~~~~~~~~~~~

Multi-level caching improves performance:

* **Edge Caching**: CDN caches segments at edge locations
* **Server Cache**: Frequently accessed content cached in memory
* **Client Cache**: Players cache upcoming segments

Database Architecture
~~~~~~~~~~~~~~~~~~~~~

* **PostgreSQL**: Primary database for metadata, users, and configurations
* **Redis**: Caching layer for session data and frequently accessed info
* **Elasticsearch**: Search engine for content discovery

Security Architecture
---------------------

Authentication & Authorization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **JWT Tokens**: Secure API authentication
* **OAuth 2.0**: Third-party integration support
* **Role-Based Access Control**: Granular permission management

Content Protection
~~~~~~~~~~~~~~~~~~

* **DRM Integration**: Industry-standard digital rights management
* **Token Authentication**: Secure stream URLs with time-limited tokens
* **Geo-blocking**: Restrict content based on geographic location
* **HTTPS Enforcement**: Encrypted transport for all communications

Monitoring & Logging
--------------------

Health Monitoring
~~~~~~~~~~~~~~~~~

* **Prometheus Metrics**: System performance metrics
* **Grafana Dashboards**: Real-time visualization
* **Alerting**: Automated alerts for critical issues

Logging
~~~~~~~

* **Structured Logging**: JSON-formatted logs for easy parsing
* **Log Aggregation**: Centralized logging with ELK stack
* **Audit Trails**: Track user actions and system changes

API Reference
-------------

For detailed API documentation, see :doc:`api_reference`.

Next Steps
----------

* Explore the :doc:`api_reference` for programmatic access
* Check :doc:`troubleshooting` for common issues
* Read :doc:`faq` for frequently asked questions
