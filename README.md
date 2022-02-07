# <<abbr title="frontend">fe</abbr>/diapos>

Presentations from our Frontend weeklies

The system is thouhgt to focus on the content creation, for which markdown files are used.

## Content creation

1. Create a new markdown file in the `./decks/` folder and name it following the pattern _yyyyMMdd-title.md_
2. Add a [YAML Front matter](https://github.com/webpro/reveal-md#yaml-front-matter) at the beginning from your file
3. `npm run start`

To add local images, media, etc. to your presentation, add them in a folder with the dat of your presentation in `./decks/assets/`.
For instance: given that your presentation md file is for `23.11.2020`, then your local assets should land in `./decks/assets/20201123/`.
Then you can reference your media in your md file like:

```md
![Alt text description](assets/20201123/description.png)
```

Happy writing! 😁

## Tech stack

Behind the scenes, this is a system based on [reveal-md](https://github.com/webpro/reveal-md) and [reveal.js](https://revealjs.com/)

<img src="https://hakim-static.s3.amazonaws.com/reveal-js/logo/v1/reveal-black-text.svg" alt="reveal.js" height="100">

## Next steps

- Setup some hooks to build (`npm run build`) the slides and host them somewhere ⛅️
- Port Unic's PWP styles to <<abbr title="frontend">fe</abbr>/diapos>
