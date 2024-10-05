Here's the updated README with instructions on how to add the script to system services:

```
# WordPress-Automatic-Email-Testing-With-Telegram-Advanced-Alerts-Serverside

Overview

This Python script is designed to monitor the email logs of various WordPress sites, checking their status and notifying you via Telegram if any issues are detected. It can automatically check the logs for specified websites and send alerts if any failures occur.

Features

- Monitor email logs from multiple WordPress sites.
- Send Telegram notifications on email failures.
- Check log files every 5 minutes.
- Alert every 5 seconds if:
  - A log file is older than 1 hour.
  - An email send fails.
  - A log file is missing or empty.
- Easy to add or remove websites from monitoring.

Requirements

- Python 3.x
- requests library (can be installed via pip install requests)

Setup Instructions

1. Clone the Repository: Download the script to your server or local machine.

2. Configure Log Files:
   - Open the script file.
   - In the log_files dictionary, you can add as many websites as you want. Each entry should follow the format:
     ```
     "Website Name": "http://example.com/path/to/emaillog.txt"
     ```
   - For example:
     ```
     log_files = {
         "AZbrand.ca": "http://test.azbrand.ca/wp-content/plugins/emaillogger/emaillog.txt",
         "ExampleSite.ca": "https://examplesite.ca/htdocs/wp-content/plugins/emaillogger/emaillog.txt"
     }
     ```

3. Set Up Telegram Bot:
   - Create a new bot on Telegram by talking to BotFather.
   - After creating your bot, you'll receive a bot token. Replace bot_token in the script with your bot's token:
     ```
     bot_token = "YOUR_BOT_TOKEN"
     ```
   - To find your chat ID, you can send a message to your bot and then access the following URL in your web browser:
     ```
     https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates
     ```
   - Look for the "chat": {"id": ...} section in the response and use this value to set channel_id in the script:
     ```
     channel_id = "YOUR_CHAT_ID"
     ```

4. Run the Script:
   - Execute the script using Python:
     ```
     python WordPress-Automatic-Email-Testing-With-Telegram-Advanced-Alerts-Serverside.py
     ```

Adding to System Services (Linux)

To ensure the script runs continuously and restarts automatically on system reboots, you can add it to your system services. Here’s how to do it using `systemd`:

1. Create a Service File:
   - Open a terminal and create a new service file:
     ```
     sudo nano /etc/systemd/system/email-monitor.service
     ```

2. Add the Following Configuration:
   ```ini
   [Unit]
   Description=WordPress Email Monitor

   [Service]
   ExecStart=/usr/bin/python3 /path/to/WordPress-Automatic-Email-Testing-With-Telegram-Advanced-Alerts-Serverside.py
   WorkingDirectory=/path/to/
   StandardOutput=journal
   StandardError=journal
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```

   - Make sure to replace `/path/to/` with the actual path where your script is located.

3. Enable and Start the Service:
   - Run the following commands to enable and start the service:
     ```
     sudo systemctl enable email-monitor.service
     sudo systemctl start email-monitor.service
     ```

4. Check the Service Status:
   - You can check if the service is running with:
     ```
     sudo systemctl status email-monitor.service
     ```

Monitoring Logic

- The script checks the status of the specified log files every 5 minutes.
- Alerts are sent every 5 seconds if:
  - A log file is older than 1 hour.
  - An email send fails.
  - A log file is missing or empty.
- The script also checks for specific failures in the logs and will send alerts as needed.

Additional Information

- The script runs continuously, checking the status of the specified log files.
- It sends alerts via Telegram if any email failures are detected or if a log is older than one hour or missing.

Changelog

1.7.15
- Removed email from the public log.

1.7.14
- Added nonce verification to the form for improved security.
- Sanitized user input to prevent potential security issues.
- Updated UTC time handling for proper log file calculations.

1.0
- Initial release.

Upgrade Notice

1.7.15
- This update removes email from the public log for enhanced privacy and security.
```

This version includes detailed instructions on how to add the script to system services on a Linux machine. Let me know if you need any further adjustments!
