                                <section class="normal markdown-section">
                                
                                <h1 id="abstract">Abstract</h1>
<p>In this chapter, we will analyze and discuss the architecture of Node.js: an event-driven sever-side JavaScript environment. Several aspects of Node.js are analyzed, starting with the stakeholders. We give a context view to describe the different components involved and a development view to outline how Node.js is developed and the ways in which contributions can be made. We discuss the functional view, which provides the functionalities and evolution of Node.js. Lastly, we discuss Node.js from a scalability and performance perspective. We end with a short conclusion summarizing our most interesting findings regarding Node.js&apos; architecture.</p>
<h1 id="table-of-contents">Table of Contents</h1>
<ol>
<li><a href="#section-introduction">Introduction</a></li>
<li><a href="#section-stakeholder-view">Stakeholder View</a></li>
<li><a href="#section-context-view">Context View</a></li>
<li><a href="#section-development-view">Development View</a></li>
<li><a href="#section-functional-view">Functional View</a></li>
<li><a href="#section-performance-perspective">Scalability &amp; Performance Perspective</a></li>
<li><a href="#section-conclusion">Conclusion</a></li>
</ol>
<div id="section-introduction">

<h1 id="introduction">Introduction</h1>
<p>Node.js is an open-source tool for developing a wide array of server applications. Development started back in 2009, led by developer Ryan Dahl [<a href="#rdquote">1</a>]. Initially Node.js only supported Mac OS X and Linux, but later in 2011 the project was expanded to also support Windows and other lesser known operating systems. </p>
<p>The reason why Node.js was originally started is because Ryan Dahl was fed up with the disconnect between the client and the web server. Each time the client wanted to be updated with new information it had to query the web server (for example, to keep track of progress of a file upload). This had been a long-standing problem in the field of web development, but most developers just decided to deal with it. Node.js was the first real attempt at solving this problem at the root by enabling real-time communication between the client and the server. It was immediately well received, as shown by the enthusiastic reaction of the audience during the original Node.js launch presentation [<a href="#rdvideo">2</a>].</p>
<p>Since its inception, Node.js has surpassed many of its early expectations [<a href="#nodestats">3</a>]. The total amount of active contributors to the project itself increased each year to a record amount of about 480 contributors at the end of 2016. The number of downloads also continues to grow, with the total amount of downloads averaging at over 480,000 a day.</p>
<p>Because of the immense popularity of Node.js we wanted to study its architecture and how it is used to achieve some of the unique functionalities Node.js has to offer. We will first discuss the <a href="#section-stakeholder-view">Stakeholders</a> and the <a href="#section-context-view">Context View</a> to get an idea of who and what is involved in the development, usage and maintenance of Node.js. Afterwards we will analyze Node.js from a <a href="#section-development-view">development viewpoint</a> where we will talk more about the technical structure of Node.js and the design guidelines and patterns used by Node.js. Then we will highlight some of the most unique and distinctive functionalities that Node.js has to offer in the <a href="#section-functional-view">Functional View</a>. Through this we hope to explain what made Node.js so unique and successful. Finally we will describe how the architecture of Node.js manages to serve such a wide userbase by considering the <a href="#section-performance-perspective">performance and scalability</a>.</p>
<div id="section-stakeholder-view">

<h1 id="stakeholder-view">Stakeholder View</h1>
<p>This section discusses various stakeholders involved in Node.js and provides a classification of the stakeholders as proposed by Rozanski and Woods [<a href="#rw">4</a>]. Node.js is owned and governed by the <a href="https://nodejs.org/en/foundation/" title="Node.js Foundation&apos;s Homepage" target="_blank">Node.js Foundation</a> which consists of the following stakeholders:</p>
<ol>
<li>Board: Sets the business direction and oversees legal, financial and marketing domains.</li>
<li>Technical Steering Committee (TSC): Sets the technical direction and is responsible for technical governance of all Node.js projects including Node.js Core.</li>
<li>Foundation Members: They can be businesses or individuals. Both types of members have representation on the board.</li>
<li>Core Technical Committee: The Foundation sponsors the Node.js Core project and entrusts its governance to the Core Technical Committee (CTC).</li>
<li>Collaborators: The Collaborators along with the CTC maintain the nodejs/node GitHub repository. The collaborators are primarily involved in development, maintenance and testing of Node.js. Collaborators are organized into various Working Groups (WG) which have specific areas of responsibility such as testing, build, documentation and so on.</li>
</ol>
<p><a href="#stakeholder_view">Figure 1</a> provides an overview of Node.js stakeholders.</p>
<div id="stakeholder_view">

