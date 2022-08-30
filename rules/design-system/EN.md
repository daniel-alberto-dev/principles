# Design system development

> **Important.** These provisions apply to all of our new projects that we write from scratch, as well as existing projects that we redo.

## 1. General Provisions

1.1. We are switching to [Atomic Design](https://atomicdesign.bradfrost.com/chapter-2/) methodology. **Why:** we want to use in all projects a single, understandable for both designers and developers, methodology, and maintain order in our components.

1.2. We use CSS modules. **Why:** they work well out of the box in [CRA](https://create-react-app.dev/) and [next.js](https://nextjs.org/), have isolated namespace, supported by TypeScript, have built-in Autoprefixer, at the output, we have transpiled CSS, i.e. in production, we do not overload the user's browser with redundant computations at runtime.

1.3. For block composition, we follow the [BAM](https://en.bem.info/) rules (where applicable).

1.4. We use a storybook as a documentation system. **Why:** it is an excellent system for documenting components + playground rolled into one.

1.5. When organizing props in the design system, we rely on the props system in the [AntDesign](https://ant.design/components/overview/) components. **Why:** Ant is very well designed, we can safely rely on their experience and not reinvent the wheel.

## 2. Directory structure

at the root - the `designSystem` directory, inside it - the subdirectories:

- **atoms** - if you decompose a page, then an atom is the smallest possible interface element, which is so small that it cannot be broken down into its constituent parts. A required condition is that it **cannot be composed of other atoms**. **Examples:** divider, link, logo, preloader, simple input, simple button

- **molecules** - logically separate elements that are no longer atoms but are not yet organisms. The required condition is that the molecules **do not need to know anything about business logic, the data model in the application, routing, or network requests**. **Examples:** complex input (for example, with an icon), button with a preloader, modal window, upload area, avatar

- **organisms** - complex blocks and various panels, as well as any simple (at first glance) blocks that know about business logic, data model, routing, or network requests. **Examples:** header, navigation block, registration form, social media login button, like button (provided that it serves network requests itself)

- **templates** - page templates, content templates within entities **having their own URL**. **Examples:** template of a page with a login/registration form, a template of an error page (404/500), a template of the main page, a template of a typical modal window with a form (provided that modal windows are opened by URL)

- **pages** - pages and other entities (for example, modal windows), **having their own URL**

- **providers** - various providers. **Examples:** intl provider, redux provider, apollo provider
