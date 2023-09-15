---
# Leave the homepage title empty to use the site title
title:
date: 2023-09-15
type: landing

sections:
  - block: about.biography
    id: about
    content:
      title: 
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: admin
      design:
        background:
          image: 
            filename: sweden1.jpg
            filters: 
              brightness: 0.1
            # Text color (true=light, false=dark, or remove for the dynamic theme color).
            text_color_light: true
          #  Image fit. Options are `cover` (default), `contain`, or `actual` size.
            size: cover
          # Image focal point. Options include `left`, `center` (default), or `right`.
            position: center
          # Use a fun parallax-like fixed background effect on desktop? true/false
            parallax: true


  - block: collection
    id: publications
    content:
      title: Recent Publications
      text: |-
          {{% callout note %}}
          Quickly discover relevant content by [filtering publications](./publication/).
          {{% /callout %}}
      filters:
        folders:
          - publication
        exclude_featured: true
    design:
      columns: '2'
      view: citation

  - block: contact
    id: contact
    content:
      title: Contact
      # Automatically link email and phone or display as text?
      autolink: true
      email: Raymond.zhang[atchoum]hotmail.fr
      # phone: 888 888 88 88
      address:
        street: 3 rue Joliot-Curie
        city: Gif-sur-Yvette
        region: Essonne
        postcode: '91190'
        country: France
        country_code: '+33'
        # coordinates:
        #   latitude: '37.4275'
        #   longitude: '-122.1697'
      directions: Batiment Bréguet
        # office_hours:
        #   - 'Monday 10:00 to 13:00'
        #   - 'Wednesday 09:00 to 10:00'
        # appointment_url: 'https://calendly.com'
        # contact_links:
        #   - icon: twitter
        #     icon_pack: fab
        #     name: DM Me
        #     link: 'https://twitter.com/Twitter'
        #   - icon: skype
        #     icon_pack: fab
        #     name: Skype Me
        #     link: 'skype:echo123?call'
        #   - icon: keybase
        #     icon_pack: fab
        #     name: Chat on Keybase
        #     link: 'https://keybase.io/'
        #   - icon: comments
        #     icon_pack: fas
        #     name: Discuss on Forum
        #     link: 'https://discourse.gohugo.io'
        
        # # Email form provider
        # form:
        #   provider: netlify
        #   formspree:
        #     id:
        #   netlify:
        #     # Enable CAPTCHA challenge to reduce spam?
        #     captcha: true    
    design:
      columns: '2'
---