<p><img src="images-node/stakeholder_view.png" alt="" title="Figure 1: Stakeholder View"><br>
<em>Figure 1: Stakeholder View</em></p>
<p>In order to provide a more precise and fine-grained view of the roles of the stakeholders, we provide a classification of stakeholders according to Rozanski and Woods [<a href="#rw">4</a>].</p>
<table>
<thead>
<tr>
<th>Type</th>
<th>Stakeholders</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Developers</td>
<td>Core Technical Committee (CTC), Collaborators, Any developers on GitHub</td>
<td>CTC and Collaborators are actively involved in the development, maintenance and documentation of the project. They are also responsible for reviewing issues and merging pull requests from other Collaborators and GitHub users.</td>
</tr>
<tr>
<td>Acquirers</td>
<td>Node.js Foundation</td>
<td>The Foundation decides the business and technical direction of Node.js and is responsible for governance,  marketing and sales.</td>
</tr>
<tr>
<td>Assessors</td>
<td>Testing Working Group (WG), Benchmarking WG</td>
<td>They test the quality and compliance of Node.js.</td>
</tr>
<tr>
<td>Communicators</td>
<td>Website WG, Documentation WG, Evangelism WG, Foundation&#x2019;s Education Committee</td>
<td>The Website WG maintains the node.org website. Documentation WG is involved in documentation of APIs and the website. Evangelism WG promotes community events and manages social media content. The Education Committee helps users explore and learn Node.js.</td>
</tr>
<tr>
<td>Maintainers</td>
<td>Developers</td>
<td>Core Technical Committee makes decisions on the evolution of the project and the Collaborators are responsible for all maintenance tasks.</td>
</tr>
<tr>
<td>Support Staff</td>
<td>Collaborators</td>
<td>Collaborators provide support for the development of Node.js by helping users and novice contributors.</td>
</tr>
<tr>
<td>System Administrators</td>
<td>Collaborators</td>
<td>Collaborators also assume the role of system administrators.</td>
</tr>
<tr>
<td>Suppliers</td>
<td>Windows, Mac, Linux, SunOS and Docker</td>
<td>These stakeholders supply hardware and software that the system runs on.</td>
</tr>
</tbody>
</table>
<p>We have analyzed some of the latest <a href="https://github.com/nodejs/node/pulls" target="_blank">pull requests</a> and <a href="https://github.com/nodejs/node/issues" target="_blank">issues</a> to identify how the stakeholders collaborate to develop the system and make decisions. Node.js&apos; governance policy suggests that collaborators are responsible for reviewing each other&apos;s pull requests and must include the CTC (by labelling it ctc-review) if there is disagreement among the collaborators regarding the proposed change. However, we observed in the last 25 pull requests that at least one member of the CTC was included as a reviewer even if the item was not labelled as ctc-review. This suggests that the CTC are the main integrators of the project. Their focus is to ensure that the commits are of high quality. Also, we observed that pull requests labelled &quot;test&quot; or &quot;build&quot; generally involve a member of the relevant working group.</p>
<p><a href="#stakeholder_powergrid">Figure 2</a> provides the power grid view of Node.js stakeholders. It is used to classify the stakeholders based on their interest in the system and their power to influence the development of the system. Such a classification can help identify the stakeholders that have the highest influence on the system so that their interests may be prioritized.</p>
<div id="stakeholder_powergrid">

<p><img src="images-node/PI_Grid.png" alt="" title="Figure 2: Stakeholders power grid view"><br>
<em>Figure 2: Stakeholder power grid view</em></p>
<h2 id="high-power-high-interest-manage-closely">High power high interest: Manage closely</h2>
<p>These are stakeholders that are responsible for building and maintaining Node.js. It includes the Node.js Foundation and project team which are responsible for deciding the technical direction, development and maintenance of Node.js</p>
<h2 id="low-power-high-interest-keep-informed">Low power high interest: Keep informed</h2>
<p>These are stakeholders who do not have much power in influencing the development of Node.js but have high interest in the system. It includes third-party developers that build Node.js packages and companies that build IDEs for Node.js. It also includes competitors of Node.js such as PHP, Golang, Reactor project and so on who have high interest in how Node.js evolves.</p>
<h2 id="high-power-low-interest-keep-satisfied">High power low interest: Keep Satisfied</h2>
<p>This includes businesses who build applications using Node.js. Clients that are members of Node.js Foundation have the power to influence the evolution and technical direction of Node.js.</p>
<h2 id="low-power-low-interest-monitor">Low power low interest: Monitor</h2>
<p>This category includes stakeholders that do not have any power or interest in Node.js but provide services that are used in the development of the system. This includes services like GitHub for source control, Jenkins for Continuous Integration. It also includes individual developers who build applications using Node.js.</p>
<div id="section-context-view">

