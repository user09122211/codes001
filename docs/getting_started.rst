Getting Started
===============

This guide will help you get started with our IPTV solution quickly and easily.

Prerequisites
-------------

Before you begin, ensure you have the following:

* **Python 3.8+**: Required for running the IPTV server components
* **FFmpeg**: For video encoding and transcoding
* **Stable Internet Connection**: Minimum 10 Mbps recommended for HD streaming
* **Compatible Media Player**: VLC, Kodi, or any HLS/DASH compatible player

Installation
------------

Clone the Repository
~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   git clone https://github.com/yourusername/iptv.git
   cd iptv

Install Dependencies
~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   pip install -r requirements.txt

Configuration
-------------

Basic Configuration
~~~~~~~~~~~~~~~~~~~

Create a configuration file :code:`config.yaml` in the root directory:

.. code-block:: yaml

   server:
     host: 0.0.0.0
     port: 8080
     workers: 4
   
   streaming:
     protocol: hls
     segment_duration: 6
     playlist_size: 5
   
   logging:
     level: INFO
     file: logs/iptv.log

Adding Channels
~~~~~~~~~~~~~~~

Create a channel list file :code:`channels.m3u`:

.. code-block:: m3u

   #EXTM3U
   #EXTINF:-1,Channel Name 1
   http://example.com/stream1.m3u8
   #EXTINF:-1,Channel Name 2
   http://example.com/stream2.m3u8

Usage
-----

Starting the Server
~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   python main.py --config config.yaml

The server will start and be available at :code:`http://localhost:8080`

Accessing Streams
~~~~~~~~~~~~~~~~~

Once the server is running, you can access streams via:

* **Web Interface**: :code:`http://localhost:8080/web`
* **M3U Playlist**: :code:`http://localhost:8080/playlist.m3u`
* **EPG Guide**: :code:`http://localhost:8080/epg.xml`

Using with Popular Players
--------------------------

VLC Media Player
~~~~~~~~~~~~~~~~

1. Open VLC
2. Go to Media → Open Network Stream
3. Enter the stream URL: :code:`http://localhost:8080/stream/channel1.m3u8`
4. Click Play

Kodi
~~~~

1. Install the "PVR IPTV Simple Client" addon
2. Configure with your M3U playlist URL
3. Enable the addon and access from TV section

Mobile Devices
~~~~~~~~~~~~~~

For iOS and Android, use compatible IPTV player apps such as:

* **iOS**: GSE Smart IPTV, IPTV Smarters
* **Android**: TiviMate, IPTV Smarters, VLC

Advanced Configuration
----------------------

Transcoding Settings
~~~~~~~~~~~~~~~~~~~~

Enable hardware-accelerated transcoding in :code:`config.yaml`:

.. code-block:: yaml

   transcoding:
     enabled: true
     codec: h264
     preset: fast
     crf: 23
     hardware: nvenc  # or vaapi, qsv

CDN Integration
~~~~~~~~~~~~~~~

For large-scale deployments, configure CDN settings:

.. code-block:: yaml

   cdn:
     enabled: true
     provider: cloudflare
     cache_ttl: 3600

Troubleshooting
---------------

Common Issues
~~~~~~~~~~~~~

**Stream Not Playing**

* Verify the source URL is accessible
* Check firewall settings
* Ensure FFmpeg is properly installed

**Buffering Issues**

* Increase buffer size in player settings
* Check network bandwidth
* Reduce stream quality or bitrate

**EPG Not Loading**

* Verify EPG source URL
* Check XML format validity
* Ensure proper timezone configuration

Next Steps
----------

* Learn about the :doc:`architecture` of the system
* Explore the :doc:`api_reference` for programmatic access
* Check :doc:`troubleshooting` for common issues
* Read our :doc:`faq` for frequently asked questions
