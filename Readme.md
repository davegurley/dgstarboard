# Starboard documentation template

[Starboard][1] is a tool which creates Trello boards for tracking the various tasks necessary when onboarding, offboarding, or crossboarding employees. We use it extensively within Heroku.

This repository is a template for the guides you'll need to author for using Starboard in your organization.

Fork this repository and add your own onboarding/offboarding/crossboarding guides.

## How do I format content in this repo?

First, you'll need to author your `data.json` file. This manifest is the core of the parser. It provides some required metadata and specifies which teams require which documents.

```JSON
{
  "teams": {
    "id": "Heroku",
    "slug": "heroku-teams",
    "additional_paths": ["", "/extra"],
    "children": [
      {
        "id": "Engineering",
        "slug": "engineering",
        "children": [
          {"id": "Frontend", "slug": "backend"},
          {"id": "Backend", "slug": "backend"}
        ]
      },
      {
        "id": "Marketing",
        "slug": "marketing"
      }
    ]
  },
  "lists_order": ["Pre-Hire", "First Day", "First Week", "First Month"]
}
```
- `Teams` is a tree representing the teams in your company.
  - `id` is actually the name of the team.
  - `slug` the path-safe (lowercase, no spaces) team name. This is used to find the markdown guides for a given team.
  - `additional_paths` is an array of paths to additional documents which will be sourced for this team. If you have guides which are relevant for multiple teams, you can put the common content in a separate file and pull it in using this property.
  - `children` an array of sub-teams.
- `lists_order` Different guides can create and contribute to multiple lists in the new board. Sometimes, the ordering of the list has some semantic value — for example, pre-hire, first day, etc. You can manually specify that ordering using lists_order.

## How is the repository structured? (File Hierarchy)

Onboarding files for a team will be all the files per team up to the root.
So if you are in the team `engineers` you will have the onboarding files of engineers and heroku-teams, as well as any `onboarding.md` files located in directories specified by the `additional_paths` property of any team in the path.

For example, if someone is joining the "engineers" team, we expect to have `/heroku-teams/engineers/onboarding.markdown`, `/heroku-teams/onboarding.markdown`, `/onboarding.markdown` and `/extra/onboarding.markdown`.

If a file is missing, starboard will silently skip it.

## Markdown file format

See the `onboarding.markdown` located in the root directory for an example.

You can target the same trello list from multiple files — for example, different teams might have cards to contribute to the "First Day" list. Take care to use the exact same list name everywhere!

[1]: http://github.com/heroku/starboard