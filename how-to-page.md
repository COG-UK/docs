---
layout: docpost
title: Adding a page to this site
date_published: 2020-03-23 13:45:00 +0000
date_modified:  2020-03-23 13:45:00 +0000
author: samstudio8
maintainer: samstudio8
---

[Fork this repository on Github](http://github.com/cog-UK/docs/), or clone it locally to your system.

Create `<yourpagename>.md` in an appropriate location. You may wish to group some pages by creating a directory for them. You can do all of those from your browser if you wish.

Pages should begin with the following markup:

```
---
layout: docpost
title: <YOUR PAGE TITLE>
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-03-22 21:50:00 +0000
author: <YOUR USERNAME (no special characters)>
maintainer: <YOUR USERNAME (no special characters)>
---
```

The title of the page specified in the `title` field will automatically be added to the page when it is rendered, so there's no need to add the `#` markdown header again.

For instructions on how to use markdown, see [Github's guide on mastering markdown](https://guides.github.com/features/mastering-markdown/).

Once you've finished, use Github to file a pull request against the repository.

Don't forget to edit `index.md` and add the link to your new page. Use the existing links in `index.md` as an example.
