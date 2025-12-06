---
date: 2025-12-06
---
# **Project Definition**

The main goal of this project is to be able to create apps quickly via having a pre-built components list that we can `plug-and-play` in our projects instead of building them from scratch (avoid boilerplate). This project will applicable through 3 stages:

- **Stage 1**: Making multiple apps, some personal (startup MVPs apps), some dedicated to selling as a white-label app in different industries. The reason for doing so is to refine the process and make sure it works well and that we have the component list needed.
    
- **Stage 2:** Since we have a ready to use framework with all the necessary components. We can now make apps faster, and we can market that to our clients by having a mobile development agency with the USP of quick app delivery without sacrificing quality or functionality.
    
- **Stage 3:** After we have refined the framework, tested it with real-life scenarios, and made enough money off Stage 2, then we can start selling the framework itself helping agencies build apps quickly either through a one-time payment framework license or subscription-based model (SaaS).
    

This work plan would affect the Distribution and Componentization process. Processes to be defined below:

# **I – Distribution**

If we have a set of components, how are we supposed to use them?

### **1 – Template Engine**

We need a web-interface (or a Desktop App built with Compose Multiplatform). This interface will allow us to create components from text-based templates using `Handlebars` (exists in both JVM and JavaScript frameworks) through the following process:

- Components exist as `.hbs` files
    
- After the user picks the component from a dedicated list, he should fill a form with the necessary information for each field that is part of this specific template. For example, if you want to add a Room Entity, You can pick Room > Entity, then fill in the fields like name, table name, primary keys and field list (each field with its name, type...,etc.).
    
- By clicking create, all the necessary files are generated, ready to download with a text description of what they serve and how to add (a little manual).
    

The Templating Engine can also generate a full project template with all boilerplate code following the same process with the ability to add components directly: User can pick components one by one, and they would be added exactly where they should be following the projects decided on architecture.

This project helps with preparing 70% of the project on the first day without any coding at all where the remaining work can be focused on Business Logic.

> UI Components can also be created using the templating engine, but it is a little bit extreme requiring a dedicated Editor with a drag-and-drop interface (way later)

### **2 – LLM**

It can go through 2 stages, but stage 2 could be a little extreme maybe to consider in the future:

- **Stage 1:** an AI Agent Helper (not Code), that will help fill in the form fields for component templates based on user prompt. To take the example of the Room Entity, the user can explain what the entity does; then the agent will fill the form directly and allow the user to change anything if needed or just accept.
    
- **Stage 2:** an actual AI Agent Coder, where the user just chats with the agent and expects the app to be ready. This is a far future goal as we need to 1 - Be able to make the full app from scratch, which means we should have every possible component ready, then 2 - We have to define the whole CI-CD guaranteeing that the framework also builds and delivers the project as executable ready to publish.
    

> The second stage is not necessary since our main target is to help developers speed up the process of app development. We can touch other markets (Vibe Coders) later.

# **II – Componentization**

A component is any type of code that can be reused. Our goal is not to start from scratch but instead refactor existing refactors based on our philosophy and needs. There are three types of components:

### **1 – Template (file) x Snippet = Templates**

I merged these two because they have the same structure/use case. Both should be created from a template changing only the name and maybe adding some tweaks (Templates initially focused on files while Snippets focused on functions or parts of code). The Tenmplates are basically anything that should be customized by the user.

### **2 – Library**

Contrary to Templates, this is something used as it is. A library that can be added as a dependency and its classes/functions called.

## **How to define components**

Components are defined via an entry file (as of now, the file should be named `README.md` to be properly recognized by GitHub, but the name can change if we have to). Each component should be within a dedicated directory:

- If it is Templates, the directory should have the entry file with the definition of the component and documentations (for usage and others); the template files are `.hbs` well structured within nested folders based on needs; and a `JSON` file describing the Form Structure (to be detailed later)
    
- If it is a Library, the directory should have the entry file and the source code of a typical library (Kotlin/Java or Android).
    

The entry file should have both the definition of the component and documentation for usage and other purposes where the definition should be fully done on properties and the documentation should be done as content in Markdown format. (This content is the one used as documentation when the user generates that component on the Template Engine). The definition should have:

- id: to differentiate components
    
- kompozer: depends, do we need to keep track of who did what?
    
- type: template or library
    
- category: components are organized within folders representing the category, but it should also be declared here
    
- tags: not as necessary but helpful
    
- sources: list of links (from where was this component extracted/inspired for reference)
    
- uses: ids list of other components that are necessary for this component
    
