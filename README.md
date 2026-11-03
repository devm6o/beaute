# beauté

A clean, simple Hugo theme for tech blogging. Posts are grouped into sections,
tagged by topic, and searchable from a client-side search page.

Requires Hugo 0.146.0 or later (the standard edition is fine).

## Install

Put the theme in `themes/beaute` and add this to your site's `hugo.toml`:

```toml
theme = 'beaute'

# Hugo does not take these two settings from the theme, so set them in your site.
[outputs]
  home = ['HTML', 'RSS', 'JSON']   # JSON is the search index

[markup.highlight]
  noClasses = false                # code colours come from the theme's CSS
```

## Content

- **Posts** go in a section folder, e.g. `content/linux/my-post.md`. Each
  top-level folder is a section.
- **Special pages** are chosen with `layout` in front matter:

  | Page              | Front matter          |
  | ----------------- | --------------------- |
  | `content/about.md`    | `layout = 'about'`    |
  | `content/search.md`   | `layout = 'search'`   |
  | `content/sections.md` | `layout = 'sections'` |

- Use `description` in front matter for summaries; otherwise the start of the
  post is used.
- Set `contentLang = 'ja'` on a post written in Japanese for better line
  breaking.

## Configuration

```toml
[params]
  description = 'Notes on software, systems, and security.'
  googleFonts = true   # false = system fonts only, no external requests

[params.author]
  name = 'Your Name'
  bio = 'A line about you.'
  avatar = '/images/avatar.jpg'   # file in static/
  [[params.author.links]]
    name = 'GitHub'
    url = 'https://github.com/your-name'
```

The theme adds a main menu (Sections, Tags, About, Search). Define
`[[menus.main]]` in your site to replace it. A menu entry with
`params.icon = 'search'` is shown as a magnifying-glass icon.

## Try it

The theme folder is also a demo site:

```sh
cd themes/beaute
hugo server
```

## License

[MIT](LICENSE). IBM Plex fonts are loaded from Google Fonts under the SIL Open
Font License.
