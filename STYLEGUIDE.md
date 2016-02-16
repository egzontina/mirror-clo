
This style guide is specifically for blog posts on GitLab.com. 

Refer to our [official documentation style guide](http://doc.gitlab.com/ce/development/doc_styleguide.html#documentation-styleguide) which covers formatting. 
Everything included in this guide is an addendum or blog-specific override to that guide. 

Table of contents

- [Markup and formatting](#markup)
- [Person](#person)
- [Formality](#formality)
- [Images](#images)

## <a name="markup"></a>Markup and formatting

See references directly in the documentation style guide. Of particular use.

- [Writing text][doctext]
- [Formatting text][docformatting]
- [Links in text][doclinks]

## <a name="person"></a>Person

Generally in blog posts, it's normal to write from first person singular point of view. 
"I've found" or "I think" are common. 
In tutorials we should use first person plural "we" and second person "you." 

Instead of... 

> In this post I will..  

Use

> In this post we will... 

## <a name="formality"></a>Formality

GitLab tutorial blog posts should be written in a friendly style, but free of 
jargon or memes.
Avoid using cultural idioms and references that could exclude or confluse readers. 

## <a name="images"></a>Images

### Creating images

Static images should be used to illustrate concepts, provide diagrams, elements of the UI or orient the reader.
Images should not be used to render commands or configuration which would prevent
someone being able to copy and paste. 

Animated GIFs can be used sparingly where you need to show a process or some event
happening over the course of time or several actions.
Animated GIFs should not replace text descriptions or instructions. 

### Preparing images

For the blog, images should also be formatted in a 700 x 490 pixel *proportion* 
so the image doesn't get clipped when displayed as a lead image in the blog list.
Compress the image, for example using [TinyPNG.com][tinypng] or any other image editor.

### Where to place images

Images used to illustrate articles should be placed in the /source/images/blogimages directory. 
Unless they are free to use lead images from [Unsplash][unsplash]. 
Those should be placed in the /source/images/unsplash directory.

### Including images in the document

For including the image in the markdown text, refer to "Inside the document"
guidelines in the [Documentation style guide][docimages].

Credit where credit is due: Some of the guidelines are inspired by the 
[Digital Ocean tutorial style guide][dostyleguide].


[unsplash]: https://unsplash.com/
[tinypng]: https://tinypng.com/
[doctext]: http://doc.gitlab.com/ce/development/doc_styleguide.html#text 
[docformatting]: http://doc.gitlab.com/ce/development/doc_styleguide.html#formatting
[doclinks]: http://doc.gitlab.com/ce/development/doc_styleguide.html#links
[docimages]: http://doc.gitlab.com/ce/development/doc_styleguide.html#images
[dostyleguide]: https://www.digitalocean.com/community/tutorials/how-to-write-an-article-for-the-digitalocean-community)