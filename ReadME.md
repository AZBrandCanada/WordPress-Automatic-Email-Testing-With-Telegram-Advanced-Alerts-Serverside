
# WordPress-Automatic-Email-Testing-With-Telegram-Advanced-Alerts-Serverside

## Overview

This Python script is designed to monitor the email logs of various WordPress sites, checking their status and notifying you via Telegram if any issues are detected. It can automatically check the logs for specified websites and send alerts if any failures occur.
This Monitor Works In Conjunction With The Wordpress Plugin 
https://github.com/AZBrandCanada/Wordpress-Automatic-Email-Testing-With-Telegram-Alerts

## Features

- Monitor email logs from multiple WordPress sites.
- Send Telegram notifications on email failures.
- Check log files every 5 minutes.
- Alert every 10 minutes if:
  - A log file is older than 8 hours.
  - An email send fails.
  - A log file is missing or empty.
- Easy to add or remove websites from monitoring.

## Requirements

- Python 3.x
- requests library (can be installed via `pip install requests`)

## Setup Instructions

1. **Clone the Repository**: Download the script to your server or local machine.

2. **Configure Log Files**:
   - Open the script file.
   - In the `log_files` dictionary, you can add as many websites as you want. Each entry should follow the format:
     ```
     "Website Name": "http://example.com/wp-content/plugins/automatic-email-testing-with-telegram-alerts/emaillog.txt"
     ```
   - For example:
     ```
     log_files = {
         "AZbrand.ca": "http://test.azbrand.ca/wp-content/plugins/automatic-email-testing-with-telegram-alerts/emaillog.txt",
         "ExampleSite.ca": "https://examplesite.ca/htdocs/wp-content/plugins/automatic-email-testing-with-telegram-alerts/emaillog.txt"
     }
     ```

3. **Set Up Telegram Bot**:
   - Create a new bot on Telegram by talking to BotFather.
   - After creating your bot, you'll receive a bot token. Replace `bot_token` in the script with your bot's token:
     ```
     bot_token = "YOUR_BOT_TOKEN"
     ```
   - To find your chat ID, you can send a message to your bot and then access the following URL in your web browser:
     ```
     https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates
     ```
   - Look for the `"chat": {"id": ...}` section in the response and use this value to set `channel_id` in the script:
     ```
     channel_id = "YOUR_CHAT_ID"
     ```

4. **Run the Script**:
   - Execute the script using Python:
     ```
     python3 1.13TestEmail.py
     ```

## Adding to System Services (Linux)

To ensure the script runs continuously and restarts automatically on system reboots, you can add it to your system services. Here’s how to do it using `systemd`:

1. **Create a Service File**:
   - Open a terminal and create a new service file:
     ```
     sudo nano /etc/systemd/system/email-monitor.service
     ```

2. **Add the Following Configuration**:
   ```
   [Unit]
   Description=WordPress Email Monitor

   [Service]
   ExecStart=/usr/bin/python3 /path/to/1.13TestEmail.py
   WorkingDirectory=/path/to/
   StandardOutput=journal
   StandardError=journal
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```

## Changelog
= 1.8.13 =
* Admin Styling

= 1.8.12 =
* Fixed Null Variable
* Fixed Performance Degredation

= 1.8.1 =
* Tested Wordpress 6.9
* Provided Legacy Support for PHP 7.3

= 1.7.19 =
* Updated JavaScript to correctly calculate the time difference between current UTC time and next email send time.
* Added a clear indication when an email is currently being sent.
* Improved the display format of current time and countdown timer.
* Added custom classes for HTML and JavaScript elements.

= 1.7.18 =
* Improved internationalization: avoided using variables or defines as text, context, or text domain parameters.
* Documented use of third-party API (api.telegram.org).
* Updated to use `wp_enqueue` commands for better script management.
* Created unique prefixes for generic function/class/define/namespace/option names.
* Updated transient prefixes.

= 1.7.17 =
* Added new functionality to handle edge cases in email scheduling.
* Improved error logging for better diagnostics.
* Enhanced security features to protect against potential vulnerabilities.

= 1.7.16 =
* Updated the license information to include CC BY-ND 4.0 details.

= 1.7.15 =
Removed email from the public log.

= 1.7.14 =
Added nonce verification to the form for improved security.
Sanitized user input to prevent potential security issues.
Updated UTC time handling for proper log file calculations.

= 1.0 =
Initial release.

## Upgrade Notice

= 1.7.15 =
This update removes email from the public log for enhanced privacy and security.

---

Feel free to let me know if you need any additional changes!
