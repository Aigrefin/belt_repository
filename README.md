# belt_repository
This repository is a content manager for the utility belt.

# Mecanism

## What is this place ?
This places plays the role of a [CMS](https://en.wikipedia.org/wiki/Content_management_system), meaning it defines a website content (e.g. the home page of a website).
The [belt_content](https://github.com/Aigrefin/belt_repository/tree/master/belt_content) contains the pages read by the application (i.e. the website). It uses [belt.conf](https://github.com/Aigrefin/belt_repository/blob/master/belt_content/routes.conf) to translate a relative url to the name of a belt file. For example, according to the belt.conf, when the user access http://website/index, the routes parameter tells the application to use the file index.md as the content of this page.
Each file is redacted in markdown file, and is interpreted by the application.

## How to use ?
Right now, you can create two kind of pages : basic pages, and belt pages.
Whatever the kind, these are the two first steps :
* Create your page in [belt_content](https://github.com/Aigrefin/belt_repository/tree/master/belt_content). Name it as you wish, it is not the name that the user of the website will see.
* Create a route for it in [belt.conf](https://github.com/Aigrefin/belt_repository/blob/master/belt_content/belt.conf). Each of theses examples are valid for a file named _test.md_ :
 * test = test.md => http://website/test
 * category/test = test.md => http://website/category/test
 * whatever = test.md => http://website/whatevere

### Basic page
It is uniquely made of markdown. You have no more steps than previously described.
The markdown you type is interpreted by [markdown4j](https://code.google.com/p/markdown4j/#Google_map_address_link) and therefore contains basic markdown features plus the one described by this page.
Once you finish your page, it takes less than a minute to be available on the application.
If you want to see some markdown, the page you're reading right now has been redacted with this syntax.

### Belt page
A belt page is an enhanced page. It is also made of markdown, but another interpreter acts on the content you write.
If you want your page to become a belt page, follow the steps previously described and edit [belt.conf](https://github.com/Aigrefin/belt_repository/blob/master/belt_content/belt.conf) and put the route to you file in the belt-pages list. For example, if your file is test.md, and your path is category/my_test, the belt.conf will look like this :

<pre><code>
  routes {
    category/my_test = test.md
  }
  belt-pages = [
    category/my_test
  ]
</code></pre>

## What's a belt page ?
After being parsed by the application, the belt page will contain an interactive heading (marked as # in markdown), made so that you can filter the direct sub-headings (marked as ## in markdown).
Sub-headings are interactive too ! You can select them : Any selected sub-heading will stay visible if you activate the heading, whereas any non-selected sub-heading will be hidden.
Other features of sub-headings are the ability to expand/collapse them, and to specify a quick description, visible whether is collapsed or not.
### How write one ?
The top of the page can be made of anything and is interpreted as pure markdown, until a # is met. This # will be the main heading, for example :

<pre><code>
  Whatever **you** want
  # heading
</code></pre>

After the heading, anything can be redacted and will be interpreted as pure markdown, until a ## is met. This ## will be a sub-heading, for example :

<pre><code>
  Whatever **you** want
  # heading
  some stuff.
  [github](https://github.com)
  ## sub-heading
</code></pre>

A sub-heading must be follow by a sub-sub-headings named Glimpse. It has to be [list](http://daringfireball.net/projects/markdown/syntax#list). It is interpreted as a quick description that won't be collapsed :

<pre><code>
  Whatever **you** want
  
  # heading
  some stuff.
  [github](https://github.com)
  
  ## sub-heading
  
  ### Glimpse
  * **lenght** : 42
  * **type** : fourth
  * **date** : 27/02/1998
  * **Rating** : 5/5
</code></pre>

After Glimpse, another sub-sub-heading must be added, named Content. It can be anything markdown, but the headings must start from ####. It is interpreted as the content of the sub-heading :

<pre><code>
  Whatever **you** want
  
  # heading
  some stuff.
  [github](https://github.com)
  
  ## sub-heading
  
  ### Glimpse
  * **lenght** : 42
  * **type** : fourth
  * **date** : 27/02/1998
  * **Rating** : 5/5

  ### Content
  This content is only displayed if the user clicks on the sub-heading.
  
  #### a another heading simply interpreted as markdown
  some stuff in it:
  
  * a
  * b
  * c
  
  #### hello
  world
</code></pre>

The example is redacted [here](https://github.com/Aigrefin/belt_repository/blob/master/belt_content/example.md), and has been added to [belt.conf](https://github.com/Aigrefin/belt_repository/blob/master/belt_content/belt.conf).
