Frequently Asked Questions (FAQ)
=================================

General Questions
-----------------

What is IPTV?
~~~~~~~~~~~~~

IPTV (Internet Protocol Television) is a system that delivers television content using Internet Protocol networks instead of traditional broadcast, satellite, or cable formats. This allows for more flexible viewing options including live TV, video-on-demand, and time-shifted media.

Is IPTV legal?
~~~~~~~~~~~~~~

Yes, IPTV technology itself is completely legal. However, it's important to use licensed content providers and respect copyright laws. Always ensure you have the right to access the content you're streaming.

What do I need to use IPTV?
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* A stable internet connection (minimum 10 Mbps for HD)
* A compatible device (smart TV, computer, smartphone, tablet, or set-top box)
* An IPTV player application (VLC, Kodi, etc.)
* A subscription to a legitimate IPTV service or your own content sources

Technical Questions
-------------------

What video formats are supported?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Our IPTV system supports multiple video codecs:

* **H.264/AVC**: Most widely supported format
* **H.265/HEVC**: Better compression, requires newer hardware
* **VP9**: Open-source alternative
* **AV1**: Next-generation codec (experimental)

Audio formats include AAC, MP3, Opus, and AC3.

What is the difference between HLS and DASH?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Both are adaptive bitrate streaming protocols:

* **HLS (HTTP Live Streaming)**: Developed by Apple, uses .m3u8 playlists, widely supported
* **DASH (Dynamic Adaptive Streaming over HTTP)**: MPEG standard, more flexible, growing adoption

Our system supports both formats for maximum compatibility.

How much bandwidth do I need?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Recommended bandwidth per stream:

* **SD (480p)**: 2-3 Mbps
* **HD (720p)**: 5-8 Mbps
* **Full HD (1080p)**: 10-15 Mbps
* **4K UHD**: 25-50 Mbps

For multiple simultaneous streams, add the requirements together.

Can I record live TV?
~~~~~~~~~~~~~~~~~~~~~

Yes, the system supports DVR functionality:

* **Cloud DVR**: Recordings stored on server
* **Local DVR**: Recordings saved to local storage
* **Series Recording**: Automatically record all episodes

Configure recording schedules through the web interface or API.

Why is my stream buffering?
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Common causes of buffering:

1. **Insufficient bandwidth**: Check your internet speed
2. **Server overload**: Too many concurrent users
3. **Network congestion**: Peak usage times
4. **Client device**: Limited processing power

Solutions:

* Reduce stream quality
* Use wired connection instead of WiFi
* Close other bandwidth-intensive applications
* Increase buffer size in player settings

Configuration Questions
-----------------------

How do I add new channels?
~~~~~~~~~~~~~~~~~~~~~~~~~~

Channels can be added via:

1. **M3U Playlist**: Import existing M3U file
2. **Web Interface**: Add channels manually through admin panel
3. **API**: Programmatically add channels via REST API
4. **EPG Import**: Auto-discover channels from EPG source

See :doc:`getting_started` for detailed instructions.

Can I customize the channel order?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Yes, you can:

* Manually reorder channels in the web interface
* Set favorite channels for quick access
* Create custom channel groups/categories
* Hide unwanted channels

How do I set up EPG (Electronic Program Guide)?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

EPG setup steps:

1. Obtain EPG source URL (XMLTV format recommended)
2. Configure EPG grabber in settings
3. Set update schedule (recommended: every 6 hours)
4. Map channels to EPG IDs if needed

Multiple EPG sources can be configured for different regions/languages.

Device Compatibility
--------------------

What devices support IPTV?
~~~~~~~~~~~~~~~~~~~~~~~~~~

IPTV works on most modern devices:

* **Smart TVs**: Samsung, LG, Sony, Android TV
* **Streaming Devices**: Roku, Amazon Fire TV, Apple TV, Chromecast
* **Computers**: Windows, macOS, Linux
* **Mobile**: iOS, Android tablets and phones
* **Game Consoles**: PlayStation, Xbox (via browser or apps)

Best IPTV players for each platform:

* **Universal**: VLC Media Player
* **Android**: TiviMate, IPTV Smarters
* **iOS**: GSE Smart IPTV, PlayerXtreme
* **Smart TV**: Built-in players or dedicated apps