- alternative_for: list of ids, used for in case the user wants something else that does the same job differently
    
- related_to: list of ids, used for related components with similar functionality
    

> About the remaining fields that were defined but removed now:
> 
> - composing/composed_of: would be the same as used, there's no difference between a component composed of other ones or use other ones (uses could be composed_of if the naming is not very descriptive).
>     
> - used_by: could be inferred by looking for all components that use this component.
>     
> - complexity: I don't see any use of it, plus it can be inferred from the uses field (if a component doesn't use any other component, then it is atomic).
>     
> - date: no need for date
>     

The documentation should define how the component is used properly, better be flat with no hierarchy (everything is just a heading and content).

## **How to create components in The Project**

As defined before: we start from Obsidian, creating the entry file, then moving into Android Studio or any other IDE to add Handlebars templates or the library itself. If the component is a library, then its module should be created in Android Studio, then the content of the created folder (usually it is automatically added in `root`) should be moved into the component's directory. After moving files, we should update `settings.gradle` adding this line `project(":component-name").projectDir = file("component-path}")`

# **III – Knowledge Base (Additional)**

This is not necessary, basically a set of overall guidelines and best practices. What we can do is add them separately in a dedicated branch, then each reads the other's knowledge base, or we can have one act as a merger and the other as a reviewer (reviewing the merge). The goal is that our knowledge of the Mobile Development is shared.

> Note: This is not the current `/docs` as it is dedicated to explain the process of components and work. This should be in a different directory that we can call `knowledge/`

---

# **Components List**

The goal was initially to define a list of components, but I would instead define a process since I have noticed that there are three main groups of components:

- **Logic Components**: Covers the architecture, data, network, background, utilities and testing to a certain extent. For example:
    
    - data through `room` and `datastore` both holding data locally
        
    - network pulls data from backend
        
    - background through `workmanager` triggers the pulling of data from the network and caching on local storage
        
    - architecture managing everything through a `repository` and both data and network are considered as `datasources` and it goes vertically until `viewmodels` which provides the data to the UI layer
        
    - dependency injection provides all components to each other
        
    - utilities are used to help with the process: like `results`, `crashes-catching`, `error-handling`...etc.
        
- **UI Components**: covers the second main part of the app showcasing the data.
    
- **Additional Components**: that add extra features to the app like maps, audio and video, camera, sensors, location, permissions...etc.
    

> NOTE: These are groups and not categories, as you can see there are different categories withing the same group

The point here is that it would be better for each one to take care of a specific group itself rather than going with a randomized list of components to help eliminate context switching. Logic Components need to be grouped together (we have multiple categories) while UI Components are technically all grouped in the same category, but there are too many and ambiguous (too many variations) which make the two groups relatively similar in terms of time/energy needed.

Additional Components instead can be split randomly since each one is unrelated to the other.

> Bottom line:
> 
> - One picks UI Components and is responsible for figuring out the list of all possible variations of UI components + Theming techniques to be able to make any type of UI.
>     
> - The other picks Logic Components and is responsible for preparing the architecture that would provide the 70% of the app's logic (Data)
>     

# **Final run-through Process**

Based on this split, each kompozer has a bucket of components that he has to go through one by one; every component should be defined as an issue. Once a component is ready, it is put for review and the reviewer has to review it and validate it if ready. The kompozer never stops unless there is a non-validated issue (he has to fix it first). From a management point of view: The kompozer first checks the issues to be reviewed and the status of their issues, if everything is clear, they can move into actual work/development.

Once the whole bucket is finished. It could be updated adding more components if needed or closed completely, and kompozer has to move to **Additional Components**.

> We should set a soft deadline, once passed no component should be done (especially if Additional), and instead we should prepare for the distribution phase.

## **How should the component be formated for Distribution**?

Components should be formated with `Handlebars` format:

- {{ and }} are placeholders that are filled with data rendered (passed via `JSON` by the user when they fill the form). Everything that is dynamic should be between {{ and }}
    
- Other expressions and forms are used to express conditions, loops, etc. There's a dedicated format for `Handlebars` that should be preferably learned.
    

Components should be initially created normally as `Kotlin` files (or other extensions) but should be refactored on Distribution Phase to the `Handlebars` format.

A form structure file is also defined in the component's directory, which defines what the form will look like and what it should have as fields. In `.hbs` as mentioned earlier, every dynamic part is expressed using placeholder syntax {{ and }}. Within it, it should contain an id used in the passed `JSON` file. That `JSON` file should be generated from the form and that form is defined via the form structure (in other words, the form should be dynamic and changes based on the form structure file).