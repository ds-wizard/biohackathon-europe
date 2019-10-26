# DS Wizard for Biohackathon Europe 2019

This [DS Wizard](https://ds-wizard.org) repository contains set-up and related stuff for [Biohackathon Europe 2019](https://www.biohackathon-europe.org)

## Setup local DS Wizard

Requirements: [docker](https://www.docker.com) and [docker-compose](https://docs.docker.com/compose/)

1. Just simply run `docker-compose up -d`
2. Open [http://localhost:8080](http://localhost:8080) in your favorite web-browser.
3. Login as *albert.einstein@example.com* with password *password*.
4. Go to **Knowledge Models** and import them from file(s) that are located in `knowledge-models` folder of this repository
5. Explore DS Wizard and start with hacking!

For more information, visit the [DSW documentation](https://docs.ds-wizard.org).

## How to hack integrations

1. Investigate `dsw:integrations:1.0.0` knowledge model in the DS Wizard:

  - In **Knowledge Models**, view details of the *Integration examples* KM (knowledge model).
  - Press **Create KM Editor** and name your customization of the KM.
  - Using **Preview**, read the descriptions and try out the questions.
  - Back in **Knowledge Model** view, tak a look at integration settings for FAIRsharing, Bio.tools, and TeSS.
  - Then also take a look at the questions inside chapters in the KM.

2. Select some API that you want to integrate and investigate it. The API should provide some search-based listing of items suitable as answer to certain question. Example: [ORCID API](https://orcid.org/organizations/integrators/API) for question to select certain members of a project.
3. Once you know how to work with API to get the list (you can try it out using [curl](https://curl.haxx.se) or [Postman](https://www.getpostman.com)), create a new integration in the KM. Name it appropriately to the integrated service and fill the settings for integration.
4. Create a new chapter named also using name of the integrated service. Then in the **Text** field of the chapter, describe the service and its API integration in detail (similarly to the examples). Use [Markdown](https://www.markdownguide.org/cheat-sheet/) syntax for the description.
5. Create a question in the chapter to demonstrate your API integration and test it out.
6. When you are done, you can release a new version of the KM using **Publish**.

## How to hack templates

1. Prepare a KM for which you want to create a DMP template.
2. Investigate contents of `dmp-templates` folder:

  - `common.json` is the metadata file for *Common DSW Template* and references `common/root.html.j2`.
  - `common/root.html.j2` is the template file for rendering answered questionnaire into a HTML document (that can be then transformed into DOCX, LaTeX, PDF, and other formats). It uses Jinja templating markup, more concretely its implementation [Ginger](https://ginger.tobiasdammers.nl/guide/) for Haskell.
  - `common/root.css` is the cascade stylesheet used in `common/root.html.j2` (using `include` directive).

3. Start a simple template by creating your `<template-name>.json` file that will reference your `<template-name>.html.j2` template, where you can prepare the layout for now.
4. In the DS Wizard, create a questionnaire for your KM and export it. Pick your template, HTML format, and instead of pressing **Download** use right mouse button any copy the link of that button.
5. Open a new tab in the browser and paste the link (should be something like `http://localhost:3000/questionnaires/e99406e2-9116-45f6-93fb-b7668bda4c83/dmp?format=**html**&templateUuid=43a3fdd1-8535-42e0-81a7-5edbff296e65`). Change the format parameter from `html` to `html-preview` (e.g. `http://localhost:3000/questionnaires/e99406e2-9116-45f6-93fb-b7668bda4c83/dmp?format=**html-preview**&templateUuid=43a3fdd1-8535-42e0-81a7-5edbff296e65`) and press Enter.
6. Now you should see the DMP document in the browser instead of downloading it. It is "live" - you can edit your `<template-name>.html.j2` file, save it, refresh the tab in your browser and it will show the new content. You do not have to restart the DSW nor to close the tab.
7. Work iteratively on the template to display what you need. For investigating provided structures, you can print them out into some `<pre>` or take a look in [our documentation](https://docs.ds-wizard.org/en/latest/admin/configuration.html#dmp-templates).

TIP: You can use prepared *Hackathon Explanatory Template* to explore what data are provided to the template. Exploration can be both in the Wizard and also in `dmp-templates/explanatory.html.j2`.

## Possible configurations

You can change the configurations in the `config` folder. For example, you can change the color to your favorite or edit the welcome message/warning.

## License

This project (excluding knowledge models) is licensed under the MIT License - see the [LICENSE](LICENSE) file for more details.