<h1 id="context-view">Context View</h1>
<p>In this section we will discuss all external entities that Node.js interacts with and the context in which they interact with each other. Through this analysis we aim to get an overview of the ecosystem in which Node.js resides through which we can identify dependencies and end users of interest. </p>
<h2 id="system-scope-and-responsibilities">System scope and responsibilities</h2>
<p>According to <a href="https://nodejs.org/en/about/" target="_blank">their own website</a>, Node.js was designed to build scalable network applications. Node.js is mainly meant to provide developers with the foundations for common server-side functionalities, for example [<a href="#archint">5</a>]:</p>
<ul>
<li>Binary data manipulation</li>
<li>File system I/O operations</li>
<li>Database access</li>
<li>Computer networking</li>
</ul>
<p>Node.js is very lightweight and many higher-level functionalities are intentionally relegated to the many packages that are offered through its package ecosystem (called npm), which provides access to the world&apos;s largest collection of open source libraries and frameworks.</p>
<h2 id="external-entities">External entities</h2>
<p>We have grouped all the external entities that are related to Node.js into several categories which we discuss sequentially below. An overview of all the entities and their relations to Node.js can be found in <a href="#context_view_graph">Figure 3</a>. </p>
<div id="context_view_graph">

<p><img src="images-node/context_view.png" alt="" title="Figure 3: Context View"> <br>
<em>Figure 3: Context View</em></p>
<h3 id="development">Development</h3>
<p>These are different entities that are related to the actual development of Node.js, such as programming languages and testing.</p>
<p><strong>Programming languages</strong></p>
<p>Node.js is almost entirely written in JavaScript. It uses Google&apos;s V8 engine to execute all the JavaScript code, but since this engine is itself written in C++, some parts of Node.js&apos;s codebase that interact directly with this engine are also written in C++. Finally, Python is used to run many of the automated tests for Node.js.</p>
<p><strong>Dependencies</strong></p>
<p>There are a number of libraries or products that Node.js explicitly depends upon. Since Node.js was meant to be lightweight it offers only the most basic necessities for a product of its kind out of the box and thus, it does not have too many dependencies. Instead, it relies on the wide variety of additional plugins and libraries offered through npm, which can be used to extend the functionality of a Node.js application with many standardized solutions to common problems.</p>
<ul>
<li><a href="https://github.com/libuv/libuv" target="_blank">libuv</a>: Node.js is asynchronous and libuv provides a consistent interface for common asynchronous tasks across all supported platforms.</li>
<li><a href="https://github.com/c-ares/c-ares" target="_blank">c-ares</a>: a library for asynchronous DNS requests.</li>
<li><a href="https://github.com/openssl/openssl" target="_blank">openssl</a>: a library of cryptographic functions for security purposes.</li>
<li><a href="https://github.com/nodejs/http-parser" target="_blank">http parser</a>: parses HTTP requests and responses.</li>
<li><a href="https://v8docs.nodesource.com/" target="_blank">v8</a>: the Javascript engine used by Node.js to run all of its JavaScript code.</li>
<li><a href="https://github.com/madler/zlib" target="_blank">zlib</a>: a library used for (de)compression.</li>
</ul>
<p><strong>Tools</strong></p>
<p>In addition to the dependencies mentioned above, Node.js makes use of a couple of additional tools. These are not dependencies in the sense that Node.js cannot work without them, but can be thought of as additional features that enrich the Node.js experience.</p>
<ul>
<li><a href="https://docs.npmjs.com/" target="_blank">npm</a>: the package manager of Node.js that offers access to a multitude of open source libraries.</li>
<li><a href="https://github.com/nodejs/node-gyp" target="_blank">gyp</a>: a build system to build those parts of Node.js and its dependencies that require compilation.</li>
<li><a href="https://github.com/google/googletest" target="_blank">gtest</a>: a unit testing suite for C and C++ code.</li>
</ul>
<p><strong>Testing</strong></p>
<p>As we previously mentioned while discussing the dependencies, gtest is used for C++ related tests. For the JavaScript code, the Python library pytest is used to configure and run the tests.</p>
<p><strong>Distribution</strong></p>
<p>Node.js is available on Windows, Mac, Linux, SunOS and Docker. It can be downloaded directly from <a href="https://nodejs.org/en/download/" target="_blank">their own website</a> or through one of many third party <a href="https://nodejs.org/en/download/package-manager/" target="_blank">package managers</a> that offer it. Those packagers are responsible for packaging the Node.js code base themselves, so Node.js stresses that any issues people run into should be reported to them. If it turns out to be an issue with Node.js itself, those packagers will contact Node.js to notify them accordingly.</p>
<p><strong>Competitors</strong></p>
<p>Node.js is of course not the only platform that provides server-side functionalities. The following is a list of competitors that provide in some way the same functionalities that Node.js provides:</p>
<ul>
<li><a href="http://php.net/" target="_blank">PHP</a></li>
<li><a href="https://golang.org/" target="_blank">Golang</a></li>
<li><a href="http://vertx.io/" target="_blank">Vert.x</a></li>
<li><a href="http://projectreactor.io/" target="_blank">Reactor project</a></li>
<li><a href="https://celluloid.io/" target="_blank">Celluloid-io</a></li>
<li><a href="http://reactphp.org/" target="_blank">Reactphp</a></li>
<li><a href="http://cyclone.io/" target="_blank">Cyclone.io</a></li>
</ul>
<h3 id="users">Users</h3>
<p>The users of Node.js can be divided into two subcategories. The individual community and enterprise.</p>
<p><strong>Individual community</strong></p>
<p>The individual community are the types of users that uses Node.js as hobby or for research. They do not intend to make money by using Node.js. Such users are developers and universities.</p>
<p><strong>Enterprise</strong></p>
<p>Enterprise are the users who do use Node.js as a tool in their company to help improve their product. Some major companies that use Node.js commercially are [<a href="#enterprise">6</a>]:</p>
<ul>
<li>Netflix</li>
<li>PayPal</li>
<li>Uber</li>
<li>IBM</li>
<li>Microsoft</li>
</ul>
<h3 id="feedback--developers">Feedback &amp; Developers</h3>
<p>For real-time discussion about Node.js development there is the #node.js IRC channel on the irc.freenode.net server. For general communication to all people working <em>with</em> Node.js and not just <em>on</em> Node.js, they also have a number of communication channels:</p>
<ul>
<li>The official <a href="https://twitter.com/nodejs" target="_blank">Node Twitter account</a> through which they keep their followers up to date. </li>
<li>A weekly mailing list called Node Weekly, detailing the latest events within the Node.js community. </li>
<li>NodeUp, a podcast that covers the latest Node.js-related news.</li>
</ul>
<p>Feedback and help can be found on various platforms such as StackOverflow, GitHub and Google Groups, with all three platforms having an active community for Node.js.  </p>
<p><strong>Version control &amp; Issue tracking</strong></p>
<p>Node.js is actively being developed on <a href="https://github.com/" target="_blank">GitHub</a> using Git as its version control system. The same system is also used to track issues, report bugs and discuss features.</p>
<p><strong>License</strong></p>
<p>The <a href="https://github.com/nodejs/node/blob/master/LICENSE" target="_blank">Node license</a> closely follows the <a href="https://opensource.org/licenses/mit-license.php" target="_blank">MIT license</a>.
<br><br></p>
<div id="section-development-view">

