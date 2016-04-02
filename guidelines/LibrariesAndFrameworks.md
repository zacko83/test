# Libraries and Frameworks

Always strive to use the latest technologies for the features you want to implement. Never stick to an old framework just because you're used to it. Technologies change and improve quickly. Before you start implementing, it's essential to have a plan of the technologies you want to use.

## HDE NuGet Packages

Whenever you develop an application, always ask yourself, what is its core competence? Identify any functionality, that should not be implemented within the realm of the application itself and outsource it to a separate project. Logging is a great example. It's a cross cutting concern, that should definitely not be implemented by each application over and over again. Instead, there must be one project implementing logging for all applications that need it. NuGet offers a great way of [creating packages](../howtos/CreateNugetPackages.md) which can easily be integrated and consumed by any application.

### [HDE.Log4Net](https://hdetfs.visualstudio.com/DefaultCollection/_git/Components?path=%2FHDE.Log4Net%2FReadme.md&version=GBmaster&_a=contents)

### [HDE.Data](https://hdetfs.visualstudio.com/DefaultCollection/_git/Components?path=%2FHDE.Data%2FReadme.md&version=GBmaster&_a=contents)

## Obsolete Frameworks

The list below is by far not complete, it only covers the most important legacy libraries. As a rule of thumb, if a library belongs to the namespace `THOR` it should probably not be used in new projects.

### THOR.Data and THOR.Serialization

The attempt to build our own OR-mapper was replaced by HDE.Data.

### THORGlobal

OK, this one is "just" a class and not really a framework, but it is as mighty as ten. This class knows everything and it can do everything. Therefore it's a perfect example of a [god class](https://en.wikipedia.org/wiki/God_object). Internally it has already been split up into separate components. Unfortunately we still have a myriad of usages within our THOR code. Replace them whenever you can. And never ever, ever, ever, ever, ever, ever, ever, ever, ever, ever create a new instance of it. Doing so is an obvious misconduct, leading to an instant dismissal.

### THOR.Observation

With THOR.Observation we built our own logging framework, which became obsolete since we implemented [HDE.Log4Net](../howtos/HdeLog4Net.md), which utilizes the widely used log4net library. Whenever you need logging, this is the way to go. And whenever you encounter any occurrences of THOR.Observation, replace it with log4net.
