# ogp-template

An incredibly bare-bones template for opengraph/twitter/facebook sharing niceties. [Slack has an excellent article][slack-article] on the relevant opengraph properties.

## Grid/Canon
I’ve drawn a simple grid to help with laying out elements, and a corresponding layout grid (Toggle its visibility with contrl ⌃ L in Sketch).

## Generating the images
There are slices places on the artboard for Facebook and Twitter share image sizes. Current as of the time of writing:

Facebook: 600 × 315 (1200 × 630 Retina)
Twitter: 560 × 300 (1120 × 600 Retina)

The export slices are set to @2x retina scale, to look nice and sharp on retina devices. You may want to toggle the format between png and jpeg, depending on whether your image contains graphical elements more suited to png compression, or photographic content better suited for jpeg.

## Serving the images
Depending on your criteria, there’s different strategies for serving opengraph images from your views. I use [middleman-ogp][middleman-ogp-link] [on my blog][brett-cool-blog], allowing me to specify the images in my page frontmatter.

```yaml
  ogp:
    og:
      title: 'Page title'
      description: 'Page description'
      image:
        '': http://example.com/path-to-image/og.png
        type: image/jpg
        width: 560
        height: 300
      locale:
        '': en_us
    fb:
      title: 'Page title'
      description: 'Page description'
      image:
        '': http://example.com/path-to-image/fb.png
        type: image/jpg
        width: 600
        height: 315

```

Another option is to serve up

# In `layout.haml`
Check to see if a custom image path for the ogp tag is present.
```haml
  - if @ogp_image_path.present?
    %meta{property:"og:image",       content:"http://example.com/images/#{ogp_image_path/og.png"}
    %meta{property:"fb:image",       content:"http://example.com/images/#{ogp_image_path/fb.png"}
  - else
    # Show the default ogp image.
    %meta{property:"og:image",       content:"http://example.com/images/og.png"}
    %meta{property:"fb:image",       content:"http://example.com/images/fb.png"}
-
```

# In `page.haml`
```haml
  - @ogp_image_path == foo
```


[brett-cool-blog]: http://brett.cool
[slack-article]: https://medium.com/slack-developer-blog/everything-you-ever-wanted-to-know-about-unfurling-but-were-afraid-to-ask-or-how-to-make-your-e64b4bb9254#.39pruiy2j
[middleman-ogp-link]: https://github.com/ngs/middleman-ogp
