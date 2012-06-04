<h1>Welcome to <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a></h1><br><div class='tw-tiddler-frame' data-tiddler-target='HelloThere' data-tiddler-template='HelloThere'>Welcome to <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a>, a reboot of <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlyWiki'>TiddlyWiki</a>, the venerable, reusable non-linear personal web notebook first released in 2004. It is a complete interactive wiki that can run from a single HTML file in the browser or as a powerful <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='What%20is%20node.js%3F'>node.js application</a>.<br><br><a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a> is currently at version 5.0.0.a2 and is under active development, which is to say that it is useful but incomplete. You can try out the online prototype at <a class='tw-tiddlylink tw-tiddlylink-external' href='http://tiddlywiki.com/tiddlywiki5'>http://tiddlywiki.com/tiddlywiki5</a>, <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TryingOutTiddlyWiki'>try out the command line incarnation</a>, get involved in the <a class='tw-tiddlylink tw-tiddlylink-external' href='https://github.com/Jermolene/TiddlyWiki5'>development on GitHub</a> or join the discussions on <a class='tw-tiddlylink tw-tiddlylink-external' href='http://groups.google.com/group/TiddlyWikiDev'>the TiddlyWikiDev Google Group</a>.</div><br><br><h1>Usage</h1><br><div class='tw-tiddler-frame' data-tiddler-target='CommandLineInterface' data-tiddler-template='CommandLineInterface'><a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a> can be used on the command line to perform an extensive set of operations based on tiddlers, <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlerFiles'>TiddlerFiles</a> and <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWikiFiles'>TiddlyWikiFiles</a>. For example, this loads the tiddlers from a <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlyWiki'>TiddlyWiki</a> HTML file and then saves one of them in HTML:<br><br><pre>node core/boot.js --verbose --load mywiki.html --savetiddler ReadMe ./readme.html
</pre><h2>Usage</h2><br>Running <code>boot.js</code> from the command line boots the <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlyWiki'>TiddlyWiki</a> kernel, loads the core plugins and establishes an empty wiki store. It then sequentially processes the command line arguments from left to right. The arguments are separated with spaces. The commands are identified by the prefix <code>--</code>.<br><br><pre>node core/boot.js [--&lt;option&gt; [&lt;arg&gt;[,&lt;arg&gt;]]]
</pre><br><h2>Commands</h2><br>The following commands are available.<br><br><h3> load</h3><br>Load tiddlers from 2.x.x <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlyWiki'>TiddlyWiki</a> files (<code>.html</code>), <code>.tiddler</code>, <code>.tid</code>, <code>.json</code> or other files <br><br><pre>--load &lt;filepath&gt;
</pre><br><h3> savetiddler</h3><br>Save an individual tiddler as a specified MIME type, defaults to <code>text/html</code> <br><br><pre>--savetiddler &lt;title&gt; &lt;filename&gt; [&lt;type&gt;]
</pre><br><h3> wikitest</h3><br>Run wikification tests against the tiddlers in the given directory. Include the <code>save</code> flag to save the test result files as the new targets.<br><br><pre>--wikitest &lt;dir&gt; [save]
</pre><br><code>--wikitest</code> looks for <code>*.tid</code> files in the specified folder. It then wikifies the tiddlers to both &quot;text/plain&quot; and &quot;text/html&quot; format and checks the results against the content of the <code>*.html</code> and <code>*.txt</code> files in the same directory.<br><br><h3> server</h3><br>The server is very simple. At the root, it serves a rendering of a specified tiddler. Away from the root, it serves individual tiddlers encoded in JSON, and supports the basic HTTP operations for <code>GET</code>, <code>PUT</code> and <code>DELETE</code>.<br><br><pre>--server &lt;port&gt; &lt;roottiddler&gt; &lt;rendertype&gt; &lt;servetype&gt;
</pre><br>For example:<br><br><pre>--server 8080 $:/core/tiddlywiki5.template.html text/plain text/html
</pre><br>The parameters are:<br><br><pre>--server &lt;port&gt; &lt;roottiddler&gt; &lt;rendertype&gt; &lt;servetype&gt;
</pre><br><ul><li> <strong>port</strong> - port number to serve from (defaults to &quot;8080&quot;)</li><li> <strong>roottiddler</strong> - the tiddler to serve at the root (defaults to &quot;$:/core/tiddlywiki5.template.html&quot;) </li><li> <strong>rendertype</strong> - the content type to which the root tiddler should be rendered (defaults to &quot;text/plain&quot;)</li><li> <strong>servetype</strong> - the content type with which the root tiddler should be served (defaults to &quot;text/html&quot;)</li></ul><br><h3> dump tiddlers</h3><br>Dump the titles of the tiddlers in the wiki store <br><br><pre>--dump tiddlers
</pre><br><h3> dump tiddler</h3><br>Dump the fields of an individual tiddler <br><br><pre>--dump tiddler &lt;title&gt;
</pre><br><h3> dump shadows</h3><br>Dump the titles of the shadow tiddlers in the wiki store <br><br><pre>--dump shadows
</pre><br><h3> dump config</h3><br>Dump the current core configuration <br><br><pre>--dump config
</pre><br><h3> verbose</h3><br>Triggers verbose output, useful for debugging <br><br><pre>--verbose
</pre></div><br><br><h1>Architecture</h1><br><div class='tw-tiddler-frame' data-tiddler-target='TiddlyWikiArchitecture' data-tiddler-template='TiddlyWikiArchitecture'><h2> Overview</h2><br>The heart of <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlyWiki'>TiddlyWiki</a> can be seen as an extensible representation transformation engine. Given the text of a tiddler and its associated MIME type, the engine can produce a rendering of the tiddler in a new MIME type. Furthermore, it can efficiently selectively update the rendering to track any changes in the tiddler or its dependents.<br><br>The most important transformations are from <code>text/x-tiddlywiki</code> wikitext into <code>text/html</code> or <code>text/plain</code> but the engine is used throughout the system for other transformations, such as converting images for display in HTML, sanitising fragments of <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='JavaScript'>JavaScript</a>, and processing CSS.<br><br>The key feature of wikitext is the ability to include one tiddler within another (usually referred to as <em>transclusion</em>). For example, one could have a tiddler called <em>Disclaimer</em> that contains the boilerplate of a legal disclaimer, and then include it within lots of different tiddlers with the macro call <code>&lt;&lt;tiddler Disclaimer&gt;&gt;</code>. This simple feature brings great power in terms of encapsulating and reusing content, and evolving a clean, usable implementation architecture to support it efficiently is a key objective of the <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a> design.<br><br>It turns out that the transclusion capability combined with the selective refreshing mechanism provides a good foundation for building <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlyWiki'>TiddlyWiki</a>'s user interface itself. Consider, for example, the <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='StoryMacro'>StoryMacro</a> in its simplest form:<br><br><pre>&lt;&lt;story story:MyStoryTiddler&gt;&gt;
</pre><br>The story macro looks for a list of tiddler titles in the tiddler <code>MyStoryTiddler</code>, and displays them in sequence. The subtle part is that subsequently, if <code>MyStoryTiddler</code> changes, the <code>&lt;&lt;story&gt;&gt;</code> macro is selectively re-rendered. So, to navigate to a new tiddler, code merely needs to add the name of the tiddler and a line break to the top of <code>MyStoryTiddler</code>:<br><br><pre>var storyTiddler = store.getTiddler(&quot;MyStoryTiddler&quot;);
store.addTiddler(new Tiddler(storyTiddler,{text: navigateTo + &quot;\n&quot; + storyTiddler.text}));
</pre><br>The mechanisms that allow all of this to work are fairly intricate. The sections below progressively build the key architectural concepts of <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a> in a way that should provide a good basis for exploring the code directly.<br><br><h2> Tiddlers</h2><br>Tiddlers are an immutable dictionary of name:value pairs called fields.<br><br>The only field that is required is the <code>title</code> field, but useful tiddlers also have a <code>text</code> field, and some or all of the standard fields <code>modified</code>, <code>modifier</code>, <code>created</code>, <code>creator</code>, <code>tags</code> and <code>type</code>.<br><br>Hardcoded in the system is the knowledge that the <code>tags</code> field is a string array, and that the <code>modified</code> and <code>created</code> fields are <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='JavaScript'>JavaScript</a> <code>Date</code> objects. All other fields are strings.<br><br>The <code>type</code> field identifies the representation of the tiddler text with a MIME type.<br><br><h2> WikiStore</h2><br>Groups of uniquely titled tiddlers are contained in <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiStore'>WikiStore</a> objects.<br><br>The <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiStore'>WikiStore</a> also manages the plugin modules used for macros, and operations like serializing, deserializing, parsing and rendering tiddlers.<br><br>Each <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiStore'>WikiStore</a> is connected to another shadow store that is used to provide default content. Under usual circumstances, when an attempt is made to retrieve a tiddler that doesn't exist in the store, the search continues into its shadow store (and so on, if the shadow store itself has a shadow store).<br><br><h2> WikiStore Events</h2><br>Clients can register event handlers with the <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiStore'>WikiStore</a> object. Event handlers can be registered to be triggered for modifications to any tiddler in the store, or with a filter to only be invoked when a particular tiddler or set of tiddlers changes.<br><br>Whenever a change is made to a tiddler, the wikistore registers a <code>nexttick</code> handler (if it hasn't already done so). The <code>nexttick</code> handler looks back at all the tiddler changes, and dispatches any matching event handlers. <br><br><h2> Parsing and Rendering</h2><br><a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlyWiki'>TiddlyWiki</a> parses the content of tiddlers to build an internal tree representation that is used for several purposes:<br><br><ul><li> Rendering a tiddler to other formats (e.g. converting wikitext to HTML)</li><li> Detecting outgoing links from a tiddler, and from them...</li><li> ...computing incoming links to a tiddler</li><li> Detecting tiddlers that are orphans with no incoming links</li><li> Detecting tiddlers that are referred to but missing</li></ul><br>The parse tree is built when needed, and then cached by the <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiStore'>WikiStore</a> until the tiddler changes.<br><br><a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a> uses multiple parsers:<br><br><ul><li> Wikitext (<code>text/x-tiddlywiki</code>) in <code>js/WikiTextParser.js</code></li><li> <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='JavaScript'>JavaScript</a> (<code>text/javascript</code>) in <code>js/JavaScriptParser.js</code></li><li> Images (<code>image/png</code> and <code>image/jpg</code>) in <code>js/ImageParser.js</code></li><li> JSON (<code>application/json</code>) in <code>js/JSONParser.js</code></li></ul>Additional parsers are planned:<br><ul><li> CSS (<code>text/css</code>)</li><li> Recipe (<code>text/x-tiddlywiki-recipe</code>)</li></ul><br>One global instance of each parser is instantiated in <code>js/App.js</code> and registered with the main <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiStore'>WikiStore</a> object.<br><br>The parsers are all used the same way:<br><br><pre class='javascript-source'><span class='javascript-keyword'>var</span> <span class='javascript-identifier'>parseTree</span> <span class='javascript-punctuator'>=</span> <span class='javascript-identifier'>parser</span><span class='javascript-punctuator'>.</span><span class='javascript-identifier'>parse</span><span class='javascript-punctuator'>(</span><span class='javascript-identifier'>type</span><span class='javascript-punctuator'>,</span><span class='javascript-identifier'>text</span><span class='javascript-punctuator'>)</span> <span class='javascript-comment javascript-line-comment'>// Parses the text and returns a parse tree object<br>
</span></pre><br>The parse tree object exposes the following fields:<br><br><pre class='javascript-source'><span class='javascript-keyword'>var</span> <span class='javascript-identifier'>renderer</span> <span class='javascript-punctuator'>=</span> <span class='javascript-identifier'>parseTree</span><span class='javascript-punctuator'>.</span><span class='javascript-identifier'>compile</span><span class='javascript-punctuator'>(</span><span class='javascript-identifier'>type</span><span class='javascript-punctuator'>)</span><span class='javascript-punctuator'>;</span> <span class='javascript-comment javascript-line-comment'>// Compiles the parse tree into a renderer for the specified MIME type
</span><span class='javascript-identifier'>console</span><span class='javascript-punctuator'>.</span><span class='javascript-identifier'>log</span><span class='javascript-punctuator'>(</span><span class='javascript-identifier'>parseTree</span><span class='javascript-punctuator'>.</span><span class='javascript-identifier'>toString</span><span class='javascript-punctuator'>(</span><span class='javascript-identifier'>type</span><span class='javascript-punctuator'>)</span><span class='javascript-punctuator'>)</span><span class='javascript-punctuator'>;</span> <span class='javascript-comment javascript-line-comment'>// Returns a readable string representation of the parse tree (either <code>text/html</code> or <code>text/plain</code>)
</span><span class='javascript-keyword'>var</span> <span class='javascript-identifier'>dependencies</span> <span class='javascript-punctuator'>=</span> <span class='javascript-identifier'>parseTree</span><span class='javascript-punctuator'>.</span><span class='javascript-identifier'>dependencies</span><span class='javascript-punctuator'>;</span> <span class='javascript-comment javascript-line-comment'>// Gets the dependencies of the parse tree (see below)<br>
</span></pre><br>The dependencies are returned as an object like this:<br><br><pre>{
	tiddlers: {&quot;tiddlertitle1&quot;: true, &quot;tiddlertitle2&quot;: false},
	dependentAll: false
}
</pre><br>The <code>tiddlers</code> field is a hashmap of the title of each tiddler that is linked or included in the current one. The value is <code>true</code> if the tiddler is a <em>'fat'</em> dependency (ie the text is included in some way) or <code>false</code> if the tiddler is a <em><code>skinny</code></em> dependency.<br><br>The <code>dependentAll</code> field is used to indicate that the tiddler contains a macro that scans the entire pool of tiddlers (for example the <code>&lt;&lt;list&gt;&gt;</code> macro), and is potentially dependent on any of them. The effect is that the tiddler should be rerendered whenever any other tiddler changes.<br><br><h2> Rendering</h2><br>The <code>parseTree.compile(type)</code> method returns a renderer object that contains a <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='JavaScript'>JavaScript</a> function that generates the new representation of the original parsed text.<br><br>The renderer is invoked as follows:<br><br><pre class='javascript-source'><span class='javascript-keyword'>var</span> <span class='javascript-identifier'>renderer</span> <span class='javascript-punctuator'>=</span> <span class='javascript-identifier'>parseTree</span><span class='javascript-punctuator'>.</span><span class='javascript-identifier'>compile</span><span class='javascript-punctuator'>(</span><span class='javascript-string'>&quot;text/html&quot;</span><span class='javascript-punctuator'>)</span><span class='javascript-punctuator'>;</span>
<span class='javascript-keyword'>var</span> <span class='javascript-identifier'>html</span> <span class='javascript-punctuator'>=</span> <span class='javascript-identifier'>renderer</span><span class='javascript-punctuator'>.</span><span class='javascript-identifier'>render</span><span class='javascript-punctuator'>(</span><span class='javascript-identifier'>tiddler</span><span class='javascript-punctuator'>,</span><span class='javascript-identifier'>store</span><span class='javascript-punctuator'>)</span><span class='javascript-punctuator'>;</span>
</pre><br>The <code>tiddler</code> parameter to the <code>render</code> method identifies the tiddler that is acting as the context for this rendering &mdash; for example, it provides the fields displayed by the <code>&lt;&lt;view&gt;&gt;</code> macro. The <code>store</code> parameter is used to resolve any references to other tiddlers.<br><br><h2> Rerendering</h2><br>When rendering to the HTML/SVG DOM in the browser, <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a> also allows a previous rendering to be selectively updated in response to changes in dependent tiddlers. At the moment, only the <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiTextRenderer'>WikiTextRenderer</a> supports rerendering.<br><br>The rerender method on the renderer is called as follows:<br><br><pre>var node = document.getElementById(&quot;myNode&quot;);
var renderer = parseTree.compile(&quot;text/html&quot;);
myNode.innerHTML = renderer.render(tiddler,store);
// And then, later:
renderer.rerender(node,changes,tiddler,store,renderStep);
</pre><br>The parameters to <code>rerender()</code> are:<br><br><table class='table'><tbody><tr class='evenRow'><th align='left'>Name</th><th align='left'>Description</th></tr><tr class='oddRow'><td align='left'>node</td><td align='left'>A reference to the DOM node containing the rendering to be rerendered</td></tr><tr class='evenRow'><td align='left'>changes</td><td align='left'>A hashmap of <code>{title: &quot;created|modified|deleted&quot;}</code> indicating which tiddlers have changed since the original rendering</td></tr><tr class='oddRow'><td align='left'>tiddler</td><td align='left'>The tiddler providing the rendering context</td></tr><tr class='evenRow'><td align='left'>store</td><td align='left'>The store to use for resolving references to other tiddlers</td></tr><tr class='oddRow'><td align='left'>renderStep</td><td align='left'>See below</td></tr></tbody></table><br>Currently, the only macro that supports rerendering is the <code>&lt;&lt;story&gt;&gt;</code> macro; all other macros are rerendered by calling the ordinary <code>render()</code> method again. The reason that the <code>&lt;&lt;story&gt;&gt;</code> macro goes to the trouble of having a <code>rerender()</code> method is so that it can be carefully selective about not disturbing tiddlers in the DOM that aren't affected by the change. If there were, for instance, a video playing in one of the open tiddlers it would be reset to the beginning if the tiddler were rerendered.<br></div><br><br><h1>Plugin Mechanism</h1><br><div class='tw-tiddler-frame' data-tiddler-target='PluginMechanism' data-tiddler-template='PluginMechanism'><h1>Introduction</h1><br><a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a> is based on a 500 line boot kernel that runs on node.js or in the browser, and everything else is plugins.<br><br>The kernel boots just enough of the <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlyWiki'>TiddlyWiki</a> environment to allow it to load tiddlers as plugins and execute them (a barebones tiddler class, a barebones wiki store class, some utilities etc.). Plugin modules are written like <code>node.js</code> modules; you can use <code>require()</code> to invoke sub components and to control load order.<br><br>There are several different types of plugins: parsers, serializers, deserializers, macros etc. It goes much further than you might expect. For example, individual tiddler fields are plugins, too: there's a plugin that knows how to handle the <code>tags</code> field, and another that knows how to handle the special behaviour of<br>the <code>modified</code> and <code>created</code> fields.<br><br>Some plugins have further sub-plugins: the wikitext parser, for instance, accepts rules as individual plugins.<br><br><h1>Plugins and Modules</h1><br>In <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a>, a plugin is a bundle of related tiddlers that are distributed together as a single unit. Plugins can include tiddlers which are <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='JavaScript'>JavaScript</a> modules. <br><br>The file <code>core/boot.js</code> is a barebones <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlyWiki'>TiddlyWiki</a> kernel that is just sufficient to load the core plugin modules and trigger a startup plugin module to load up the rest of the application.<br><br>The kernel includes:<br><br><ul><li> Eight short shared utility functions</li><li> Three methods implementing the plugin module mechanism</li><li> The <code>$tw.Tiddler</code> class (and three field definition plugins)</li><li> The <code>$tw.Wiki</code> class (and three tiddler deserialization methods)</li><li> Code for the browser to load tiddlers from the HTML DOM</li><li> Code for the server to load tiddlers from the file system</li></ul><br>Each module is an ordinary <code>node.js</code>-style module, using the <code>require()</code> function to access other modules and the <code>exports</code> global to return <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='JavaScript'>JavaScript</a> values. The boot kernel smooths over the differences between <code>node.js</code> and the browser, allowing the same plugin modules to execute in both environments.<br><br>In the browser, <code>core/boot.js</code> is packed into a template HTML file that contains the following elements in order:<br><br><ul><li> Ordinary and shadow tiddlers, packed as HTML <code>&lt;DIV&gt;</code> elements</li><li> <code>core/bootprefix.js</code>, containing a few lines to set up the plugin environment</li><li> Plugin <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='JavaScript'>JavaScript</a> modules, packed as HTML <code>&lt;SCRIPT&gt;</code> blocks</li><li> <code>core/boot.js</code>, containing the boot kernel</li></ul><br>On the server, <code>core/boot.js</code> is executed directly. It uses the <code>node.js</code> local file API to load plugins directly from the file system in the <code>core/modules</code> directory. The code loading is performed synchronously for brevity (and because the system is in any case inherently blocked until plugins are loaded).<br><br>The boot kernel sets up the <code>$tw</code> global variable that is used to store all the state data of the system.<br><br><h1>Core </h1><br>The 'core' is the boot kernel plus the set of plugin modules that it loads. It contains plugins of the following types:<br><br><ul><li> <code>tiddlerfield</code> - defines the characteristics of tiddler fields of a particular name</li><li> <code>tiddlerdeserializer</code> - methods to extract tiddlers from text representations or the DOM</li><li> <code>startup</code> - functions to be called by the kernel after booting</li><li> <code>global</code> - members of the <code>$tw</code> global</li><li> <code>config</code> - values to be merged over the <code>$tw.config</code> global</li><li> <code>utils</code> - general purpose utility functions residing in <code>$tw.utils</code></li><li> <code>tiddlermethod</code> - additional methods for the <code>$tw.Tiddler</code> class</li><li> <code>wikimethod</code> - additional methods for the <code>$tw.Wiki</code> class</li><li> <code>treeutils</code> - static utility methods for parser tree nodes </li><li> <code>treenode</code> - classes of parser tree nodes</li><li> <code>macro</code> - macro definitions</li><li> <code>editor</code> - interactive editors for different types of content</li><li> <code>parser</code> - parsers for different types of content</li><li> <code>wikitextrule</code> - individual rules for the wikitext parser</li><li> <code>command</code> - individual commands for the <code>$tw.Commander</code> class</li></ul><br><a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a> makes extensive use of <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='JavaScript'>JavaScript</a> inheritance:<br><br><ul><li> Tree nodes defined in <code>$:/core/treenodes/</code> all inherit from <code>$:/core/treenodes/node.js</code></li><li> Macros defined in <code>$:/core/macros/</code> all inherit from <code>$:/core/treenodes/macro.js</code></li></ul><br><code>tiddlywiki.plugin</code> files<br></div><br><br><h1>Planned <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiText'>WikiText</a> Features</h1><br><div class='tw-tiddler-frame' data-tiddler-target='NewWikiTextFeatures' data-tiddler-template='NewWikiTextFeatures'>It is proposed to extend the existing <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-resolves' href='TiddlyWiki'>TiddlyWiki</a> <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiText'>WikiText</a> syntax with the following extensions<br><br><ol><li> Addition of <code>**bold**</code> character formatting</li><li> Addition of <code>`backtick for code`</code> character formatting</li><li> Addition of <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiCreole-style'>WikiCreole-style</a> forced line break, e.g. <code>force\\linebreak</code></li><li> Addition of <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiCreole-style'>WikiCreole-style</a> headings, e.g. <code>==Heading</code></li><li> Addition of <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiCreole-style'>WikiCreole-style</a> headings in tables, e.g. <code>|=|=table|=header|</code></li><li> Addition of white-listed HTML and SVG tags intermixed with wikitext</li><li> Addition of <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='WikiCreole-style'>WikiCreole-style</a> pretty links, e.g. <code>[[description -&gt; link]]</code></li><li> Addition of multiline macros, e.g.</li></ol><pre>&lt;&lt;myMacro
param1: Parameter value
param2: value
&quot;unnamed parameter&quot;
param4: ((
A multiline parameter that can go on for as long as it likes
and contain linebreaks.
))
&gt;&gt;
</pre><ol><li> Addition of typed text blocks, e.g.</li></ol><pre>	$$$.js
		return &quot;This will have syntax highlighting applied&quot;
	$$$
</pre></div><br><br><em>This <code>readme</code> file was automatically generated by <a class='tw-tiddlylink tw-tiddlylink-internal tw-tiddlylink-missing' href='TiddlyWiki5'>TiddlyWiki5</a></em><br>