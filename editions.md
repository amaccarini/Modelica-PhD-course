---
layout: page
title: 📊 Previous editions
nav_order: 5
description: Info about previous editions
---

# 📊 Previous editions
<br>
The course has been conducted annually since 2021. Across all editions, 100+ students from over 50 organizations worldwide have attended the course. Hover over a highlighted country to see the affiliated organizations.

<div id="editions-map-container" style="position: relative; width: 100%; margin: 20px 0;">
  <svg id="editions-world-map" style="width: 100%; height: auto; display: block;"></svg>
  <div id="editions-tooltip" style="position: fixed; background: #ffffff; border: 1px solid #cccccc; padding: 10px 14px; border-radius: 6px; display: none; pointer-events: none; max-width: 280px; box-shadow: 2px 4px 12px rgba(0,0,0,0.18); font-size: 0.85em; z-index: 9999; line-height: 1.4;"></div>
</div>

<script src="https://d3js.org/d3.v7.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/topojson@3/dist/topojson.min.js"></script>
<script>
(function () {
  var orgs = {
    40:  { name: "Austria",         list: ["Graz University of Technology", "University of Applied Sciences Technikum Vienna"] },
    56:  { name: "Belgium",         list: ["University of Ghent", "KU Leuven"] },
    124: { name: "Canada",          list: ["Concordia University", "Polytechnique Montréal", "Université du Quebec", "University of Calgary", "Rensselaer Polytechnic Institute"] },
    196: { name: "Cyprus",          list: ["The Cyprus Institute"] },
    208: { name: "Denmark",         list: ["Aalborg University", "Aarhus University", "Technical University of Denmark", "University of Southern Denmark", "METROTHERM", "Grundfoss"] },
    233: { name: "Estonia",         list: ["Tallinn University of Technology"] },
    246: { name: "Finland",         list: ["Vaasa University"] },
    276: { name: "Germany",         list: ["Karlsruhe Institute of Technology", "Technical University of Munich", "Technische Hochschule Ingolstadt", "Bochum University of Applied Sciences", "Technical University of Darmstadt"] },
    356: { name: "India",           list: ["Indian Institute of Technology Madras"] },
    372: { name: "Ireland",         list: ["University College Dublin"] },
    380: { name: "Italy",           list: ["Polytechnic University of Milan", "Polytechnic University of Turin", "Sapienza University of Rome", "University of Padua", "University of Sannio", "Ricerca sul Sistema Energetico - RSE"] },
    528: { name: "Netherlands",     list: ["Eindhoven University of Technology", "University of Twente"] },
    578: { name: "Norway",          list: ["Norwegian University of Science and Technology", "University of Stavanger"] },
    724: { name: "Spain",           list: ["Universitat Politècnica de Catalunya", "Suno", "Tekniker"] },
    752: { name: "Sweden",          list: ["Linnaeus University"] },
    756: { name: "Switzerland",     list: ["Empa", "Lucerne University of Applied Sciences and Arts"] },
    826: { name: "United Kingdom",  list: ["University College London", "The University of Edinburgh"] },
    840: { name: "United States",   list: ["Arizona State University", "Harvard University", "Illinois Institute of Technology", "Lawrence Berkeley National Laboratory", "Louisiana State University", "North Carolina State University", "Pacific Northwest National Laboratory", "Purdue University", "Texas A&M University", "University of Alabama", "University of California, Berkeley", "Carrier", "Jacobs", "Vigilent"] }
  };

  var width = 960, height = 600;
  var svg = d3.select("#editions-world-map")
    .attr("viewBox", "0 0 " + width + " " + height)
    .attr("preserveAspectRatio", "xMidYMid meet");

  var projection = d3.geoNaturalEarth1()
    .scale(153)
    .translate([width / 2, height / 2]);

  var path = d3.geoPath().projection(projection);
  var tooltip = d3.select("#editions-tooltip");

  d3.json("https://cdn.jsdelivr.net/npm/world-atlas@2/countries-110m.json").then(function (world) {
    var countries = topojson.feature(world, world.objects.countries);

    svg.selectAll("path")
      .data(countries.features)
      .join("path")
      .attr("d", path)
      .attr("fill", function (d) { return orgs[+d.id] ? "#2979ff" : "#d4d4d4"; })
      .attr("stroke", "#ffffff")
      .attr("stroke-width", "0.5")
      .style("cursor", function (d) { return orgs[+d.id] ? "pointer" : "default"; })
      .on("mouseover", function (event, d) {
        var country = orgs[+d.id];
        if (country) {
          d3.select(this).attr("fill", "#0d47a1");
          var listHTML = country.list.map(function (o) {
            return "<li style='margin:3px 0;'>" + o + "</li>";
          }).join("");
          tooltip
            .html("<strong style='font-size:0.95em;'>" + country.name + "</strong><ul style='margin:6px 0 2px 0;padding-left:18px;'>" + listHTML + "</ul>")
            .style("display", "block");
        }
      })
      .on("mousemove", function (event) {
        var x = event.clientX + 16;
        var y = event.clientY - 12;
        var tipWidth = 280;
        if (x + tipWidth > window.innerWidth) { x = event.clientX - tipWidth - 10; }
        tooltip.style("left", x + "px").style("top", y + "px");
      })
      .on("mouseout", function (event, d) {
        d3.select(this).attr("fill", function () { return orgs[+d.id] ? "#2979ff" : "#d4d4d4"; });
        tooltip.style("display", "none");
      });
  });
}());
</script>