<h1 id="development-view">Development View</h1>
<p>The Development View details how the architecture supports the software development process and which development guidelines are to be taken into account by all developers. Development views communicate the aspects of the architecture of interest to those stakeholders involved in building, testing, maintaining, and enhancing the system.</p>
<h2 id="module-organization">Module Organization</h2>
<p>Node.js is both a product of its own as well as a service upon which other applications can be built. Because of this, it is useful to consider the design choices made for both in our analysis. Some of the choices made at a basic level in the Node.js architecture affect how applications using Node.js should be developed. <a href="#module_organization">Figure 4</a> shows a diagram depicting the high-level layered structure of Node.js as described in [<a href="#mo">7</a>].</p>
<div id="module_organization">

<p><img src="images-node/module_organization.jpg" alt="" title="Figure 4: Module Organization"> <br>
<em>Figure 4: Module Organization</em></p>
<p>The Module and Application Ecosystem refers to the collection of all software that was built using Node.js. It is connected to all other layers in the diagram, which signifies that in theory developers of Node.js applications are free to connect to any of Node.js&apos; layers. In practice most applications limit themselves to accessing only the Node.js Core Library.</p>
<p>This Core Library contains a variety of JavaScript files that simplify the development process for Node.js users. It offers a lot of common functionality out of the box, such as cryptography, network connections, event handling, etc. A part of the code in this library is marked as &quot;internal&quot;, which hides a part of the API from the end user. The end user can still call these API functions if they wanted to, but since the format of these APIs can change without notice, they are marked as internal to discourage people from doing so.</p>
<p>The Application Binary Interface (commonly referred to as the ABI) is a relatively new part of Node.js [<a href="#abi">8</a>]. The idea behind the ABI is to provide the end user with a stable API through which they can access the underlying JavaScript engine. At this point that engine is Google&apos;s V8, but the ABI allows Node.js to potentially switch to a different engine in the future. Also the ABI ensures that no new version of Node.js is required if changes are made to Google&apos;s V8 engine. The Binary Abstraction Layer serves a similar purpose, but it abstracts the ABI even further. On top of that, it also provides abstracted access to other dependencies aside from the JavaScript engine.</p>
<h1 id="design-patterns">Design Patterns</h1>
<p>This section discusses some of the design patterns used in Node.js.</p>
<h3 id="singleton-pattern">Singleton Pattern</h3>
<p>The singleton pattern limits the number of instances of a particular object to just one. Node.js uses module caching to implement the Singleton pattern and caches a module after the first time it is loaded. Every subsequent call to a module using <code>require(&lt;module_name&gt;)</code> returns the same instance of the cached module. In that way, these modules can thus be thought of as singletons.</p>
<h3 id="dependency-injection-container">Dependency Injection Container</h3>
<p>Application modules built on Node.js typically use a backbone object that acts as a dependency injection container. Services such as logging and database access which are required throughout almost any application built on Node.js are attached to the backbone object and this object in turn can be used by the modules that require these services. In this way, modules have their dependencies injected from the outside through the use of the backbone object. The module is thus isolated from any changes in its dependencies.</p>
<h3 id="event-driven-programming">Event-Driven Programming</h3>
<p>In an event-driven program the flow of the application is the result of events that are fired or states that are changed. In general there is one single, global mechanism that listens for such events and whenever one is fired it will call the corresponding callback function. In Node.js this mechanism is called the Event Loop, which we will discuss in great detail in the <a href="#section-functional-view">Functional View</a> and the <a href="#section-performance-perspective">Performance and Scalability Perspective</a>.</p>
<h2 id="codeline-organization">Codeline Organization</h2>
<p>In this section we will give a brief overview of the source code structure of Node.js, also called codeline organization. A well-defined codeline organization allows for automated builds, tests and releases. This has the potential of greatly simplifying the development process. The structure of Node.js&apos; code is as follows:</p>
<table>
<thead>
<tr>
<th>Directory</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>benchmark</td>
<td>This directory contains the code and data for benchmarking and measuring the performance of different Node.js implementations. The benchmarks are classified into 25 directories depending on the subsystem they benchmark. It also includes a miscellaneous directory for benchmarks that do not clearly fit in one of the predefined categories.</td>
</tr>
<tr>
<td>deps</td>
<td>This directory contains the source code of the third party components that Node.js depends on, some of which are shown in <a href="#module_organization">Figure 4</a>.</td>
</tr>
<tr>
<td>doc</td>
<td>This directory contains all the documentation for Node.js, such as API explanations, changelogs, development guides, etc.</td>
</tr>
<tr>
<td>lib</td>
<td>This directory contains the JavaScript modules used in Node.js. The modules in lib/internal are meant for use in Node.js core and are not meant to be accessed from user modules.</td>
</tr>
<tr>
<td>src</td>
<td>This directory contains the bindings that expose the C/C++ libraries to JavaScript.</td>
</tr>
<tr>
<td>test</td>
<td>This directory consists of the code used to test Node.js. The <code>common.js</code> module in this folder contains a number of helper functions for commonly occurring tasks in tests.</td>
</tr>
<tr>
<td>tools</td>
<td>This directory contains additional tools that are useful for development with Node.js, like build functionality, automated testing libraries, etc.</td>
</tr>
</tbody>
</table>
<div id="section-functional-view">

