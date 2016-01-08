# Vision

ALE at its core: create and populate views serverside. This is the single most important thing ALE does.

## Quick recap

ALE is already doing an really awesome job at:
- [x] being all native
 - for the times you are in need of native components
- [x] letting us code less
 - we don't need to parse json to data objects on client
 - we don't need to implement a view controller which populates its views
 - loading of data is implemented once
 - new templates are created once for both android and ios
- [x] presenting content from various data structures easily
 - using handlebars `{{foo.down.there.at[2]}}`

Basically we are able to create populated native views and components directly from server – which is pretty awesome.


## Road ahead – 3 frameworks

We have to be more agnostic to the technology itself and rather use the right tools for the right problem. Often you will find that none of these frameworks alone will meet your needs. In some cases you will find that you will need to use all 3 frameworks.


#### ALE 3.0

Should implement a new architecture which allows for
- better threading
- specify an engine to use for nodelets rendering
- physics on items in a scrollview
- animations on trigger events like "loaded", "visibleFirstTime", etc

What we would like to do:
- move away from json and over to javascript

What we shouldn't do:
- ALE is not HTML, we can not have feature parity with html. Specifally we won't:
 - support text wrapping images


#### WALE (Webview+ALE) 1.0

A webview enriched with ale nodes. The webview will act as a host for all content. The webview may at any time request native to present specific nodes at given coordinates. This way we can leverage all the technology within html and on top of that enrich with gracious native components.


#### IVYControllers 1.0

When tapping on a node or a resource in general we open a controller. Controllers are focused on a single task and they expect data to be delivered in a specific format. If you need full control and want to render and parse data natively then this is the way to go.

The current contract for `controllers` as it is in ivy now should be formalized and refined.

###### Native controller: `ale`

Takes a link to a document. Loads a template found in `_settings.template`. Renders node.

###### Native controller: `pager`

Takes an instance of a flow or cardlist and renders them using integration/html.

###### Native controller: `article`

Takes an article id and renders it using integration/html.

###### Native controller: Homescreen

Takes a link to a json document listing recommended items and tabs to render.
