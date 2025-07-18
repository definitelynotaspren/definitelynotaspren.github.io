---
layout: default
title: Home
---

<button id="questionBtn">What questions should I be asking?</button>
<div id="suggestions"></div>

<script>
document.getElementById('questionBtn').addEventListener('click', function () {
  fetch('{{ "/assets/comments/latest.json" | relative_url }}')
    .then(function (res) { return res.json(); })
    .then(function (data) {
      var container = document.getElementById('suggestions');
      container.innerHTML = '';
      var card = document.createElement('div');
      card.className = 'suggestion-card';
      var summary = document.createElement('p');
      summary.textContent = data.summary;
      card.appendChild(summary);
      var actionsWrap = document.createElement('div');
      data.actions.forEach(function (a) {
        var span = document.createElement('span');
        span.className = 'action-badge';
        span.textContent = a;
        actionsWrap.appendChild(span);
      });
      card.appendChild(actionsWrap);
      container.appendChild(card);
    });
});
</script>