<h1 id="functional-view">Functional View</h1>
<p>In this section we will describe the most important and unique functionalities of Node.js. We will also address the architectural elements and choices that make these functions possible. Node.js indirectly offers vast amounts of functionality through the myriad of applications that have been built upon it, such as chat bots, application monitoring and data streaming. However, since our focus is on Node.js itself we are mainly interested in its architecture and will therefore also focus solely on the functionalities offered directly to developers working with Node.js.</p>
<h2 id="threading">Threading</h2>
<p>The threading mechanism of Node.js is quite different from other webservers. For example, webservers based on PHP and ASP.NET typically create a new thread for each client request. That client request thus causes the entire program to be reinstantiated on the thread for that specific request. So while the webserver is definitely multi-threaded, each program instance served to a client operates only on a single thread.</p>
<p>As we mentioned in the <a href="#section-development-view">Development View</a>, Node.js is built upon <a href="https://github.com/libuv/libuv" target="_blank">libuv</a>, which allows it to perform asynchronous or non-blocking I/O operations. Because of this, Node.js is able to use only a single &quot;calling thread&quot; that serves all incoming client requests without causing independent requests to block each other. Any work that needs to be done is passed off to a thread pool where it is assigned to a separate thread on which it will be executed. After the work has been done, control is ceded back to the calling thread to provide the client with the appropriate response to their original request [<a href="#codingeek">9</a>]. </p>
<p>In a later section on the <a href="#section-performance-perspective">Performance &amp; Stability Perspective</a> we will discuss the advantages and disadvantages that these two approaches carry with them. For now it suffices to emphasize the differences from an architectural point of view. We will now elaborate on the calling thread, commonly referred to as the event loop.</p>
<h2 id="event-loop">Event Loop</h2>
<p>As we previously discussed in the Development View, Node.js is based on the event-driven programming paradigm [<a href="#nodesource">10</a>]. This becomes clear through the so-called event loop, a process that is constantly accepting incoming requests and providing responses to previously accepted requests. In between accepting a request and responding to it, the event loop will refer work that needs to be done to one of the background workers, as mentioned in the previous subsection on Threading. Node.js makes good use of JavaScript&apos;s support for callbacks by allowing a callback to be sent along with each such task. <a href="#EventLoop1">Figure 5</a> pictures the execution model as we have discussed it so far.</p>
<div id="EventLoop1">

