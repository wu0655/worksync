---
title: "Concept"
date: 2022-01-24T16:37:30+08:00
draft: true
---

# flexibility and extensibility
- Extensibility and flexibility are additional characteristics related to maintainability.
    - The level of extensibility reflects how easy it is to extend or enhance the software system. Software systems that are designed to be extensible take future growth into consideration by anticipating the need to add new functionality.
    - Flexibility is similar but mostly focuses on how easy it is to change a capability so that it can be used in a way that wasn't originally designed. Both extensibility and flexibility are characteristics that dictate the level of ease with which someone can perform perfective maintenance.
## Adding new behaviors
If you were to write the beginnings of a bookmarking application—let’s call it Bark, short for BookmARK—you might use a multitier architecture to separate the concerns of persisting, manipulating, and displaying bookmark data. You might build a small set of features on top of those layers of abstraction to make something useful. What happens when you’re ready to add new functionality?

In an ideal extensible system, adding new behavior involves __strictly__ adding new code without changing existing code. Adding new behavior to an extensible system means adding new classes, methods, functions, or data that encapsulate the new behavior (figure1).

## Modifying existing behaviors
You might need to change code you or someone else has already written for a number of reasons. You might need to change the behavior, in the case of fixing a bug or addressing a change in requirements. You might need to refactor the code, keeping the behavior consistent while making the code easier to work with. In these cases, you aren’t necessarily looking to extend the code with new behavior, but the flexibility of the code still plays a big role.

Kent Beck wittily said, “For each desired change, make the change easy (warning: this may be hard), then make the easy change.” Flexibility of code is a measure of its resistance to change. Ideal flexibility means that any piece of your code can be easily swapped out for another implementation. Code that requires shotgun surgery to change is rigid; it fights against change by making you work hard. Breaking down the resistance first—through practices like decomposition, encapsulation, etc.—paves the way to making the specific change you originally intended.

# overhead
![overhead](./img/overhead.svg)

# Safety vs. Security
- Safety means no harm is caused, deliberately or not. Security means that no deliberate harm is caused.
- deliberate 故意的
- [link](https://www.perforce.com/blog/kw/software-safety-vs-security-whats-different)

[Differences Between ‘Security’ and ‘Safety’ from OVA web](https://learningenglish.voanews.com/a/differences-between-security-and-safety-/5791194.html)

- “Security” often has to do with a group’s efforts to protect its members from harm. 
- “Safety” most often relates to a personal feeling of being free from harm or danger. 
- Security seems to define efforts and measures that are outside of an individual, while safety is closer to an inner feeling.

- Here is a simple discussion to show the difference:
    - Did you think about safety when you moved to that neighborhood?
    - Yes, I did. Luckily, there is a security guard at the front door of the apartment.


# Route vs Bridge
- Routing allows multiple networks to communicate independently and yet remain separate, whereas bridging connects two separate networks as if they were a single network.
- In the OSI model, bridging is performed in the data link layer (layer 2)

Bridging is called transparent when the frame format and its addressing aren't changed substantially. Non-transparent bridging is required especially when the frame addressing schemes on both sides of a bridge are not compatible with each other,

