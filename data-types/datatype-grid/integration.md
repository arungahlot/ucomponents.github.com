---
layout: datatypesubpage
title: Integration
description: DataType Grid is basically a DataType that allows you to store DataTypes in a grid-like fashion. Think Excel, but with other Datatypes instead of textboxes. 
category: DataType Grid
excerpt: How to do advanced stuff with Datatype Grid.
since_version: 3.0
sidebar: <h4>Table of contents</h4>
    <ul>
        <li><a href="../">Usage</a></li>
        <li><a href="../compatible-datatypes">Compatible Datatypes</a></li>
        <li><a href="../localization">Localization</a></li>
        <li><a href="../razor-samples">Razor Samples</a></li>
        <li>Integration</li>
    </ul>
---
### Manipulate data from code ###
<span class="versions">
	<strong>Versions:</strong>
	<span class="badge badge-warning">5.4.2</span>
	<span class="badge badge-warning">5.5.x</span>
</span>

#### Example ####

	// Get reference to content
	var contentService = UmbracoContext.Current.Application.Services.ContentService;
	var content = contentService.GetById(Model.CurrentPage.Id);

	// Get original data
	var data = new GridRowCollection(content.GetValue("dataTypeGrid").ToString());

	// Change data
	foreach (var row in data)
	{
	    var cell = row.GetCell("test");
	    cell.Value = new Random().Next(0, 10).ToString();
	}

	content.SetValue("dataTypeGrid", data.ToString());

	// Save content
	var result = contentService.SaveAndPublish(content);