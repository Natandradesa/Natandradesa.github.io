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

  - block: markdown
    content:
      title: '📚 My Research'
      subtitle: ''
      text: |-
        {{/* Hugo Blox: Contact */}}
{{/* Documentation: https://hugoblox.com/blocks/ */}}
{{/* License: https://github.com/HugoBlox/hugo-blox-builder/blob/main/LICENSE.md */}}

{{/* Initialise */}}
{{ $page := .wcPage }}
{{ $block := .wcBlock }}
{{ $autolink := default true $block.content.autolink }}
{{ $data := $block.content }}

{{ $form_provider := lower $block.content.form.provider | default "" }}

{{ $use_netlify_form := eq $form_provider "netlify" }}
{{ $use_formspree_form := eq $form_provider "formspree" }}
{{ $use_form := or $use_netlify_form $use_formspree_form }}

{{ $use_netlify_captcha := $block.content.form.netlify.captcha | default true }}
{{ $use_formspree_captcha := $block.content.form.formspree.captcha | default false }}

{{ $columns := $block.design.columns | default "2" }}

{{ if and $use_formspree_form $use_formspree_captcha }}
  <script src="https://www.google.com/recaptcha/api.js" async defer></script>
{{ end }}

<div class="col-12 {{if eq $columns "2"}}col-lg-8{{end}}">
  {{ with $block.content.text }}<p>{{ . | emojify | $page.RenderString }}</p>{{ end }}

  {{ if $use_form }}

  {{ $post_action := "" }}
    {{ if $use_netlify_form }}
      {{ $post_action = "netlify" }}
    {{ else if $use_formspree_form }}
      {{ if not $block.content.form.formspree.id }}
        {{ errorf "You have chosen to use Formspree as the provider for the contact form. Please set your Formspree Form ID in the Contact widget or disable the form.\nDocumentation: https://docs.hugoblox.com/widget/contact/" }}
      {{ end }}
      {{ if and $use_formspree_captcha (not $block.content.form.formspree.captcha_key) }}
        {{ errorf "You have chosen to use reCAPTCHA for Formspree. Please set your Formspree CAPTCHA KEY in the Contact widget or disable reCAPTCHA.\nDocumentation: https://help.formspree.io/hc/en-us/articles/360022811154" }}
      {{ end }}
      {{ $post_action = printf "action=\"https://formspree.io/f/%s\"" $block.content.form.formspree.id }}
    {{ end }}

  <div class="mb-3">
      <form name="contact" method="POST" {{ $post_action | safeHTMLAttr }} {{ if $use_netlify_form }}netlify-honeypot="_gotcha"{{ end }} {{ if $use_netlify_captcha }}data-netlify-recaptcha="true"{{ end }} {{ with $block.content.form.netlify.success_url }}action="{{ . | relLangURL }}"{{ end }}>
        <div class="form-group form-inline">
          <label class="sr-only" for="inputName">{{ i18n "contact_name" }}</label>
          <input type="text" name="name" class="form-control w-100" id="inputName" placeholder="{{ i18n "contact_name" | default "Name" }}" required>
        </div>
        <div class="form-group form-inline">
          <label class="sr-only" for="inputEmail">{{ i18n "contact_email" }}</label>
          <input type="email" name="email" class="form-control w-100" id="inputEmail" placeholder="{{ i18n "contact_email" | default "Email" }}" required>
        </div>
        <div class="form-group">
          <label class="sr-only" for="inputMessage">{{ i18n "contact_message" }}</label>
          <textarea name="message" class="form-control" id="inputMessage" rows="5" placeholder="{{ i18n "contact_message" | default "Message" }}" required></textarea>
        </div>
        {{ if $block.content.form.netlify.attachments }}
          <div class="form-group form-inline">
            <label class="sr-only" for="fileUpload">{{ i18n "contact_attachment" }}</label>
            <input type="file" name="file" class="form-control w-100" id="fileUpload" placeholder="{{ i18n "contact_attachment" | default "Attach file" }}">
          </div>
        {{ end }}
        <div class="d-none">
          <label>Do not fill this field unless you are a bot: <input name="_gotcha"></label>
        </div>
        {{ if and $use_netlify_form $use_netlify_captcha }}
          <div class="form-group" data-netlify-recaptcha="true"></div>
        {{ else if and $use_formspree_form $use_formspree_captcha }}
          <div class="g-recaptcha" data-sitekey="{{ $block.content.form.formspree.captcha_key }}"></div>
          </br>
        {{ end }}
        <button type="submit" class="btn btn-primary px-3 py-2 w-100">{{ i18n "contact_send" | default "Send" }}</button>
      </form>
    </div>
  {{ end }}

  <ul class="fa-ul">

  {{ if $data.email }}
    <li>
      <i class="fa-li fas fa-envelope fa-2x" aria-hidden="true"></i>
      <span id="person-email">
      {{- if $autolink }}<a href="mailto:{{ $data.email }}">{{ $data.email }}</a>{{ else }}{{ $data.email }}{{ end -}}
      </span>
    </li>
    {{ end }}

  {{ with $data.phone }}
    <li>
      <i class="fa-li fas fa-phone fa-2x" aria-hidden="true"></i>
      <span id="person-telephone">
      {{- if $autolink }}<a href="tel:{{ . }}">{{ . }}</a>{{ else }}{{ . }}{{ end -}}
      </span>
    </li>
    {{ end }}

  {{ $addr_formatted := "" }}{{/* Scoping for maps. */}}
    {{ if $data.address.street | or $data.address.city | or $data.address.region | or $data.address.postcode | or $data.address.country }}
      {{ $addr_formatted = partial "functions/get_address" (dict "root" . "address" $data.address) }}
      <li>
        <i class="fa-li fas fa-map-marker fa-2x" aria-hidden="true"></i>
        <span id="person-address">{{$addr_formatted}}</span>
      </li>
    {{ end }}

  {{ with $data.directions }}
    <li>
      <i class="fa-li fas fa-compass fa-2x" aria-hidden="true"></i>
      <span>{{ . | markdownify | emojify }}</span>
    </li>
    {{ end }}

  {{ with $data.office_hours }}
    <li>
      <i class="fa-li fas fa-clock fa-2x" aria-hidden="true"></i>
      <span>
        {{- if not (reflect.IsSlice .)}}{{/* Support legacy string format. */}}
          {{- . | markdownify | emojify -}}
        {{else}}
          {{- delimit . "<br>" | markdownify | emojify -}}
        {{end -}}
      </span>
    </li>
    {{ end }}

  {{ with $data.appointment_url }}
    <li>
      <i class="fa-li fas fa-calendar-check fa-2x" aria-hidden="true"></i>
      <a href="{{ . }}" target="_blank" rel="noopener">{{ i18n "book_appointment" | default "Book an appointment" }}</a>
    </li>
    {{ end }}

  {{/* Contact links. */}}
    {{ range $data.contact_links }}
    {{ $pack := or .icon_pack "fas" }}
    {{ $pack_prefix := $pack }}
    {{ if in (slice "fab" "fas" "far" "fal") $pack }}
      {{ $pack_prefix = "fa" }}
    {{ end }}
    {{ $link := .link }}
    {{ $scheme := (urls.Parse $link).Scheme }}
    {{ $target := "" }}
    {{ if not $scheme }}
      {{ $link = .link | relLangURL }}
    {{ else if in (slice "http" "https") $scheme }}
      {{ $target = "target=\"_blank\" rel=\"noopener\"" }}
    {{ end }}
    <li>
      <i class="fa-li {{ $pack }} {{ $pack_prefix }}-{{ .icon }} fa-2x" aria-hidden="true"></i>
      <a href="{{ $link | safeURL }}" {{ $target | safeHTMLAttr }}>{{.name|markdownify|emojify|safeHTML}}</a>
    </li>
    {{ end }}

  </ul>

  {{ if and site.Params.features.map.provider $data.coordinates.latitude }}
  <div class="d-none">
    <input id="map-provider" value="{{ lower site.Params.features.map.provider }}">
    <input id="map-lat" value="{{ $data.coordinates.latitude }}">
    <input id="map-lng" value="{{ $data.coordinates.longitude }}">
    <input id="map-dir" value="{{ $addr_formatted }}">
    <input id="map-zoom" value="{{ site.Params.features.map.zoom | default "15" }}">
    <input id="map-api-key" value="{{ site.Params.features.map.api_key }}">
  </div>
  <div id="map"></div>
  {{ end }}

</div>
    design:
      columns: '1'
---