<p><img src="images-node/NodeThreads.png" alt="" title="Figure 5: NodeJS Execution Model"> <br>
<em>Figure 5: NodeJS Execution Model</em> (from <a href="http://www.codingeek.com/tutorials/nodejs/is-nodejs-single-threaded/" target="_blank">http://www.codingeek.com/tutorials/nodejs/is-nodejs-single-threaded/</a>)</p>
<p>Each of these callbacks is registered to an Event Queue, where it waits to be called as soon as the corresponding task has been finished. These callbacks are all executed on the main thread again, as they are responsible for providing the client with a response. Therefore it is advisable to keep the callback functions as lightweight as possible, as they will cause delay for other simultaneous requests. As long as there are callbacks in this queue, the event loop will remain active to respond to all outstanding client requests. <a href="#Event_Loop">Figure 6</a> shows the interplay between the mechanisms behind the Event Queue, the event loop and the thread pool.</p>
<div id="Event_Loop">

<p><img src="images-node/nodejs-event-loop.png" alt="" title="Figure 6: Single Threaded event loop model"> <br>
<em>Figure 6: Single Threaded event loop model</em> (from <a href="http://www.journaldev.com/7462/node-js-architecture-single-threaded-event-loop" target="_blank">http://www.journaldev.com/7462/node-js-architecture-single-threaded-event-loop</a>)</p>
<p>In Node.js every object that can fire events is an instance of the <code>EventEmitter</code> class. Each of these objects has an <code>on()</code> method in which a type of event can be specified along with the appropriate callback such that each time the named event is fired, the corresponding callback is called. If multiple callbacks have been assigned to the same event, all of them will be executed in a synchronous manner (according to the first in, first out principle). If necessary developers can override this procedure by using the <code>setImmediate()</code> method for a callback to switch to an asynchronous model.</p>
<p>Some of the core modules of Node.js that extend the <code>EventEmitter</code> class are the <code>Server</code>, <code>Socket</code>, <code>http</code> and <code>fs</code> (short for File System) modules. For all of these it is easy to imagine how the event-based way of programming enables the system as a whole to function in a non-blocking way. Without events, the program would have to postpone executing any of its subsequent code until it has received a response from a remote server or until a file has been read completely. By specifying callbacks for such events, the main program can continue being executed, only returning to the callback when new data has become available.</p>
<h2 id="package-management">Package Management</h2>
<p>Node.js uses a package manager in order for developers to add modules to their applications. These modules add new functionality to existing applications. This new functionality can help developers create their app or enhance their app for the users.<br>
Although most packages are modules, there are some packages that are not modules for they have no index.js or main field in the package.json file for use in Node.js programs[<a href="#npmweb">11</a>]. This way the Node.js program cannot use the <code>require</code> function to load the package and is thus not a module.</p>
<h3 id="npm">npm</h3>
<p>When installing node, the package manager called <em>npm</em> is automatically installed as well. npm is written in JavaScript and was developed by Isaac Z. Schlueter. He saw that module packaging was not done well in node compared to other platforms. This was the reason for him to come up with npm[<a href="#npmwiki">12</a>]. npm makes it easy for developers to share, reuse and update shared JavaScript code and uses nested dependencies as shown in <a href="#nesteddependencies">Figure 7</a><br></p>
<div id="nesteddependencies">

<p><img src="images-node/nested_dependencies.png" alt="" title="Figure 7: npm nested dependicies"> <br>
<em>Figure 7: npm nested dependicies</em> (from <a href="https://maxogden.com/nested-dependencies.html" target="_blank">https://maxogden.com/nested-dependencies.html</a>)</p>
<p>npm comes with a command line client that interacts with a remote registry. The <a href="https://en.wikipedia.org/wiki/CommonJS" target="_blank">CommonJS</a> format is used for the packages on the registry along with a metadata file, package.json. There is no screening for the packages on the registry, so anyone can upload their package. Because of this, the quality of packages is very diverse. Some security risks are present because of this rule. Although the npm server admins can delete malicious packages, deleting packages may cause failure of applications using those packages.<br>
npm can also be used for managing applications locally. By defining a package.json file for a node application, dependencies can be automatically downloaded and updated by using npm. Even versions can be set for packages, if an application only works with a certain version, so that npm will not update that package and only installs that version of the package.</p>
<h3 id="other-package-managers">Other package managers</h3>
<p>Next to npm there are other third-party package managers that can be used with node. Yarn for example is package manager that was released by Facebook. All these package managers use the npm public registry, but are different in the client-side experience.  </p>
<div id="section-performance-perspective">

<h1 id="performance-and-scalability-perspective">Performance and Scalability Perspective</h1>
<p>This section provides a detailed view on how the architecture of Node.js enables the development of highly scalable server-side web applications.
In order to understand how Node.js achieves scalability, it is first necessary to understand the drawbacks of traditional web server architectures when handling a large number of concurrent requests that are I/O or network intensive. Ryan Dahl, the creator of Node.js provides an insight into the design limitations of traditional web server frameworks.</p>
<pre><code class="lang-txt"> &quot;Turns out, a lot of the frameworks were designed in a way that they made the assumption a
  request &#x2014; response is something that happens instantaneously and that your entire web
  development experience should be abstracted as a function. You get a request, you return a
  response. That is the extent of your context.&quot;&#x2014; Ryan Dahl
</code></pre>
<p>As we pointed out in the previous section, this type of request/response architecture uses multi-threading to provide concurrent handling of requests. However, since a new thread is created for each request and because of the use of blocking I/O calls, such an architecture cannot scale up efficiently. The sections below discuss how the event-driven architecture of Node.js differs from this traditional approach with respect to performance and scalability.</p>
<h2 id="multi-threaded-requestresponse-model-with-blocking-io">Multi-Threaded Request/Response Model with Blocking I/O</h2>
<p><a href="#SynchronousIO">Figure 8</a> shows the request processing mechanism in web servers with multi-threaded synchronous I/O model. Here, a new thread is created for each incoming request at the server. The thread blocks when I/O operations are being executed. Though this type of thread-per-request model provides concurrent handling of requests, it is evident from <a href="#SynchronousIO">Figure 8</a> that a large amount of memory and CPU is tied-up without use when the thread blocks while waiting for I/O or network calls to return. Also, as the number of concurrent requests increases, the overhead of thread management becomes high.</p>
<div id="SynchronousIO">

<p><img src="images-node/SynIO.png" alt="" title="Figure 8: Synchronous I/O"> <br>
<em>Figure 8: Synchronous I/O (from <a href="http://bijoor.me/2013/06/09/java-ee-threads-vs-node-js-which-is-better-for-concurrent-data-processing-operations/" target="_blank">http://bijoor.me/2013/06/09/java-ee-threads-vs-node-js-which-is-better-for-concurrent-data-processing-operations/</a>)</em></p>
<h2 id="single-threaded-asynchronous-io-model">Single Threaded Asynchronous I/O Model</h2>
<p><a href="#AsynchronousIO">Figure 9</a> shows the request processing mechanism in web servers which run a single thread and perform non-blocking I/O calls. Node.js uses a similar concurrency model which makes it more scalable than the multi-threaded model. This model uses a single thread which services all the incoming requests at the web server. The I/O operations are executed as events and do not block the calling thread. It is clear from <a href="#AsynchronousIO">Figure 9</a> that this model utilizes the CPU more efficiently than the multi-threaded model. Also, since it uses a single thread, it is more memory efficient compared to the multi-threaded model.</p>
<div id="AsynchronousIO">

<p><img src="images-node/ASynIO.png" alt="" title="Figure 9: Asynchronous I/O"> <br>
<em>Figure 9: Asynchronous I/O (from <a href="http://bijoor.me/2013/06/09/java-ee-threads-vs-node-js-which-is-better-for-concurrent-data-processing-operations/" target="_blank">http://bijoor.me/2013/06/09/java-ee-threads-vs-node-js-which-is-better-for-concurrent-data-processing-operations/</a>)</em></p>
<p>At the backend however, threads are still required to execute the various I/O operations in parallel. But this complexity is hidden away from the Node.js application which makes programming on Node.js much easier. Also, since this model moves away from the thread-per-request architecture, it does not incur the overhead of thread management.</p>
<p>Despite its superior concurrency model, the Node.js architecture is not suitable to scale across multiple cores in a system. Since Node.js uses a single thread to service all incoming requests, it cannot leverage multiple cores in the system by distributing the load across cores. Listed below are two mechanisms to overcome this.</p>
<ul>
<li><p>Node.js provides the <a href="https://nodejs.org/api/cluster.html#cluster_how_it_works" target="_blank">Cluster API</a>  which applications can use to distribute incoming connections across worker processes which run on multiple cores.</p>
</li>
<li><p>The libuv library which manages the threads in Node.js by default creates 4 threads in the thread pool when the node process starts running. The <code>UV_THREADPOOL_SIZE</code> environment variable can be configured to create a maximum of 128 threads which are distributed across cores by the server operating system.</p>
</li>
</ul>
<div id="section-conclusion">

<h1 id="conclusion">Conclusion</h1>
<p>In this chapter we have analyzed the architecture of Node.js on different perspectives and views, so that the readers could have a broad idea of what Node.js is and what is it&apos;s structure.</p>
<p>As aspiring software architects, analyzing Node.js structure has been enlightening experience for us. It has provided useful insight as to how complex modular architectures are developed and managed, and the reasons for doing so. We appreciated the opportunity to analyze the various architectural aspects of Node.js which allowed us to become intimately familiar with a project we had all heard of but had never really figured out completely. From the stakeholders and the ecosystem in which Node.js resides to the more technical aspects dealing with the software development process, the functionalities and the scalability.</p>
<div id="section-references">

<h1 id="references">References</h1>
<ol>
<li><div id="rdquote">Dahl, R (2010-11-09). &quot;Joyent and Node&quot;. Google Groups., <a href="https://groups.google.com/forum/#!topic/nodejs/lWo0MbHZ6Tc" target="_blank">https://groups.google.com/forum/#!topic/nodejs/lWo0MbHZ6Tc</a>, Accessed on April 3rd, 2017</div></li>
<li><div id="rdvideo">Video: Ryan Dahl: Original Node.js presentation (November 26th, 2009), <a href="https://www.youtube.com/watch?v=ztspvPYybIY" target="_blank">https://www.youtube.com/watch?v=ztspvPYybIY</a>, Accessed on April 3rd, 2017.</div></li>
<li><div id="nodestats">Node By Numbers (January 1st, 2017), <a href="https://nodesource.com/node-by-numbers" target="_blank">https://nodesource.com/node-by-numbers</a>, Accessed on April 3rd, 2017.</div></li>
<li><div id="rw">Nick Rozanski and Eoin Woods. Software Systems Architecture: Working with Stakeholders using Viewpoints and Perspectives. Addison-Wesley, 2012.</div></li>
<li><div id="archint"> Li, A. (June 5th, 2016), Architecture of Node.js&#x2019; Internal Codebase, <em>Yet Another Node.js Blog</em>, <a href="https://arenli.com/architecture-of-node-js-internal-codebase-57cd8376b71f" target="_blank">https://arenli.com/architecture-of-node-js-internal-codebase-57cd8376b71f</a>, Accessed on February 25th, 2017</div></li>
<li><div id="enterprise"> Delgado, A. (October 5th, 2017), Top 5 companies using NodeJS in production, <a href="https://www.linkedin.com/pulse/top-5-companies-using-nodejs-production-anthony-delgado" target="_blank">https://www.linkedin.com/pulse/top-5-companies-using-nodejs-production-anthony-delgado</a>, Accessed on February 26th, 2017</div></li>
<li><div id="mo">Node.js Foundation (2017), Development | Node.js, <a href="https://nodejs.org/en/get-involved/development/#stability-policy" target="_blank">https://nodejs.org/en/get-involved/development/#stability-policy</a>, Accessed on March 6th, 2017</div></li>
<li><div id="abi">Krill, P. (November 29th, 2017), Node.js update makes JavaScript VMs future-proof, <a href="http://www.infoworld.com/article/3145428/javascript/node-js-making-strides-in-javascript-vm-independence.html" target="_blank">http://www.infoworld.com/article/3145428/javascript/node-js-making-strides-in-javascript-vm-independence.html</a>, Accessed on March 6th, 2017</div></li>
<li><div id="codingeek">Rahul, G. (October 27th, 2017), Is NodeJS single threaded - Let&apos;s find out, <a href="http://www.codingeek.com/tutorials/nodejs/is-nodejs-single-threaded/" target="_blank">http://www.codingeek.com/tutorials/nodejs/is-nodejs-single-threaded/</a>, Accessed on April 2nd, 2017</div></li>
<li><div id="nodesource">Norris, T. (January 5th, 2017), The Nodesource Blog, <a href="https://nodesource.com/blog/understanding-the-nodejs-event-loop/" target="_blank">https://nodesource.com/blog/understanding-the-nodejs-event-loop/</a>, Accessed on April 2nd, 2017</div></li>
<li><div id="npmweb">Packages and Modules, <a href="https://docs.npmjs.com/how-npm-works/packages" target="_blank">https://docs.npmjs.com/how-npm-works/packages</a>, Accessed on April 2nd, 2017</div></li>
<li><div id="npmwiki">npm (software), <a href="https://en.wikipedia.org/wiki/Npm_(software" target="_blank">https://en.wikipedia.org/wiki/Npm_(software</a>), Accessed on April 2nd, 2017 </div></li>
</ol>
</div></div></div></div></div></div></div></div></div></div></div></div></div></div></div></div></div>
                                
                                </section>
