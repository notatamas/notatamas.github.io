# FOSS IOW GIS

This project is created as an academic assignment for the SDI Module on CU. The website incorporates a number of proprietary and free GIS mapping solutions.

## Approach

The site generation is implemented in <a href="https://jekyllrb.com/">Jekyll</a>. The layout is generated with the <a href="http://shopify.github.io/liquid/">Liquid</a> template language. Hosted on <a href="https://pages.github.com/">Github Pages</a>,
 the layout is based on <a href="http://getbootstrap.com/">Bootstrap</a>
 and <a href="https://jquery.com/">jQuery</a>
 and inspired by the <a href="https://startbootstrap.com/template-overviews/clean-blog/">Clean blog</a> Bootstrap theme by <a href="http://davidmiller.io/">David Miller</a>.</p>

Each map is stored in a Jekyll Collection, therefore the pages presenting the various maps are created using for loops, such as:

```
{% for map in site.maps %}
    {% map.sample_content %}
{% endfor %}
```
The site is created with modular design principles, therefore to avoid repetition, the common elements are included in the following way:
```
{% include secure_warning.html %}
```

The site also makes use of Jekyll variables, and stores them in the config file. Later these variables are used as:

```
{{ site.gm_api_key }}
```
This way the Google maps API key can be referenced from every page of the site.

## Warning
Modern browsers do not allow HTTP requests in sites using HTTPS.
Since Github pages uses HTTPS and the CU server uses HTTP, some requests are blocked.
To overcome this issue, the following approach is suggested:

Start chrome with allowed insecure content:

On \*nix systems:
```
google-chrome --allow-running-insecure-content
```
On Windows:
```
"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --allow-running-insecure-content
```
Please make sure to close every chrome instance before, otherwise chrome will just start a new tab in the current session.

## To examine the code locally:
* Clone or download the repository
* Install Ruby and Jekyll
* Cd into the folder
* Start the server with 'jekyll serve --watch'
* Navigate to 127.0.0.1:4000


## License

MIT license.
