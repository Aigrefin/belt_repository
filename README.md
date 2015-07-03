# belt_repository
This repository is a content manager for the utility belt.

# Mecanism

## What I see ?
The [belt_content](https://github.com/Aigrefin/belt_repository/tree/master/belt_content) contains the pages read by the application. It uses [routes.conf](https://github.com/Aigrefin/belt_repository/blob/master/belt_content/routes.conf) to translate a relative url to the name of a belt file.
Each belt file is a markdown file interpreted by the application.

## How to use ?
* Create your page in [belt_content](https://github.com/Aigrefin/belt_repository/tree/master/belt_content)
* Create a route for it in [routes.conf](https://github.com/Aigrefin/belt_repository/blob/master/belt_content/routes.conf)
* Write your page in markdown using features described by [markdown4j](https://code.google.com/p/markdown4j/#Google_map_address_link) and, if you wish, following conventions described below.
* That's it ! Your page will automatically be accessible in less than a minute from the application.

## How to make it work with the application features ?
The application is made to access pieces of information, previously selected, to be accessible immediatly.

It considers every ## as an element that can be selected, and every # as an element that toggles the visibility of its ## children that were not selected.

## Limitations
For the moment you need one and only one # and as many ## following # as you want on each page. All subsections of ## (like ###) are included in ##.
