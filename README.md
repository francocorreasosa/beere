# beere

**beere** is the codename for an idea to organize minimal information we need to organize JS related meetups in Montevideo.

> Why beere? I don't know, got it from a random project name generator because I'm too lazy to think of a name.

## Description

The main idea is to have a website where meetup organizers can post events and optionally attendees can RSVP. Though considering things will be online for some more time this may not be needed at first.

### Technical aspects

This is the simplest part of the idea, we'd have a static site (which in this repo I'll represent with a Next.js app + JSON files) which will be the single source of truth for the events data.
This app would be hosted in GH Pages, Vercel, Netlify or similar platform, free of charge for the community.

### From the point of view of the organizer

Since this website would be completely static and hosted on Github/Vercel/Netlify, there is no servers where organizers can authenticate themselves and there is no gatekeeper to avoid non-organizers posting events. So the idea would be to have text-based files in the Github Repository, where only organizers can push updates. Github's CODEOWNERS feature would be in change of gatekeeping other users from approving PRs to each meetups folders.

### Example

Ignoring the application's core files, the data files would be structured like the following:

```
meetups/
    the-montevideo-js-meetup/
        2021-05-10.md # or .yml, .json, etc...
        2021-06-12.md
        2022-07-19.md
        ...
    react-js-mvd-meetup/
        2021-05-12.md
        2021-06-13.md
        2022-07-20.md
        ...
```

Each file would contain basic information for each event like:

```markdown
---
title: JS Montevideo edición invierno en casa
call_link: https://meet.google.com/nwz-iupo-oyd
rsvp_enabled: true 
start_time: 19:00
end_time: 21:00
---

Se vino el invierno, esta frio, pero nos quedamos en casa tapados con una frazada en el sofá y en lugar de mirar una serie nos miramos un nuevo capitulo de MontevideoJS.

Charlas:
- React Query: Redux is not everything by Nicolás Santos
- ClojureScript by Maurício Eduardo Chicupo Szabo
- Hablemos sin saber: Serverless* moderado por Gabriel Chertok

* La idea de esta sección es hablar entre la gente que asista sobre las tendencias Serverless y como nos ayudan y que problemas nos causan. 

``` 

#### How are we going to keep this secure without bothering maintainers?
 
**Here's an example use case:** Fede and Cherta are the organizers of the MVD JS meetup, hence only they can approve PRs that touch any files inside `meetups/the-montevideo-js-meetup/`, and we can enforce this with a [CODEOWNERS](https://docs.github.com/es/github/creating-cloning-and-archiving-repositories/about-code-owners) file at the root of the repo like the following:

```
/meetups/the-montevideo-js-meetup/*     @fedekau @cherta
```

This same concept would apply for all meetups so only organizers of **that** meetup can approve changes within their folder (and core maintainers of the repo as well).

### From the point of view of the attendee

In the case we don't need RSVPs, the site only acts as read-only and no information from attendees is stored anywhere. Otherwise, we could implement something like Firebase which for our size will be free-forever and just store RSVP information while keeping core event info in the repo.
