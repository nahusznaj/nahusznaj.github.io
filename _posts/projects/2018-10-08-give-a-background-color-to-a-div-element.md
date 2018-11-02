---
layout: article
title: HTML and CSS with Freecodecamp
categories: projects
modified: 2018-10-08T16:28:11-04:00
tags: [HTML, CSS]
comments: true
share: true
read_time: true
---


{"index.html":"<link href=\"https://fonts.googleapis.com/css?family=Lobster\" rel=\"stylesheet\" type=\"text/css\">\n<style>\n  .red-text {\n    color: red;\n  }\n\n  h2 {\n    font-family: Lobster, monospace;\n  }\n\n  p {\n    font-size: 16px;\n    font-family: monospace;\n  }\n\n  .thick-green-border {\n    border-color: green;\n    border-width: 10px;\n    border-style: solid;\n    border-radius: 50%;\n  }\n\n  .smaller-image {\n    width: 100px;\n  }\n  .silver-background {\n    background-color: silver;\n  }\n</style>\n\n<h2 class=\"red-text\">CatPhotoApp</h2>\n<main>\n  <p class=\"red-text\">Click here to view more <a href=\"#\">cat photos</a>.</p>\n  \n  <a href=\"#\"><img class=\"smaller-image thick-green-border\" src=\"https://bit.ly/fcc-relaxing-cat\" alt=\"A cute orange cat lying on its back.\"></a>\n  \n  <div class=\"silver-background\">\n    <p>Things cats love:</p>\n    <ul>\n      <li>cat nip</li>\n      <li>laser pointers</li>\n      <li>lasagna</li>\n    </ul>\n    <p>Top 3 things cats hate:</p>\n    <ol>\n      <li>flea treatment</li>\n      <li>thunder</li>\n      <li>other cats</li>\n    </ol>\n  </div>\n  \n  <form action=\"/submit-cat-photo\">\n    <label><input type=\"radio\" name=\"indoor-outdoor\" checked> Indoor</label>\n    <label><input type=\"radio\" name=\"indoor-outdoor\"> Outdoor</label><br>\n    <label><input type=\"checkbox\" name=\"personality\" checked> Loving</label>\n    <label><input type=\"checkbox\" name=\"personality\"> Lazy</label>\n    <label><input type=\"checkbox\" name=\"personality\"> Energetic</label><br>\n    <input type=\"text\" placeholder=\"cat photo URL\" required>\n    <button type=\"submit\">Submit</button>\n  </form>\n</main>"}