Troubleshooting
===============

This guide helps you diagnose and resolve common issues with the IPTV system.

Stream Playback Issues
----------------------

Stream Not Loading
~~~~~~~~~~~~~~~~~~

**Symptoms**: Player shows loading indefinitely or displays error message.

**Possible Causes**:

1. Invalid stream URL
2. Server is not running
3. Firewall blocking connection
4. Codec incompatibility

**Solutions**:

* Verify the stream URL is correct and accessible:

  .. code-block:: bash

     curl -I http://localhost:8080/stream/channel1.m3u8

* Check if the server is running:

  .. code-block:: bash

     systemctl status iptv-server
     # or
     ps aux | grep iptv

* Test connectivity:

  .. code-block:: bash

     ping localhost
     telnet localhost 8080

* Try a different player (VLC, MPV, etc.)

Buffering Problems
~~~~~~~~~~~~~~~~~~

**Symptoms**: Video plays but frequently pauses to buffer.

**Possible Causes**:

1. Insufficient bandwidth
2. High server load
3. Network congestion
4. Client device performance

**Solutions**:

* Check your internet speed:

  .. code-block:: bash

     speedtest-cli

* Reduce stream quality in player settings
* Increase buffer size:

  * **VLC**: Tools → Preferences → Input/Codecs → Network caching (increase to 3000ms)
  * **Kodi**: Settings → Player → Videos → Adjust cache settings

* Close other bandwidth-intensive applications
* Use wired connection instead of WiFi when possible

No Audio or Video
~~~~~~~~~~~~~~~~~

**Symptoms**: Stream plays but missing audio or video.

**Solutions**:

* Check codec support in your player
* Update FFmpeg to latest version:

  .. code-block:: bash

     sudo apt update && sudo apt install ffmpeg

* Try different output format in configuration:

  .. code-block:: yaml

     streaming:
       video_codec: h264
       audio_codec: aac

Server Issues
-------------

Server Won't Start
~~~~~~~~~~~~~~~~~~

**Symptoms**: Server fails to start or crashes immediately.

**Solutions**:

* Check logs for error messages:

  .. code-block:: bash

     tail -f logs/iptv.log

* Verify configuration file syntax:

  .. code-block:: bash

     python -c "import yaml; yaml.safe_load(open('config.yaml'))"

* Check if port is already in use:

  .. code-block:: bash

     netstat -tlnp | grep 8080
     # or
     lsof -i :8080

* Ensure all dependencies are installed:

  .. code-block:: bash

     pip install -r requirements.txt

High CPU Usage
~~~~~~~~~~~~~~

**Symptoms**: Server consuming excessive CPU resources.

**Solutions**:

* Reduce number of concurrent transcoding jobs:

  .. code-block:: yaml

     transcoding:
       max_workers: 2

* Enable hardware acceleration:

  .. code-block:: yaml

     transcoding:
       hardware: nvenc  # NVIDIA
       # or
       hardware: vaapi  # Intel VAAPI
       # or
       hardware: qsv    # Intel QuickSync

* Lower output quality or reduce number of bitrate profiles
* Monitor with htop or top to identify bottlenecks

Memory Leaks
~~~~~~~~~~~~

**Symptoms**: Memory usage continuously increases over time.

**Solutions**:

* Restart server periodically via cron:

  .. code-block:: bash

     0 4 * * * systemctl restart iptv-server

* Check for known issues in project repository
* Enable memory profiling:

  .. code-block:: yaml

     monitoring:
       memory_profiling: true

EPG Issues
----------

EPG Not Updating
~~~~~~~~~~~~~~~~

**Symptoms**: Program guide shows outdated or no information.

**Solutions**:

* Manually trigger EPG update:

  .. code-block:: bash

     python scripts/update_epg.py

* Verify EPG source URL is accessible:

  .. code-block:: bash

     curl -I https://epg-source.example.com/guide.xml

* Check EPG parser logs:

  .. code-block:: bash

     tail -f logs/epg.log

* Validate XML format:

  .. code-block:: bash

     xmllint --noout epg.xml

Incorrect Timezone
~~~~~~~~~~~~~~~~~~

**Symptoms**: Program times are offset by several hours.

**Solutions**:

* Set correct timezone in configuration:

  .. code-block:: yaml

     epg:
       timezone: America/New_York

* Ensure system timezone is correct:

  .. code-block:: bash

     timedatectl
     sudo timedatectl set-timezone America/New_York

Authentication Issues
---------------------

Login Fails
~~~~~~~~~~~

**Symptoms**: Cannot authenticate with valid credentials.

**Solutions**:

* Verify database connection
* Check user exists in database:

  .. code-block:: sql

     SELECT * FROM users WHERE email = 'user@example.com';

* Reset password:

  .. code-block:: bash

     python scripts/reset_password.py user@example.com

* Clear session cache:

  .. code-block:: bash

     redis-cli FLUSHDB

Token Expired Too Quickly
~~~~~~~~~~~~~~~~~~~~~~~~~~

**Solutions**:

* Adjust token expiration in configuration:

  .. code-block:: yaml

     auth:
       token_expiry: 86400  # 24 hours in seconds

* Implement token refresh mechanism in client application

Database Issues
---------------

Connection Errors
~~~~~~~~~~~~~~~~~

**Symptoms**: Database connection failures.

**Solutions**:

* Verify database service is running:

  .. code-block:: bash

     systemctl status postgresql

* Check connection string in configuration:

  .. code-block:: yaml

     database:
       host: localhost
       port: 5432
       name: iptv_db
       user: iptv_user
       password: secure_password

* Test connection manually:

  .. code-block:: bash

     psql -h localhost -U iptv_user -d iptv_db

Slow Queries
~~~~~~~~~~~~

**Solutions**:

* Add database indexes:

  .. code-block:: sql

     CREATE INDEX idx_channels_category ON channels(category);
     CREATE INDEX idx_epg_start_time ON epg_programs(start_time);

* Enable query logging to identify slow queries:

  .. code-block:: yaml

     database:
       log_queries: true
       slow_query_threshold: 1.0

* Run vacuum and analyze:

  .. code-block:: sql

     VACUUM ANALYZE;

Performance Optimization
------------------------

General Tips
~~~~~~~~~~~~

* Use SSD storage for better I/O performance
* Enable caching at multiple levels (Redis, CDN, browser)
* Implement connection pooling for database
* Use async operations where possible
* Monitor performance metrics regularly

Load Balancing
~~~~~~~~~~~~~~

For high-traffic deployments:

* Use Nginx or HAProxy as reverse proxy
* Deploy multiple server instances
* Implement sticky sessions for live streams
* Use CDN for static content delivery

Getting Help
------------

If you're still experiencing issues:

1. **Check Logs**: Most issues leave traces in log files
2. **Search Issues**: Look for similar problems in the issue tracker
3. **Community Forum**: Ask for help in community forums
4. **GitHub Issues**: Open a new issue with detailed information

When Reporting Issues
~~~~~~~~~~~~~~~~~~~~~

Include the following information:

* System information (OS, Python version, etc.)
* Configuration file (with sensitive data removed)
* Relevant log excerpts
* Steps to reproduce the problem
* Expected vs actual behavior

.. code-block:: bash

   # Collect system info
   python scripts/collect_debug_info.sh

Next Steps
----------

* Read :doc:`faq` for frequently asked questions
* Return to :doc:`index` for main documentation
* Check :doc:`api_reference` for API details
