API Reference
=============

This document provides comprehensive documentation for the IPTV REST API.

Base URL
--------

All API requests should be made to:

.. code-block:: text

   http://localhost:8080/api/v1

Authentication
--------------

Most API endpoints require authentication using JWT tokens. Include the token in the Authorization header:

.. code-block:: bash

   curl -H "Authorization: Bearer YOUR_JWT_TOKEN" \
        https://api.iptv.example.com/api/v1/channels

Obtaining a Token
~~~~~~~~~~~~~~~~~

.. http:post:: /auth/login

   Authenticate user and receive access token.

   **Request Body**:

   .. code-block:: json

      {
        "username": "user@example.com",
        "password": "securepassword"
      }

   **Response**:

   .. code-block:: json

      {
        "access_token": "eyJhbGciOiJIUzI1NiIs...",
        "refresh_token": "eyJhbGciOiJIUzI1NiIs...",
        "expires_in": 3600,
        "token_type": "Bearer"
      }

Channels API
------------

.. http:get:: /channels

   Retrieve a list of all available channels.

   **Query Parameters**:

   :param category: Filter by category (optional)
   :param language: Filter by language (optional)
   :param limit: Maximum number of results (default: 50)
   :param offset: Pagination offset (default: 0)

   **Response**:

   .. code-block:: json

      {
        "total": 150,
        "offset": 0,
        "limit": 50,
        "channels": [
          {
            "id": "ch001",
            "name": "News Channel",
            "category": "News",
            "language": "en",
            "logo": "https://cdn.example.com/logos/news.png",
            "stream_url": "http://localhost:8080/stream/ch001.m3u8",
            "epg_id": "news-channel.us",
            "is_active": true
          }
        ]
      }

.. http:get:: /channels/{channel_id}

   Get details for a specific channel.

   **Path Parameters**:

   :param channel_id: The unique identifier of the channel

   **Response**:

   .. code-block:: json

      {
        "id": "ch001",
        "name": "News Channel",
        "description": "24/7 news coverage",
        "category": "News",
        "language": "en",
        "country": "US",
        "logo": "https://cdn.example.com/logos/news.png",
        "stream_url": "http://localhost:8080/stream/ch001.m3u8",
        "backup_streams": [
          "http://backup1.example.com/ch001.m3u8",
          "http://backup2.example.com/ch001.m3u8"
        ],
        "epg_id": "news-channel.us",
        "is_active": true,
        "created_at": "2024-01-01T00:00:00Z",
        "updated_at": "2024-01-15T12:00:00Z"
      }

.. http:post:: /channels

   Create a new channel (requires admin privileges).

   **Request Body**:

   .. code-block:: json

      {
        "name": "Sports Channel",
        "description": "Live sports coverage",
        "category": "Sports",
        "language": "en",
        "country": "US",
        "stream_url": "http://source.example.com/sports.m3u8",
        "logo_url": "https://cdn.example.com/logos/sports.png"
      }

   **Response**:

   .. code-block:: json

      {
        "id": "ch002",
        "name": "Sports Channel",
        "status": "created",
        "message": "Channel created successfully"
      }

.. http:put:: /channels/{channel_id}

   Update an existing channel.

   **Request Body**:

   .. code-block:: json

      {
        "name": "Updated Channel Name",
        "is_active": false
      }

.. http:delete:: /channels/{channel_id}

   Delete a channel (requires admin privileges).

EPG (Electronic Program Guide) API
----------------------------------

.. http:get:: /epg

   Retrieve EPG data for channels.

   **Query Parameters**:

   :param channel_id: Filter by specific channel
   :param start: Start time (ISO 8601 format)
   :param end: End time (ISO 8601 format)
   :param limit: Maximum number of programs (default: 100)

   **Response**:

   .. code-block:: json

      {
        "programs": [
          {
            "id": "prog001",
            "channel_id": "ch001",
            "title": "Morning News",
            "description": "Latest news and weather updates",
            "start_time": "2024-01-15T06:00:00Z",
            "end_time": "2024-01-15T09:00:00Z",
            "category": "News",
            "rating": "TV-G",
            "thumbnail": "https://cdn.example.com/epg/morning-news.jpg"
          }
        ]
      }

.. http:get:: /epg/{channel_id}/now

   Get currently playing program for a channel.

   **Response**:

   .. code-block:: json

      {
        "channel_id": "ch001",
        "current_program": {
          "id": "prog002",
          "title": "Midday Report",
          "start_time": "2024-01-15T12:00:00Z",
          "end_time": "2024-01-15T13:00:00Z",
          "progress": 45
        },
        "next_program": {
          "id": "prog003",
          "title": "Afternoon News",
          "start_time": "2024-01-15T13:00:00Z",
          "end_time": "2024-01-15T14:00:00Z"
        }
      }

Streams API
-----------

