---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
{% assign release_notes = site.data.release_notes | sort: 'version' | reverse %}
{% for release in release_notes %}
{% assign version_parts = release.version | split: '.' %}
{% assign major_version = version_parts[0] | capitalize %}
{% assign minor_version = version_parts[1] %}

{% if forloop.first or major_version != previous_major_version %}
# UAT {{ major_version }}.x.x.x
{% assign previous_major_version = major_version %}
{% endif %}

{% if forloop.first or minor_version != previous_minor_version %}
## {{ major_version }}.{{ minor_version }}.x.x
{% assign previous_minor_version = minor_version %}
{% endif %}

{{ release.note_link }}

{% endfor %}

