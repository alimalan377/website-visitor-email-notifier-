# website-visitor-email-notifier-
when you need a notif from your web site by an email you can use it
git clone https://github.com/USERNAME/website-visitor-email-notifier.git

cd website-visitor-email-notifier

pip install -r requirements.txt

python3 app.py
Flask
Flask-Mail
from flask import Flask, request
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from datetime import datetime

app = Flask(__name__)

# ==========================
# Gmail Configuration
# ==========================

GMAIL_EMAIL = "YOUR_GMAIL@gmail.com"
GMAIL_APP_PASSWORD = "YOUR_APP_PASSWORD"

RECEIVER_EMAIL = "YOUR_GMAIL@gmail.com"

# ==========================


def send_email(ip, browser, referer):

    subject = "🚨 New Website Visitor"

    body = f"""
A new visitor has entered your website.

Time:
{datetime.now()}

IP Address:
{ip}

Browser:
{browser}

Referer:
{referer}
"""

    msg = MIMEMultipart()
    msg["From"] = GMAIL_EMAIL
    msg["To"] = RECEIVER_EMAIL
    msg["Subject"] = subject

    msg.attach(MIMEText(body, "plain"))

    try:

        server = smtplib.SMTP("smtp.gmail.com", 587)
        server.starttls()

        server.login(GMAIL_EMAIL, GMAIL_APP_PASSWORD)

        server.sendmail(
            GMAIL_EMAIL,
            RECEIVER_EMAIL,
            msg.as_string()
        )

        server.quit()

        print("Email Sent!")

    except Exception as e:
        print(e)


@app.route("/")

def home():

    ip = request.headers.get(
        "X-Forwarded-For",
        request.remote_addr
    )

    browser = request.headers.get(
        "User-Agent"
    )

    referer = request.headers.get(
        "Referer",
        "Direct Visit"
    )

    send_email(
        ip,
        browser,
        referer
    )

    return """
    <h1>Welcome!</h1>
    <p>Your visit has been recorded.</p>
    """


if __name__ == "__main__":

    app.run(
        host="0.0.0.0",
        port=5000,
        debug=True
    )
    sudo apt update

sudo apt install python3-pip

pip3 install flask
python3 app.py

this is finally you got 
New Website Visitor

IP:
185.xxx.xxx.xxx

Time:
2026-06-27 19:34

Browser:
Chrome 138

OS:
Windows 11

User-Agent:
Mozilla/5.0 ...
