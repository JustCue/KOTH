---
layout: article
titles:
      en      : &EN       Weapon and Attachment Compatibility Chart
      en-GB   : *EN
      en-US   : *EN
      en-CA   : *EN
      en-AU   : *EN
      zh-Hans : &ZH_HANS  归档
      zh      : *ZH_HANS
      zh-CN   : *ZH_HANS
      zh-SG   : *ZH_HANS
      zh-Hant : &ZH_HANT  歸檔
      zh-TW   : *ZH_HANT
      zh-HK   : *ZH_HANT
      ko      : &KO       아카이브
      ko-KR   : *KO
      fr      : &FR       Archives
      fr-BE   : *FR
      fr-CA   : *FR
      fr-CH   : *FR
      fr-FR   : *FR
      fr-LU   : *FR
      tr      : &TR       Arşivdekiler
full_width: true
---





This chart details the compatibility of various weapons with a range of attachments, including suppressors and optics. A green checkmark (✅) indicates compatibility, while a red cross (❌) indicates incompatibility.

# Weapon and Attachment Compatibility


<style>
/* Responsive visibility for mobile vs desktop */
@media (min-width: 768px) {
  .mobile-view { display: none; }
  .desktop-view { display: block; }
}
@media (max-width: 767px) {
  .mobile-view { display: block; }
  .desktop-view { display: none; }
}

/* Desktop table styling */
table {
  width: 100%;
  max-width: 100%;
  border-collapse: collapse;
  table-layout: fixed;
  word-wrap: break-word;
}
th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
  overflow-wrap: break-word;
  word-break: break-word;
}
thead {
  background-color: #f2f2f2;
}
</style>

{% comment %}
Dynamically extract all unique attachment keys
{% endcomment %}
{% assign all_keys = "" %}
{% for item in site.data.weapon_compatibility %}
  {% for key in item.attachments %}
    {% unless all_keys contains key[0] %}
      {% assign all_keys = all_keys | append: key[0] | append: "," %}
    {% endunless %}
  {% endfor %}
{% endfor %}
{% assign attachment_keys = all_keys | split: "," | uniq | sort %}
{% assign attachment_keys = attachment_keys | reject: "" %}

<div class="desktop-view">
  <table>
    <thead>
      <tr>
        <th>Weapon</th>
        {% for key in attachment_keys %}
          <th>{{ key | replace: '_', ' ' }}</th>
        {% endfor %}
        <th>Suppressor</th>
      </tr>
    </thead>
    <tbody>
      {% for item in site.data.weapon_compatibility %}
      <tr>
        <td><strong>{{ item.weapon }}</strong></td>
        {% for key in attachment_keys %}
          <td>
            {% if item.attachments[key] == true %}
              ✅
            {% else %}
              ❌
            {% endif %}
          </td>
        {% endfor %}
        <td>
          {% if item.suppressor != "NA" %}
            ✅ ({{ item.suppressor }})
          {% else %}
            ❌
          {% endif %}
        </td>
      </tr>
      {% endfor %}
    </tbody>
  </table>
</div>

<div class="mobile-view">
  {% for item in site.data.weapon_compatibility %}
  <div style="border: 1px solid #ddd; border-radius: 8px; padding: 16px; margin: 10px 0; box-shadow: 0 2px 5px rgba(0,0,0,0.1);">
    <h3 style="margin-top: 0;">{{ item.weapon }}</h3>

    <div><strong>Attachments:</strong></div>
    <ul style="list-style: none; padding: 0;">
      {% for key in attachment_keys %}
        <li>{{ key | replace: '_', ' ' }}: {% if item.attachments[key] == true %}✅{% else %}❌{% endif %}</li>
      {% endfor %}
    </ul>

    <div>
      <strong>Suppressor:</strong>
      {% if item.suppressor != "NA" %}
        ✅ ({{ item.suppressor }})
      {% else %}
        ❌
      {% endif %}
    </div>
  </div>
  {% endfor %}
</div>