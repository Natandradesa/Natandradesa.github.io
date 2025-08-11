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
    content:
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: admin
      text: ""
      # Show a call-to-action button under your biography? (optional)
      button:
        text: Download CV
        url: uploads/resume.pdf
    design:
      css_class: dark
      background:
        color: black
        image:
          # Add your image background to `assets/media/`.
          #filename: stacked-peaks.svg
          filename: background_image.svg
          filters:
            brightness: 1.0
          size: cover
          position: center
          parallax: false
  #- block: markdown
  #  content:
  #    title: '📚 My Research'
  #    subtitle: ''
  #    text: |-
  #      Use this area to speak to your mission. I'm a research scientist in the Moonshot team at DeepMind. I blog about machine learning, deep learning, and moonshots.
  #
  #      I apply a range of qualitative and quantitative methods to comprehensively investigate the role of science and technology in the economy.
  #      
  #      Please reach out to collaborate 😃
  #  design:
  #    columns: '1'
  
  #- block: collection
  #  id: papers
  #  content:
  #    title: Featured Publications
  #    filters:
  #      folders:
  #        - publication
  #      featured_only: true
  #  design:
  #    view: article-grid
  #    columns: 2
  - block: collection
    id: papers
    content:
      title: Publications
      text: ""
      filters:
        folders:
          - publication
        exclude_featured: false
    design:
      view: citation
      #background:
      #  gradient_start: '#004ba0'
      #  gradient_end: '#1976d2'
      #  text_color_light: false
  #- block: collection
  #  id: talks
  #  content:
  #    title: Recent & Upcoming Talks
  #    filters:
  #      folders:
  #        - event
  #  design:
  #    view: article-grid
  #    columns: 1
    
  - block: collection
    id: news
    content:
      title: Recent News
      filters:
        folders:
          - post
    design:
      view: article-grid
      columns: 1
  - block: markdown
    content:
      title: "Get In Touch"
      text: |
        **Email:** [jnas@cin.ufpe.br](mailto:jnas@cin.ufpe.br)  
        **Telefone:** +55 (11) 99999-9999  
        **Endereço:** Rua Exemplo, 123 - São Paulo, SP
    
  - block: markdown
    content:
      title: "Get In Touch"
      text: |
        **Email:** [meuemail@exemplo.com](mailto:meuemail@exemplo.com)  
        **Telefone:** +55 (11) 99999-9999  
        **Endereço:** Rua Exemplo, 123 - São Paulo, SP  

        <a href="mailto:meuemail@exemplo.com" class="btn btn-primary">
          <i class="fas fa-envelope"></i> Mail me
        </a>
    
  #- block: collection
  #  id: news
  #  content:
  #    title: Recent News
  #    subtitle: ''
  #    text: ''
  #    # Page type to display. E.g. post, talk, publication...
  #    page_type: post
  #    # Choose how many pages you would like to display (0 = all pages)
  #    count: 5
  #    # Filter on criteria
  #    filters:
  #      author: ""
  #      category: ""
  #      tag: ""
  #      exclude_featured: false
  #      exclude_future: false
  #      exclude_past: false
  #      publication_type: ""
  #    # Choose how many pages you would like to offset by
  #    offset: 0
  #    # Page order: descending (desc) or ascending (asc) date.
  #    order: desc
  #  design:
  #    # Choose a layout view
  #    #view: date-title-summary
  #    view: article-grid
  #    # Reduce spacing
  #    spacing:
  #      padding: [0, 0, 0, 0]

---