.. http:get:: /streams/{channel_id}/manifest

   Get HLS manifest for a channel.

   **Path Parameters**:

   :param channel_id: The channel identifier

   **Response**: M3U8 playlist content

   .. code-block:: text

      #EXTM3U
      #EXT-X-VERSION:3
      #EXT-X-STREAM-INF:BANDWIDTH=800000,RESOLUTION=640x360
      stream_360p.m3u8
      #EXT-X-STREAM-INF:BANDWIDTH=2500000,RESOLUTION=1280x720
      stream_720p.m3u8
      #EXT-X-STREAM-INF:BANDWIDTH=5000000,RESOLUTION=1920x1080
      stream_1080p.m3u8

.. http:get:: /streams/{channel_id}/{quality}.m3u8

   Get quality-specific HLS playlist.

   **Path Parameters**:

   :param channel_id: The channel identifier
   :param quality: Quality level (360p, 720p, 1080p, etc.)

Users API
---------

.. http:get:: /users/me

   Get current user profile.

   **Response**:

   .. code-block:: json

      {
        "id": "user123",
        "username": "john.doe",
        "email": "john@example.com",
        "subscription": {
          "plan": "premium",
          "status": "active",
          "expires_at": "2024-12-31T23:59:59Z"
        },
        "preferences": {
          "favorite_channels": ["ch001", "ch002"],
          "parental_control": false,
          "language": "en"
        }
      }

.. http:put:: /users/me/preferences

   Update user preferences.

   **Request Body**:

   .. code-block:: json

      {
        "favorite_channels": ["ch001", "ch003", "ch005"],
        "language": "es"
      }

Analytics API
-------------

.. http:get:: /analytics/viewers

   Get current viewer statistics (admin only).

   **Response**:

   .. code-block:: json

      {
        "total_viewers": 1523,
        "by_channel": [
          {
            "channel_id": "ch001",
            "channel_name": "News Channel",
            "viewers": 450
          },
          {
            "channel_id": "ch002",
            "channel_name": "Sports Channel",
            "viewers": 623
          }
        ],
        "peak_time": "20:00",
        "timestamp": "2024-01-15T20:30:00Z"
      }

Error Responses
---------------

All API errors follow a consistent format:

.. code-block:: json

   {
     "error": {
       "code": "CHANNEL_NOT_FOUND",
       "message": "The requested channel does not exist",
       "details": {
         "channel_id": "invalid_id"
       }
     }
   }

Common HTTP Status Codes:

* **200 OK**: Request successful
* **201 Created**: Resource created successfully
* **400 Bad Request**: Invalid request parameters
* **401 Unauthorized**: Authentication required or failed
* **403 Forbidden**: Insufficient permissions
* **404 Not Found**: Resource not found
* **429 Too Many Requests**: Rate limit exceeded
* **500 Internal Server Error**: Server error

Rate Limiting
-------------

API requests are rate-limited to ensure fair usage:

* **Free tier**: 100 requests per minute
* **Premium tier**: 1000 requests per minute
* **Admin tier**: No limit

Rate limit headers are included in responses:

.. code-block:: text

   X-RateLimit-Limit: 100
   X-RateLimit-Remaining: 95
   X-RateLimit-Reset: 1642267200

Webhooks
--------

Configure webhooks to receive real-time notifications:

.. http:post:: /webhooks

   Register a new webhook endpoint.

   **Request Body**:

   .. code-block:: json

      {
        "url": "https://your-server.com/webhook",
        "events": ["channel.online", "channel.offline", "viewer.joined"],
        "secret": "your-webhook-secret"
      }

Supported Events:

* ``channel.online``: Channel comes online
* ``channel.offline``: Channel goes offline
* ``viewer.joined``: User starts watching
* ``viewer.left``: User stops watching
* ``recording.started``: Recording begins
* ``recording.completed``: Recording finishes

SDK Examples
------------

Python Example
~~~~~~~~~~~~~~

.. code-block:: python

   import requests

   # Authenticate
   response = requests.post('http://localhost:8080/api/v1/auth/login',
                           json={'username': 'user', 'password': 'pass'})
   token = response.json()['access_token']

   # Get channels
   headers = {'Authorization': f'Bearer {token}'}
   channels = requests.get('http://localhost:8080/api/v1/channels',
                          headers=headers)

   print(channels.json())

JavaScript Example
~~~~~~~~~~~~~~~~~~

.. code-block:: javascript

   const token = 'your-jwt-token';

   // Get channels
   fetch('http://localhost:8080/api/v1/channels', {
     headers: {
       'Authorization': `Bearer ${token}`
     }
   })
   .then(response => response.json())
   .then(data => console.log(data));

Next Steps
----------

* Check :doc:`troubleshooting` for common issues
* Read :doc:`faq` for frequently asked questions
* Return to :doc:`index` for main documentation
