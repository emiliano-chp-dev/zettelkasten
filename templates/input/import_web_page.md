---
aliases: {{title | replace(":", "") | replace("#", "") | replace("^", "") | replace("|", "") | replace("\[", "") | replace("\]", "") | replace("\\", "") | replace("/", "")}}
citation_key: {{citekey}}
item_type: {{itemType | default("null")}}
title: {{title | replace(":", "") | replace("#", "") | replace("^", "") | replace("|", "") | replace("\[", "") | replace("\]", "") | replace("\\", "") | replace("/", "")}}
author: {{authors | default ("null")}}
website_title: {{websiteTitle | default("null")}}
website_type: {{websiteType | default("null")}}
date: {% if date %}{{date | format("yyyy")}}{% else %}null{% endif %}
short_title: {{shortTitle | default("null")}}
url: {{URL | default("null")}}
accessed: {% if accessDate %}{{accessDate | format("yyyy-MM-DD, hh:mm")}}{% else %}null{% endif %}
language: {{language | default("null")}}
rights: {{rights | default("null")}}
extra: "{{extra | default("null")}}"
date_added: {% if dateAdded %}{{dateAdded | format("yyyy-MM-DD, hh:mm")}}{% else %}null{% endif %}
last_modified: {% if dateModified %}{{dateModified | format("yyyy-MM-DD, hh:mm")}}{% else %}null{% endif %}
status: "#awaiting_review"
---

# {{title}}

> [!Link]
> Zotero link: {{firstAttachmentZoteroLink}}

> [!Cite]
> Citation key: {{citekey}}

> [!Abstract]
> {% if abstractNote -%}
> {{ abstractNote }}
> {% else -%}
> No abstract available
> {% endif %}

> [!Keywords]
> {% if allTags %}
> {% for tag in allTags.split(',') %}
>  {{tag.trim()}}
> {% endfor %}
> {% else %}
> Add some tags in Zotero.
> {% endif %}

> [!Meta]
> Item Type: {{itemType}}
> Title: {{title}}
> Author: {{authors}}
> Edition: {{edition}}
> Place: {{place}}
> Publisher: {{publisher}}
> Date: {{date | format("yyyy")}}
> ISBN: {{ISBN}}

> [!related]
{% for relation in relations -%}
{%- if relation.citekey -%}
> Related: {{relation.citekey}}
{% endif -%}
{%- endfor %}

```dataview
TABLE created, updated as modified, tags, type
FROM ""
WHERE related != null
AND contains(related, "{{citekey}}")
```

> [!summary] Summary of Key Points
> -

## Notes

| Highlight Color</mark>                  | Meaning                      |
| --------------------------------------- | ---------------------------- |
| <mark class="hltr-grey">Grey</mark>     | Mark a chapter or subchapter |
| <mark class="hltr-red">Red</mark>       | Disagree with Aauthor        |
| <mark class="hltr-orange">Orange</mark> | Important                    |
| <mark class="hltr-yellow">Yellow</mark> | Interesting                  |
| <mark class="hltr-green">Green</mark>   | Relevant                     |
| <mark class="hltr-blue">Blue</mark>     | Interesting                  |
| <mark class="hltr-purple">Purple</mark> | Research                     |

{% for annotation in annotations -%}
    {%- if annotation.annotatedText -%} 
		- <mark class="hltr-{{annotation.colorCategory | lower}}">"{{annotation.annotatedText | escape}}”</mark> [Page {{annotation.page}}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}})
    {%- endif %} 
    {%- if annotation.imageRelativePath -%}
    ![[{{annotation.imageRelativePath}}]] {%- endif %} 
{%- if annotation.comment %} 
	- {{annotation.comment}} 
{%- endif %} 
{% endfor %}