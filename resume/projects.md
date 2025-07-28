---
layout: default
title: Projects
---

Projects where I was the only significant code contributor are _italicized_, but successful projects have gone well beyond what I could have done alone.

<table>
    {% for project in site.data.projects %}
    <tr>
        <td><b><a href="{{ project[1].home }}">{{ project[0] }}</a></b></td>
        <td>
            <p>
                {{ project[1].about }}
            </p>

            <p>
                <a href="{{ project[1].github }}">On github:</a>
                <a href="{{ project[1].github }}/pulls?q=is%3Apr+is%3Aclosed+author%3Amccalluc">my commits</a>.
                
                {% for tech in project[1].tech %}
                    {{ tech }}{% if forloop.last != true %}, {% endif %}{% endfor %}.
            </p>
        </td>
    </tr>
    {% endfor %}
</table>
