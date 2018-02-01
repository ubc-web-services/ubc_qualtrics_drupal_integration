# <div id="top">UBC Qualtrics-Drupal integration</div>
A link to Qualtrics survey for demo: https://ubc.ca1.qualtrics.com/jfe/form/SV_0oiEz2f76DneukR
<br />A link to Drupal website for demo: https://qualtrics.dp7prod.webi.it.ubc.ca/
## Table of Contents:
- Getting started [≫](#getting-started)
- Embedding Qualtrics survey to a website [≫](#embedding-qualtrics-survey)
- How to make an embedded survey responsive [≫](#responsive-survey)
- How to get [anonymous-survey-link] [≫](#anonymous-survey-link)
- Exporting JSON feeds from Drupal to Qualtrics [≫](#exporting-json-feeds)
- For Developers: Guide to Debug [≫](#developers-info)
## <div id="getting-started">Getting started:</div>
To learn more about Drupal, please visit [here](https://drupal.org) for more information.
<br />To learn more about Qualtrics, please visit [here](https://www.qualtrics.com) for more information.

### Required contrib modules:
- Views [≫](https://www.drupal.org/project/views)
- Views Datasource [≫](https://www.drupal.org/project/views_datasource)
- Chaos Tools Suite [≫](https://www.drupal.org/project/ctools)
- CKEditor - WYSIWYG HTML editor [≫](https://www.drupal.org/project/ckeditor)

To download the above contrib modules, here is a [good tutorial](https://www.ostraining.com/blog/drupal/install-modules/) that covers how to install and enable contrib modules in Drupal.

If you are comfortable using Drush, Drupal's command line tool, then you can run the following commands:
```
$ drush -y dl views views_datasource ctools ckeditor
$ drush -y en views views_json views_ui
```

### Required custom modules:
- UBC Qualtrics Drupal Integration
- UBC Qualtrics Static Endpoint

If you are comfortable using Git, you can 
```
$ git clone https://github.com/ubc-web-services/ubc_qualtrics_drupal_integration.git
```
to download files. If not, you can choose to download a .zip file. [Here](https://stackoverflow.com/questions/2751227/how-to-download-source-in-zip-format-from-github/#18583977) is a good reference.

## Settings information in this demo:
- Theme: UBC CLF 7.0.4 Drupal Theme 3.0 [≫](https://github.com/ubc-web-services/Megatron)
- Administration theme: Adminimal - Responsive Administration Theme [≫](https://www.drupal.org/project/adminimal_theme)
- Additional installed modules:
	- Administration menu [≫](https://www.drupal.org/project/admin_menu)

> Note: All screenshots are from Drupal website for demo. If you started your own Drupal website, you can install the modules mentioned above to have the same look and feel of the website we are demonstrating.

## <div id="embedding-qualtrics-survey">Embedding Qualtrics survey to a website:</div>
1. Download Drupal and start building your own Drupal website.
2. Create a basic page:
Go to __Content > Add content > Page__.
Select ![picture alt](screenshots/img15.png) button located at the bottom row of the text editing tools.
In Body field, add:<br />
```html
<iframe align="middle" frameborder="no" height="800px" name="qualtrics" scrolling="auto" src=[anonymous-survey-link] width="800px"></iframe>
```
![picture alt](screenshots/img14.png)
<br />
You can copy and paste the above line, but you __must__ replace the __[anonymous-survey-link]__ with your own.
<br />You can retrieve your own __[anonymous-survey-link]__ with the step-by-step [instruction](#anonymous-survey-link).
<br />In the case of demo, the link is https://ubc.ca1.qualtrics.com/jfe/form/SV_0oiEz2f76DneukR.

3. Save the page to see the survey embedded to the designated page.
## <div id="responsive-survey">How to make an embedded survey responsive:</div>
1. Go to the page on your Drupal website with a Qualtrics survey embedded from the previous step and click __Edit__.
2. In the __Body__ field, add a containing wrapper around `iframe`. You can choose to copy and paste the below example:
```html
<div class="embedded-survey">
	<iframe align="middle" frameborder="no" height="800px" name="qualtrics" scrolling="auto" src=[Anonymous Survey Link] width="800px">
	</iframe>
</div>
```
3. Add the below line of code in your CSS file or wrap around `<style>` tag:
```css
.embedded-survey {
    position: relative;
    padding-bottom: 56.25%;
    padding-top: 35px;
    height: 0;
    overflow: hidden;
}
.embedded-survey iframe {
    position: absolute;
    top:0;
    left: 0;
    width: 100%;
    height: 100%;
}
```
4. Click __Save__.

For more information, visit [here](https://www.smashingmagazine.com/2014/02/making-embedded-content-work-in-responsive-design/).

## <div id="anonymous-survey-link">How to get [anonymous-survey-link]:</div>
1. Go to Qualtrics website and login using your CWL account.
2. Create a survey for demo.
![picture alt](screenshots/img8.png)
For the purpose of demo, I created a survey titled as ___Test: Course Evaluation___.
3. Click the survey title to see the page similar to this:
![picture alt](screenshots/img9.png)
4. Go to __Distribution__ tab located at the top of the page, and the link will be provided when the page is loaded.
![picture alt](screenshots/img10.png)

## <div id="exporting-json-feeds">Exporting JSON feeds from Drupal to Qualtrics:</div>
1. Create a page view:
Go to __Structure > Views > Add new view__ and select __Create a page__. Click __Continue & Edit__.
Under __Format__ field, click __Unformatted list__.
Click __JSON data document__ and click __Apply (all displays)__.
![picture alt](screenshots/img16.png)<br />
2. Once saved, you will be able to see the preview at the bottom of the page that is similar to this:
```
{
  "nodes" : [
    {
      "node" : {
        "title" : "Wood Products Processing"
      }
    },
    {
      "node" : {
        "title" : "Statistics"
      }
    },
    {
      "node" : {
        "title" : "Pharmacy"
      }
    },
...
```
If you click __Settings__ next to JSON data document under __Format__ field, you can modify root object name (___nodes___ in this demo) and top-level child object(___node___ in this demo).<br /><br />
3. Go to Qualtrics website and login using your CWL account.<br /><br />
4. Create a survey, or locate the existing survey that you wish to import JSON feeds from your Drupal website.<br /><br />
5. Create a question of type __Descriptive Text__.<br />
For the purpose of demo, I created a question titled as ___Test drop-down list field___ and ___Test autocomplete field___.<br /><br />
6. Click __Advanced Question Options__ on the left corner of the question card, and click __Add JavaScript__.<br /><br />
![picture alt](screenshots/img21.png)<br /><br />
7. There are __two__ options: to create a drop-down list or an autocomplete text field:<br />
* To create a __drop-down list__, copy and paste the code provided below:<br />
In JavaScript:
```javascript
Qualtrics.SurveyEngine.addOnReady(function () {
	$.getJSON('https://[your-site-domain]/[endpoint-path]', function (data) {
		var nodes = data.nodes;
		var select = document.getElementById('select');
		for (var item of nodes) {
			var temp = document.createElement('option');
			var text = document.createTextNode(item.node.title);
			temp.appendChild(text);
			select.appendChild(temp);
		}
	});
});
```
In jQuery:
```javascript
Qualtrics.SurveyEngine.addOnReady(function () {
	$.getJSON('https://[your-site-domain]/[endpoint-path]', function (data) {
		var nodes = data.nodes;
		for (var node of nodes) {
			$('#select').append('<option value=\"' + node.node.Nid + '\">' + node.node.title + '</option>');
		}
	});
});
```
* To create an __autocomplete text field__, copy and paste the code provided below:<br />
```javascript
Qualtrics.SurveyEngine.addOnReady(function () {
	$.getJSON('https://qualtrics.dp7prod.webi.it.ubc.ca/test-endpoint-program', function (data) {
		var nodes = data.nodes;
		var availableTags = [];
		for (var node of nodes) {
			availableTags.push(node.node.title);
		}
		$("#tags").autocomplete({
			source: availableTags
		});
	});

});
```
> Source: Copyright 2018 The jQuery Foundation. jQuery License

Your __[endpoint-path]__ is the path assigned to your page view

8. Click __save__ button, and find ![picture alt](screenshots/img22.png) button on top of the page.
9. Click and you will see a pop-up window that looks like this:
![picture alt](screenshots/img23.png)
10. Click __Advanced__ option and add below lines to __Header__ section:
```html
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="//code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">
  <link rel="stylesheet" href="/resources/demos/style.css">
  <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
  <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script>
```
11. Click __save__ button, and click your question to edit.
12. Click __Rich Text Editor__.
![picture alt](screenshots/img25.png)
13. Click ![picture alt](screenshots/img26.png) button.
14. For __Drop-down list__, copy and paste below line:
```html
<select id="select"></select>
```
15. For __Autocomplete text field__, copy and paste below line:
```html
<div class="ui-widget"><label for="tags">Enter: </label> <input id="tags" /></div>
```
16. Click __Save__ button, and click ![picture alt](screenshots/img24.png) to have a preview look of your survey.

## <div id="developers-info">For Developers: Guide to Debug</div>
### If questions are not displayed properly or failed to retrieve JSON feeds from Qualtrics side:
There is a quick way to check whether Qualtrics Drupal Integration module has been set up properly in __Firefox__.<br />
1. Go to your website and locate the page view with the JSON feeds you wish to export.
2. At the top of the browser, there are three tabs: __JSON, Raw Data, and Headers__. If you click __Headers__, you should see Access-Control-Allow-Origin header similar to this:

![picture alt](screenshots/img28.png)

under __Response Headers__.
3. If not, you would want to go back to your Drupal website and see if the __module has been installed and enabled__, and make sure that __all the caches are cleared__.

### When adding custom CSS or JavaScript files in Drupal
By default, Drupal automatically optimizes external resources to reduce both the size and number of requests made to your website.
Hence, you want to make sure that these options are disabled in order to properly load your custom CSS and JavaScript files:
1. Go to __Configuration > Development > Performance__ or simply __admin/config/development/performance__.
2. Under __Bandwidth Optimization__, disable all three options: Compress cached pages, Aggregate and compress CSS files, and Aggregate JavaScript files.
![picture alt](screenshots/img27.png)
3. Click __Save Configuration__.

Back to Top [__≫__](#top)
