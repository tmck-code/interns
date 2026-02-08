# interns

Resources for interns

- [interns](#interns)
  - [Youtube](#youtube)
  - [Guides \& References](#guides--references)
  - [Rules/"Design Patterns"](#rulesdesign-patterns)
    - [Bad Rules](#bad-rules)
      - ["DRY" - Don't Repeat Yourself](#dry---dont-repeat-yourself)
      - [SOLID Principles](#solid-principles)
      - [Design Patterns](#design-patterns)
      - ["Clean Code" by Robert C. Martin](#clean-code-by-robert-c-martin)
      - ["X" Sucks](#x-sucks)
    - [Good Rules](#good-rules)
  - [Some good quotes](#some-good-quotes)
  - [Recommendations](#recommendations)
  - [Resources](#resources)
    - [Youtube](#youtube-1)

---

## Youtube

| channel                | description                                   | example video                       |
|------------------------|-----------------------------------------------|-------------------------------------|
| [ByteByteGo](https://www.youtube.com/@ByteByteGo) | System Design and Software Engineering       | [APIs in 6 mins](https://www.youtube.com/watch?v=hltLrjabkiY) |
| [Bread on Penguins](https://www.youtube.com/@BreadOnPenguins) | Linux | [My Linux Productivity Workflow](https://www.youtube.com/watch?v=x22k3csfJCo) |
| Brandon Rhodes   | Good basic engineering/dev practices (Python conference talks) | [When Python Practices Go Wrong](https://www.youtube.com/watch?v=S0No2zSJmks) |
| Raymond Hettinger | Python core developer for dict/itertools/more (Python conference talks) | [Modern Dictionaries](https://www.youtube.com/watch?v=p33CVV29OG8) |
| [David Beazely](https://www.youtube.com/@dabeazllc) | Advanced-level lecturer/scientist (Python conference talks) | [The Fun of Reinvention](https://www.youtube.com/watch?v=js_0wjzuMfc) |
| [Kevin Fang](https://www.youtube.com/@kevinfaang/videos) | Incident post-mortem explanations | [SQL Command blowing up 5 billion $$ company](https://www.youtube.com/watch?v=R7VVwfh0Wpo) |
| [You Suck at Programming](https://www.youtube.com/@YouSuckatProgramming/videos) | BASH tutorials | TODO |

## Guides & References

- Git tricks: <https://ohshitgit.com/>
- Python Repo Practices: https://tmck-code.github.io/articles/20260204_python_repo_practices/20260204_python_repo_practices.html

## Rules/"Design Patterns"

### Bad Rules

> [!CAUTION]
> *Don't blindly follow these rules!*

#### "DRY" - Don't Repeat Yourself

> *"Duplication is cheaper than the wrong abstraction"*

Don't paint yourself into a corner by over-engineering abstractions too early, as you're likely to miss a pattern or nuance that only becomes clear over time as you encounter the same problem multiple times, in slightly different ways.

#### SOLID Principles

- `S`ingle Responsibility Principle
- `O`pen/Closed Principle
- `L`iskov Substitution Principle
- `I`nterface Segregation Principle
- `D`ependency Inversion Principle

These rules aim to make code more maintainable, but often lead to
- a massive increase in LOC
- excessive fragmentation of code into tiny classes and interfaces
  - that make your code harder to follow
  - might never be useful in practice

The main rule to keep in mind is "Single Responsibility" - try to ensure that each area of your code is not coupled with others, and does as close to "one thing" as is pragmatic.

#### Design Patterns

These patterns are from the 90s, when languages were very different to the ones we use in the modern age. Many of them were solving problems that no longer exist.

- Gang of Four Design Patterns
  - Singleton, Factory Method, Abstract Factory, Builder, Prototype
  - Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy
  - Chain of Responsibility, Command, Interpreter, Iterator, Mediator, Memento, Observer, State, Strategy, Template Method, Visitor

#### "Clean Code" by Robert C. Martin

See this vid (timstamped) for a great insight into why this approach (and talking about it in general) should be avoided

https://youtu.be/IRTfhkiAqPw?t=1180

#### "X" Sucks

Everything sucks, aka everything in programming has downsides and trade-offs.

Don't blindly subscribe to any particular point of view, and don't feel bad if someone has a strong opinion on something that you do.

Ultimately, the sign of a good developer is to be able to describe which downsides apply in a specific situation and balance all those downsides to suggest a good path forward.

---

### Good Rules

The Zen of Python: https://peps.python.org/pep-0020/

```
In [1]: import this
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.   If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!                                                          
```

## Some good quotes

You have a problem and decide to use regex to solve it. Now you have two problems.   

For those who have a hammer, everything is a nail.   

## Recommendations

| thing         | noob if you use | better if you use      |
|---------------|-----------------|------------------------|
| database      | mysql           | postgres               |
| installation  | anaconda        | uv + docker            |
| linting       | pylint          | ruff                   |
| editor        | sublime         | vscode/vim/jetbrains   |
| config files  | no backups      | your own dotfiles repo |

## Resources

### Youtube

| video | topic |
|---|---|
| <https://www.youtube.com/watch?v=oV9rvDllKEg> | concurrency is not parallelism |
| https://youtu.be/AWVTKBUnoIg | 5 main deployment strategies |

