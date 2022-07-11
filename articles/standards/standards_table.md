---
layout: table
type: standards
title: Standards Table
---
<style>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  overflow-x: scroll;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 15px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>

<table>
  <tr>
    <th> <font size="4">Algorithms</font> </th>
    <th> <font size="4">Recommended</font></th>
    <th> <font size="4">Acceptable</font> </th>
    <th> <font size="4">Disable</font></th>
    <th> <font size="4">Future</font> </th>
    <th> <font size="4">Debated</font> </th>
    <th> <font size="4">FIPS140</font> </th>
    <th> <font size="4">CC </font></th>
    <th> <font size="4">SuiteB </font></th>
    <th> <font size="4">CSFC </font></th>
    <th> <font size="4">PCI</font> </th>
  </tr>
  {% for member in site.data.members %}
  <tr>
    <td> <strong>{{member.Algorithm}}</strong> </td>
    <td> {{member.recommended}}</td>
    <td> {{member.acceptable}} </td>
    <td> {{member.avoid}}</td>
    <td> {{member.future}} </td>
    <td> {{member.debated}} </td>
    <td> {{member.FIPS140}} </td>
    <td> {{member.CC}} </td>
    <td> {{member.SuiteB}} </td>
    <td> {{member.CSFC}} </td>
    <td> {{member.PCI}} </td>
  </tr>
  {% endfor %}
</table>
