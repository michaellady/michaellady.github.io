---
layout: page
title: Mike Lady Link In Bio
main_nav: false
permalink: /linkinbio/
---

<script>
function trackButtonClick(buttonName, url) {
  if (typeof gtag !== 'undefined') {
    gtag('event', 'button_click', {
      'button_name': buttonName,
      'button_url': url,
      'page_location': window.location.href
    });
  }
  window.location.href = url;
}
</script>

<button type="button" name="button" class="btn" onclick="trackButtonClick('Sandbox BJJ', 'http://sandboxbjj.com')">Sandbox BJJ</button>

<button type="button" name="button" class="btn" onclick="trackButtonClick('Intake Breathing Nasal Strip', 'https://amzn.to/3Ylblzv')">Intake Breathing Nasal Strip</button>

<button type="button" name="button" class="btn" onclick="trackButtonClick('Micro Plates for Progressive Overload', 'https://amzn.to/3X6shYb')">Micro Plates for Progressive Overload</button>

<button type="button" name="button" class="btn" onclick="trackButtonClick('Humans of Grappling Podcast', 'https://anchor.fm/humans-of-grappling')">Humans of Grappling Podcast</button>

<button type="button" name="button" class="btn" onclick="trackButtonClick('Be featured on the Humans of Grappling Podcast', 'https://calendly.com/mikelady/humans-of-grappling-podcast-recording')">Be featured on the Humans of Grappling Podcast</button>

<button type="button" name="button" class="btn" onclick="trackButtonClick('YouTube Channel', 'https://www.youtube.com/c/MikeLady')">YouTube Channel</button>