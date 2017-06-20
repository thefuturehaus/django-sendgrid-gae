Django-SendGrid-GAE
===============

Simple Django backend to send email using SendGrid's Web API on GAE using task queues.

Installation
------------

Install the backend from PyPI:

.. code:: bash

    pip install fh-django-sendgrid-gae

Add the following to your project's **settings.py**:

.. code:: python

    EMAIL_BACKEND = "sgbackend.SendGridBackend"
    SENDGRID_API_KEY = "Your SendGrid API Key"

**Done!**

Example
-------

.. code:: python


    from django.core.mail import send_mail
    from django.core.mail import EmailMultiAlternatives

    send_mail("Your Subject", "This is a simple text email body.",
      "Test User <test@example.com>", ["test@example.com"])

    # or
    mail = EmailMultiAlternatives(
      subject="Your Subject",
      body="This is a simple text email body.",
      from_email="Test User <test@example.com>",
      to=["test@example.com"],
      headers={"Reply-To": "tester@example.com"}
    )
    # Add template
    mail.template_id = 'YOUR TEMPLATE ID FROM SENDGRID ADMIN'

    # Replace substitutions in sendgrid template
    mail.substitutions = {'%username%': 'testuser'}

    # Attach file
    with open('somefilename.pdf', 'rb') as file:
        mail.attachments = [
            ('somefilename.pdf', file.read(), 'application/pdf')
        ]

    mail.attach_alternative(
        "<p>This is a simple HTML email body</p>", "text/html"
    )

    mail.send()


License
-------
MIT


Enjoy :)
