# aplayer-hugo-module

A simple hugo module to help you add [Aplayer](https://aplayer.js.org/) in your hugo site with [shortcodes](https://gohugo.io/content-management/shortcodes/).  
[Metingjs](https://github.com/metowolf/MetingJS) is also supported.

## Get Started

Simple installation using hugo cli.

```
hugo mod init github.com/Runzelee/aplayer-hugo-module
```
Check your site config to make sure this module is already in use. The following is an example of yaml, and the same is true for toml and json.
```
module:
  imports:
  - path: github.com/Runzelee/aplayer-hugo-module
```
### Enable HTML Render

Set `unsafe` to true in site config to render the html code. 

```
markup:
    goldmark:
        renderer:
            unsafe: true
```
### Add shortcode in your post
```
{{ < aplayer name="<name>" url="<url>" cover="<cover>" [...] > }}
```
Loading multiple audios to a playlist is also allowed.
```
{{ < aplayer name="<name>,[name],[...]" url="<url>,[url],[...]" cover="<cover>,[cover],[...]" [...] > }}
```
Or use Metingjs to fetch music from server.
```
{{ < meting server="<server>" id="<id>" type="<type>" [...] > }}
```
See [APlayer](https://aplayer.js.org/#/home?id=options) or [Metingjs](https://github.com/metowolf/MetingJS#option) full option docs to use more properties.

Enjoy it!

Notice: Regardless of Metingjs or native Aplayer, all properties with capital letters should be replaced in shortcodes with lowercase and hyphenated. For example, `lrcType` should be replaced with `lrc-type`.

## Advanced options

### Call Aplayer official apis using inner shortcode

You can use Aplayer official apis to change properties, monitor player events, etc. to implememt advanced functions.  

Aplayer instance is ready for you, you don't need to create a new one. Just use the object `ap` directly.

```
{{ < aplayer name="<name>" ... > }}
ap.on('pause', function () {
    console.log('player paused');
});
//ap....
{{ < /aplayer > }}
```
also works with Metingjs
```
{{ < meting server="<server>" ... > }}
// Your code here.
{{ < /meting > }}
```

### Use custom CDN or self-hosted API

You can use a custom CDN or self-hosted API to improve loading speed in your region. Simply add external urls in the site config.
```
aplayer:
    cdn: xxx/aplayer.min.js    
    style_cdn: xxx/aplayer.min.css
    meting_cdn: xxx/Meing.min.js
```
## LICENSE

WTFPL

This module is very simple. There are only two html files with go template syntax, so you can do whatever you want. :D