---
toc: true
layout: post
description: 
author: Sanjeevi Subramani
categories: [Paperbits]
title: How to use Paperbits Open source Drag and drop Content builder and free static website generator to develop a website and host it in GitHub pages freely — Part II (Detailed steps)
---

This is a part-II article continuing [this](https://medium.com/lkg-in-it/how-to-use-paperbits-open-source-drag-and-drop-content-builder-and-free-website-generator-to-57408d333118) part-I, Here you will see detailed steps for working in Paperbits framework.

This Paperbits framework is used in Azure API Management Developer portal, so you can use this article to **Customize the Developer portal**.

For exploring this Paperbits framework and also to contribute someone with the website, I have contributed this [Youtube Channel](https://www.youtube.com/channel/UCCgzOyPgoN0Kqnka0BSCM1Q) to have an website developed using Paperbits framework for free as an contribution to education.

You can find that website here: [https://tnpscquickies.com](https://tnpscquickies.com/) which is completely developed by this framework and hosted in GitHub pages freely. Follow this tutorial for the detailed steps for the same.

After following [Part-I article](https://medium.com/lkg-in-it/how-to-use-paperbits-open-source-drag-and-drop-content-builder-and-free-website-generator-to-57408d333118) clone of the Paperbits repo and running the application locally using npm start command a portal will open like the image below at url: [http://localhost:8080/](http://localhost:8080/)

![](https://cdn-images-1.medium.com/max/7400/1*Vs9CC0ujvoG80mj4hRdqtA.png)

In the above image the highlighted ones are the menu to edit the website.

![](https://cdn-images-1.medium.com/max/2038/1*8cvwsGGhODnwsq3QwAvllA.png)

Above image shows the pages menu, where you can add a page or edit a page properties, if we select a page it will show like below menu to edit title and link of the page(URL) and also will show the current page in editor to edit the content.

![](https://cdn-images-1.medium.com/max/3412/1*chUpmbT5tG7B6KgEuxcUPw.png)

Hereafter will use screenshots from the custom site I developed. To add/manage any image click on media menu like below:

![](https://cdn-images-1.medium.com/max/2000/1*YXwRxOHcYWS-bhJKHUa4gQ.png)

Layouts menu is the next one where you can edit the layout which will apply to many pages which will be common — we have Home page layout and other layouts for other pages.

![](https://cdn-images-1.medium.com/max/2000/1*Pch6corKX72zBtFOtAXWqA.png)

Then Navigation menu is used for add/manage the menus.

![](https://cdn-images-1.medium.com/max/2000/1*yhbGPWTxu5yrygYt7Xj6aQ.png)

And in settings you can manage the site header and icon for site.

![](https://cdn-images-1.medium.com/max/2000/1*QO74a3-8Lpc_CfS1Me5fWw.png)

And the last menu is the Styles which is a single place for all the styles of the site which can be configurable like Fonts, Typography, Colors, Gradients, Form Controls, buttons and Cards:

![](https://cdn-images-1.medium.com/max/6888/1*rtN6lzRppYm2SOuBSzAXsQ.png)

![](https://cdn-images-1.medium.com/max/5358/1*ob9psAU_8e85q44kNtUWTA.png)

![](https://cdn-images-1.medium.com/max/3650/1*Kjk_FuzcmnEVId264RokyQ.png)

We can add menu like this:

![](https://cdn-images-1.medium.com/max/5070/1*X9eniHVjYmW5b5u0iNSEEQ.png)

After doing any edit click on save button highlighted below:

![](https://cdn-images-1.medium.com/max/5652/1*yCWrIk190Ew81COKiPiwyQ.png)

Then an json file will download copy the file and replace it in the following file: \src\data\demo.json, now your website will reload or click F5 to refresh the changes.

Editing a Page:

Select a page in pages menu, then you can add a section like on hover of your mouse in center of a section you can see plus sign highlighted in green below for adding section and for editing any section click edit icon highlighted in red below.

![](https://cdn-images-1.medium.com/max/6634/1*lDE6R7TMu4IdlWNRi0MB9g.png)

On click of add section following window will open where you can select section with different type of widgets showing empty widgets.

![](https://cdn-images-1.medium.com/max/2150/1*duGAyOnMg6sIhZGoxrnRZQ.png)

on clicking blocks you will see predefined templates of blocks which can be reused

![](https://cdn-images-1.medium.com/max/2050/1*hPzC1dZ-iwhZYi1e5KJx7Q.png)

To add an block to saved one select any customized blocks like below and click highlighted plus button in yellow

![](https://cdn-images-1.medium.com/max/5704/1*D0w2vJbzeFRjJvvIkSAacw.png)

Give it a name in the window opened

![](https://cdn-images-1.medium.com/max/2000/1*1sRub_vno2Kvy-Pwdyzm-g.png)

Now on adding section you will find that custom block in saved section like below, which you can reuse it:

![](https://cdn-images-1.medium.com/max/2098/1*ld604sAmq1Dzz6BYHiC3xQ.png)

You can edit the background of Section by clicking on edit of section and then selecting background with colors or gradients.

![](https://cdn-images-1.medium.com/max/2000/1*RoQYHVnWj6qySdSNAlVHUw.png)

![](https://cdn-images-1.medium.com/max/2000/1*ocVgzwfShtLfZ9TpJ2BLGQ.png)

![](https://cdn-images-1.medium.com/max/2000/1*iHD05mt13Hkf3YARdXFIyA.png)

I have selected the gradient for overall website here.

You can edit the content of the widget on clicking edit button of an widget

![](https://cdn-images-1.medium.com/max/3742/1*83_dcGUDvneB1XeeKXb7Ew.png)

Similar to adding an section we can add an widget like below plus button which shows on hover of an widget in block, where you can add button, testimonials, menu, card, collapsible panel, search website, Textblock and Forms.

![](https://cdn-images-1.medium.com/max/2168/1*CToqd4bPsWNG_4YswG-pgw.png)

Inside a card we can add picture select it from media library we added in menu or upload new one and adjust properties of it, like below:

![](https://cdn-images-1.medium.com/max/3186/1*9-iI2loyC7kY2gbSnyROIg.png)

Final website is available here:

[https://tnpscquickies.com](https://tnpscquickies.com/)

For your reference I have placed the whole customized website code along with Paperbits source code in the repo:
[**SSanjeevi/Paperbits-Clone-Sample-TNPSCQuickies**
*This repository contains an example of how using Paperbits you can enable advanced content authoring tools in your web…*github.com](https://github.com/SSanjeevi/Paperbits-Clone-Sample-TNPSCQuickies)

Its hosted in the following public repository as GitHub pages:
[**SSanjeevi/BlazorAppClient**
*Contribute to SSanjeevi/BlazorAppClient development by creating an account on GitHub.*github.com](https://github.com/SSanjeevi/BlazorAppClient)

There you can refer i have added the following files in addition to the website files generated from Paperbits framework:

* [nojekyll](https://github.com/SSanjeevi/BlazorAppClient/blob/master/.nojekyll)

* [404.html](https://github.com/SSanjeevi/BlazorAppClient/blob/master/404.html)

* [CNAME](https://github.com/SSanjeevi/BlazorAppClient/blob/master/CNAME)

In order for the custom host website to work.
