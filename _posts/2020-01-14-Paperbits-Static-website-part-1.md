---
toc: true
layout: post
description: 
author: "Sanjeevi Subramani"
categories: [Paperbits]
title: How to use Paperbits Open source Drag and drop Content builder and free static website generator to develop a website and host it in GitHub pages freely — Part I
---

Below things needed for the developer environment.

**Pre requisites:**

* Nodejs

* Visual studio code or any code editor

For hosting we will use **GitHub Pages**, steps at the end of tutorial.

Follow the [getting started tutorial](https://paperbits.io/wiki/getting-started) in the portal important steps added here:

**Run the below commands** in Visual studio code terminal or in cmd line.

 1. Clone the demo project from GitHub:
>  git clone https://github.com/paperbits/paperbits-demo.git

2. Switch into just cloned directory:
>  cd paperbits-demo

3. Install packages required for work:
>  npm install

4. Run demo site:
>  npm start

Now you will be able to see an application running in the localhost port 3000 or other local ports.

5. Now you can drag and drop sections, elements, widget, tiles and design the website easily.

![](https://cdn-images-1.medium.com/max/2058/1*UwlOTV4Y5FvRsiZmQFcgnA.jpeg)

Above image shows the section with background image in editor.

After the design changes click on save button you can see the json file downloaded.

Replace that file contents into the **demo.json** file in the solution folder : **src/data**.

6. Publish modified content
>  npm run publish

If you run this command, it will generate a static website in **./dist/website/ **folder of the project.

Then upload that folder into the GitHub repo you created newly and then in settings of GitHub repo change it to website and point it to master branch.

All these steps are better explained in the following version of this article:

[https://medium.com/lkg-in-it/how-to-use-paperbits-open-source-drag-and-drop-content-builder-and-free-website-generator-to-3f94acd13aef](https://medium.com/lkg-in-it/how-to-use-paperbits-open-source-drag-and-drop-content-builder-and-free-website-generator-to-3f94acd13aef)

That's all now you have created a website for free with free hosting with speed loading from GitHub.

Below is the Paperbits framework portal :

[https://paperbits.io](https://paperbits.io)

GitHub repo: [https://github.com/paperbits](https://github.com/paperbits)
