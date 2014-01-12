---
layout: page
permalink: /latex-math/
title: Online LaTeX math rendering
use_mathjax: true
extra_header_html: |
  <script type="text/x-mathjax-config">
  MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
  });
  </script>
extra_footer_html: |
  <script type="text/javascript" src="/assets/js/lz.min.js"></script>
  <script type="text/javascript">
  var render = function() {
    var latex = $("#latex-code").val();
    $("#rendered-latex").text(latex);
    MathJax.Hub.Queue(["Typeset",MathJax.Hub,"rendered-latex"]);
    var latex_encoded = LZString.compressToBase64(latex);
    window.location.hash = latex_encoded;
    $("#share_url").val(window.location);
    $("#share-wrapper").css("display", "block");
  };
  $("#render-latex-btn").on('click', render);
  var decode_hash = function() {
    if (window.location.hash.length > 0) {
      var latex = LZString.decompressFromBase64(window.location.hash.slice(1));
      if (latex == null) {
        $("#rendered-latex").text('Error: Provided URL cannot be decoded correctly.');
        alert('Error: Provided URL cannot be decoded correctly.');
      } else {
        $("#latex-code").val(latex);
        render();
      }
    }
  };
  decode_hash();
  window.onhashchange = decode_hash;
  </script>

---

Are you chatting with someone online and want to send them an equation?

Type or paste the `LaTeX` equations here, including the `$$` or `\begin{ ... }` tags:
<textarea id="latex-code" style="width:100%" rows="8" title="Type or paste LaTeX equation here"></textarea>
<input type="button" id="render-latex-btn" name="render-latex" value="Click here to render LaTeX equations" />

<p id="rendered-latex"></p>

<p id="share-wrapper" style="display:none">
URL for sharing: <br />
<textarea id="share_url" style="width:100%" rows="5"></textarea>
</p>

<hr />

Tip: you can paste paragraph text with embedded inline equations. LaTeX math markers (such as `$` and `$$`) are used to determine where equations start and finish.

[Click here for the technical information on how this works.](/blog/2013/online-latex-equation-rendering/)
