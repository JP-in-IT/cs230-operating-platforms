# cs230-operating-platforms
Software Design Document for The Gaming Room

Client and software requirements:

My client for this project was The Gaming Room, whose game Draw It or Lose It was originally built as an Android-only application. They wanted to expand the game to reach players on desktop browsers (Mac, Linux, and Windows) in addition to iOS and Android, all while keeping game rules and player data consistent across every platform. My job was to design the software architecture that would make that expansion possible, resulting in a full software design document covering requirements, constraints, the domain model, a cross-platform evaluation, and my final recommendations.

What I did particularly well:

I think the strongest part of this document is the domain model and how it ties directly into the recommendations at the end. I built the game engine around a small inheritance hierarchy (Entity as the base class, with Game, Team, and Player extending it) combined with a Singleton pattern for GameService, so every part of the application reads and writes the same list of games rather than risking inconsistent state. That object model gave me a stable foundation to reason about later sections, like why a stateless REST API over HTTPS made sense once I had already committed to a client-server architecture that treats every platform, desktop or mobile, as just another client hitting the same backend.

What was helpful about the design document process:

Working through the Evaluation table for Mac, Linux, Windows, and Mobile Devices across Server Side, Client Side, and Development Tools forced me to justify each recommendation against something concrete rather than just picking a platform because it felt familiar. For example, laying out that macOS is Unix-based and stable but isn’t offered as a hosting platform at scale is a different argument than saying Linux is the standard for hosting a REST API because it’s open source, has a small footprint, and is supported by every major cloud provider. Having to fill in that table row by row is what actually led me to the final recommendation rather than the other way around.

What I would revise:

If I revisited one part of this document, I’d expand the System Architecture View section. I left it as a placeholder note in this version since the assignment didn’t require it, but a logical topology diagram showing how clients, the REST API, and the PostgreSQL database actually connect would make the whole document easier to follow, especially for a development team member who wasn’t there for the design conversations.

Interpreting user needs: 

The core user need here wasn’t really about the game itself, it was about consistency across platforms. The Gaming Room didn’t want five different versions of the game logic maintained separately; they wanted one experience that felt the same whether someone was playing on a Windows browser or an Android phone. That’s why I centered the whole design around a single REST API that every client talks to, instead of letting each platform keep its own copy of the rules. Considering user needs mattered here because a technically sound design that ignored that consistency requirement would have functioned but completely missed what the client actually asked for.

My approach to designing software:

I worked from constraints inward rather than picking a solution first. I started by identifying what changes when you move from a single Android app to a distributed, multi-platform system (network reliability, statelessness, cross-platform compatibility, and data protection in transit), and let those constraints shape the architecture rather than assuming a REST setup from the start. For a similar project going forward, I’d use the same approach: lay out the constraints and requirements first, build the domain model to reflect the object relationships, and only then start filling in an evaluation table to justify infrastructure choices, since jumping straight to a platform recommendation without that groundwork tends to produce decisions that look reasonable but don’t hold up under scrutiny.
