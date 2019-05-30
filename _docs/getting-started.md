---
docid: getting-started
title: Install
layout: docs-getting-started
permalink: /docs/getting-started.html
---
{% capture mac %}{% include mac.md %}{% endcapture %}
{% capture ubuntu %}{% include ubuntu.md %}{% endcapture %}
{% capture centos %}{% include centos.md %}{% endcapture %}
{% capture windows %}{% include windows.md %}{% endcapture %}
{% capture ios %}{% include ios.md %}{% endcapture %}
{% capture android %}{% include android.md %}{% endcapture %}
{% capture docker %}{% include docker.md %}{% endcapture %}
{% capture raspbian %}{% include raspbian.md %}{% endcapture %}
{% capture tegra %}{% include tegra.md %}{% endcapture %}

{{mac | markdownify }}
{{ubuntu | markdownify }}
{{centos | markdownify }}
{{windows | markdownify }}
{{ios | markdownify }}
{{android | markdownify }}
{{docker | markdownify }}
{{raspbian | markdownify }}
{{tegra | markdownify }}
