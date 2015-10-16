---
title: Get In Touch
description: Use the form below to give /dev/null a piece of your mind.
body_class: contact
icon: envelope
menu: Contact
form:
    name: my-nice-form
    fields:
        - name: name
          label: Name
          framework_size: half
          placeholder: Name
          autofocus: on
          autocomplete: on
          type: text
          validate:
            required: true

        - name: email
          framework_size: half
          label: Email
          placeholder: name@example.com
          type: text
          validate:
            rule: email
            required: true

        - name: message
          framework_size: full
          label: Message
          size: long
          placeholder: Your message here
          type: textarea
          validate:
            required: true

    buttons:
        - type: submit
          value: Submit

    process:
        - email:
            from: "{{ config.plugins.email.from }}"
            to:
              - "{{ config.plugins.email.from }}"
              - "{{ form.value.email }}"
            subject: "[Feedback] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: feedback-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - message: Thank you for your feedback!
        - display: thankyou
buttons:
    - text: Take My Money
      url: '#'
      class: special
    - text: LOL Wut
      url: '#'      
---
