---
# Leave the homepage title empty to use the site title
title: ""
date: 2022-10-24
type: landing

design:
  # Default section spacing
  spacing: "6rem"

sections:
  - block: resume-biography-3
    id: about
    content:
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: me
      text: |-
        I was a PhD Student at the L2S lab at CentraleSupelec under the supervision of
        [Richard Combes](http://rcombes.supelec.free.fr/) and
        [Sheng Yang](https://l2s.centralesupelec.fr/u/yang-sheng/)
      # Show a call-to-action button under your biography? (optional)
      button:
        text: Download CV
        url: uploads/CV_Raymond_Zhang_EN.pdf
    design:
      background:
        image:
          # Add your image background to `assets/media/`.
          filename: sweden1.jpg
          filters:
            brightness: 0.6
          size: cover
          position: center
          parallax: false

  - block: collection
    id: news
    content:
      title: News
      subtitle: Latest updates
      filters:
        folders:
          - events
    design:
      view: date-title-summary
      columns: 1

  - block: collection
    id: publications
    content:
      title: Publications
      filters:
        folders:
          - publications
        featured_only: 
    design:
      view: citation
      columns: 1
      flip_alt_rows: true
---