Can I use IPTV on multiple devices simultaneously?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Yes, but depends on your subscription plan:

* **Basic**: 1-2 simultaneous streams
* **Standard**: 3-5 simultaneous streams
* **Premium**: Unlimited streams (within reason)

Check your service provider's terms.

Security & Privacy
------------------

Is my data secure?
~~~~~~~~~~~~~~~~~~

Our system implements multiple security measures:

* **HTTPS Encryption**: All communications encrypted
* **Token Authentication**: Secure API access
* **DRM Support**: Content protection
* **No Logging Option**: Privacy-focused configuration

Should I use a VPN with IPTV?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Using a VPN is recommended for:

* **Privacy**: Hides your viewing habits from ISP
* **Security**: Encrypts all traffic
* **Geo-restrictions**: Access content from different regions
* **Throttling Prevention**: Prevents ISP bandwidth throttling

Choose a reputable VPN with good speeds and no logging policy.

How do I enable parental controls?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Parental control features:

1. **Content Rating Filters**: Block channels by rating
2. **PIN Protection**: Require PIN for restricted content
3. **Viewing Time Limits**: Set allowed viewing hours
4. **Channel Locking**: Hide specific channels

Configure in Settings → Parental Controls.

Performance & Scaling
---------------------

How many concurrent users can the system handle?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Capacity depends on hardware and configuration:

* **Single Server** (consumer hardware): 50-100 concurrent streams
* **Single Server** (enterprise hardware): 200-500 concurrent streams
* **Clustered Deployment**: Thousands of concurrent streams

Scaling options:

* Horizontal scaling with load balancers
* CDN integration for geographic distribution
* Transcoding optimization

What hardware do I need for self-hosting?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Minimum requirements:

* **CPU**: Quad-core processor
* **RAM**: 8 GB
* **Storage**: 100 GB SSD
* **Network**: 1 Gbps connection

Recommended for production:

* **CPU**: 8+ cores with hardware encoding support
* **RAM**: 16-32 GB
* **Storage**: 500 GB+ NVMe SSD
* **Network**: 10 Gbps connection

Troubleshooting
---------------

Where can I find logs?
~~~~~~~~~~~~~~~~~~~~~~

Log locations:

* **Application Logs**: ``/var/log/iptv/`` or ``logs/`` directory
* **Access Logs**: ``logs/access.log``
* **Error Logs**: ``logs/error.log``
* **Transcoding Logs**: ``logs/transcoder.log``

Enable debug mode for more detailed logging:

.. code-block:: yaml

   logging:
     level: DEBUG

How do I report a bug?
~~~~~~~~~~~~~~~~~~~~~~

When reporting issues, include:

1. System information (OS, versions)
2. Configuration (with sensitive data removed)
3. Error messages and logs
4. Steps to reproduce
5. Expected vs actual behavior

Submit via GitHub Issues or community forum.

Billing & Subscription
----------------------

What payment methods are accepted?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We accept:

* Credit/Debit Cards (Visa, MasterCard, Amex)
* PayPal
* Cryptocurrency (Bitcoin, Ethereum)
* Bank Transfer (for annual plans)

All payments are processed securely.

Can I cancel my subscription anytime?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Yes, you can cancel at any time:

* **Monthly Plans**: Cancel before next billing cycle
* **Annual Plans**: Prorated refund available within 30 days
* **Free Trial**: No credit card required, auto-cancels after trial

Access continues until the end of the current billing period.

Do you offer refunds?
~~~~~~~~~~~~~~~~~~~~~

Refund policy:

* **30-day money-back guarantee** for new subscriptions
* **Pro-rated refunds** for annual plans (within first 30 days)
* **No refunds** for partial months on monthly plans

Contact support for refund requests.

More Information
----------------

For more detailed information:

* :doc:`introduction` - Learn about IPTV basics
* :doc:`getting_started` - Setup and configuration guide
* :doc:`architecture` - System architecture details
* :doc:`api_reference` - API documentation
* :doc:`troubleshooting` - Common issues and solutions

Still have questions? Contact our support team or visit the community forum.
