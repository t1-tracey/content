---
title: Graphic design for responsive sites
slug: Web/Progressive_web_apps/Responsive/Graphics_for_responsive_sites
---

In 1996, many people involved in building the Web would have laughed at you if you had told them that less than 20 years in the future we would be developing websites that worked well on mobile phones, tablets, TVs, even cars and home lighting. But today it is very much a reality. This article provides a high level discussion aimed at helping you to choose the best option for your graphical needs.

Textual content is not a problem, as text boxes are innately responsive, but the picture starts to get ugly when you start including graphics and complex layouts on your pages — especially when those graphics and layouts need to adapt to different displays! This is why we have included an entire docs section covering each of these topics (the one you are currently in, and [app layout](/en-US/docs/Web/Apps/app_layout).)

In addition, these days there are so many more technologies to choose from than your humble BMPs, JPGs, GIFs and PNGs. But what should you choose? This really depends on what target devices you have to support, how complex the graphics need to be, and how much interactivity your graphics require.

## Serving images selectively via CSS

In general, you will use mostly the same graphical assets for different layouts in a responsive design, but you may well include slightly different ones dependent on context. For example, if your desktop layout includes a large header graphic and several programmatic graphics (e.g. CSS drop shadows and gradients), you may want to simplify or remove certain assets for the site's mobile layout, or even provide smaller assets to suit the smaller screen better. This is because in general mobile devices will have less processing power and bandwidth available, so you want to reduce the processing and downloads. In addition, mobile devices have smaller screen sizes, so it makes sense to reduce visual clutter on a mobile layout.

[CSS media queries](/en-US/docs/Web/CSS/Media_Queries/Using_media_queries) allow us to serve different CSS rules dependent on viewport dimensions, and you should consider using [mobile first media queries](https://www.peachpit.com/articles/article.aspx?p=1960918) where possible. This means that the default layout before any media queries are encountered in the CSS is the small screen/mobile layout, not the wide screen/desktop layout. So when the page is loaded on a mobile device, the mobile will only download the mobile assets, and not the desktop resource assets.

While the pixel size of an image resource doesn't change, there are a few ways to make [HTML `<img>`s](/en-US/docs/Web/HTML/Element/img)responsive. Setting `max-width: 100%` on an image allows the image to render at its normal size when space allows, without causing pixelation, while ensuring the image never exceeds the width of its parent container. Different image files can be served depending on viewport size using the [`srcset`](/en-US/docs/Web/HTML/Element/img#srcset) and [`sizes`](/en-US/docs/Web/HTML/Element/img#sizes) attributes. The {{HTMLElement('picture')}} element can contain multiple {{HTMLElement('source')}} elements and one `<img>` element to offer alternative versions of an image for different display/device scenarios. Always make sure your images include alternative text by including an [`alt`](/en-US/docs/Web/HTML/Element/img#attr-alt) attribute.

## Coping with different resolutions

In this section we'll review different strategies for dealing with getting images to work across devices with different screen resolutions. The issue here is that raster images, when rendered on high res devices, are in danger of appearing tiny because the same number of pixels is being shown in a much smaller screen space. Most hi res devices apply a default zoom factor to the whole web page so that the content is a bit more legible, but the downside of this is that the images in question start to look pixelated and ugly because they have been zoomed in.

- high res and low res image copies
  - : One option here is to create a hi res and a low res set of images, then use [resolution media queries](/en-US/docs/Web/CSS/resolution) to serve the hi res images only to hi res devices.
- Programmatic images
  - : You should also try to use programmatic/vector graphics as much as possible, as they theoretically scale infinitely so will still look crisp at high resolutions. You could use CSS properties for generating effects like [drop shadows](/en-US/docs/Web/CSS/box-shadow), [gradients](/en-US/docs/Web/CSS/CSS_Images/Using_CSS_gradients) and [rounded corners](/en-US/docs/Web/CSS/border-radius), and you could also consider using [SVG](/en-US/docs/Web/SVG) for other UI elements, instead of raster graphics formats. Raster images within SVG files do have the same issues as other image types.
- Using fonts for icons
  - : Another technique is [web fonts](/en-US/docs/Web/CSS/@font-face) for icons. Text is infinitely scalable on the web, and you can also use CSS text properties to style your web font icons, such as [`text-shadow`](/en-US/docs/Web/CSS/text-shadow) and [`color`](/en-US/docs/Web/Guide/CSS/Getting_started/Color). Unfortunately, icon fonts are not by default accessible. If the user uses their own font, such as with the Dyslexia extension, your icons may not show. Additionally, every icon needs to be nested in an element that provides it with an accessible name, such as with [`aria-label`](/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-label).

## Interactive images

If your images need to feature some level of interactivity, such as links, other clickable areas, or animation, there are a number of options available.

- CSS
  - : As well as adding programmatic graphical effects to links (and anywhere else you might want them), CSS also allows you to write declarative [animations](/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations) and [transitions](/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions).
- JavaScript
  - : [JavaScript](/en-US/docs/Web/JavaScript) has functions that enable developers to create effects based on interactions. It is very powerful when combined with other technologies, although its complexity is a barrier for non-developers.
- SVG
  - : [SVG](/en-US/docs/Web/SVG), just like [HTML](/en-US/docs/Web/HTML)/[CSS](/en-US/docs/Web/CSS\), can be manipulated with CSS and via JavaScript. So adding interactivity is not difficult. You can also add links directly into SVG and can create animations using [SMIL](/en-US/docs/Web/SVG/SVG_animation_with_SMIL) (Synchronized Multimedia Integration Language).
- WebGL/Canvas

  - : You can create a canvas to draw interactive graphics on using the HTML {{HTMLElement('canvas')}} element, then use the Canvas API to create shapes, lines, import image files, create text, do compositing operations, and much more. Standard JavaScript can then be used to animate the image output, etc. You can create 2D imagery using the regular 2D canvas context, or 3D imagery using the more nascent [WebGL API](/en-US/docs/Web/API/WebGL_API).

    Canvas is very powerful, but it needs to be used with caution. It is good for the visuals of games and complex data visualizations, but for standard user interface elements it is not very efficient and completely inaccessible to screen reader users. Canvases are just raster images, so the text created inside them is not accessible. Also, they don't scale well.
