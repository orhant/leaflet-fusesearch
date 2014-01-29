<h1>leaflet-fusesearch</h1>

Search features in a GeoJSON layer using the lightweight JavaScript fuzzy search <a href="https://github.com/krisk/Fuse">Fuse.js</a>

<h2>Usage</h2>

First download Fuse.js from <a href="https://github.com/krisk/Fuse">this repo<a/> or 
from <a href="http://kiro.me/projects/fuse.html">Kiro's site</a>, and load it in your page before <code>leaflet-fusesearch.js</code>.<br/>
<br/>
Create the control L.Control.FuseSearch and add it to the Map.<br/>
<pre>
    var searchCtrl = L.control.fuseSearch()
    searchCtrl.addTo(map);
</pre>

Then load your GeoJSON layer and index the features, choosing the properties you want to index.
<br/>
<pre>
    searchCtrl.indexFeatures(features, ['name', 'company', 'details'];
</pre>

That's it !  By default the search control will appear on the top right corner of the map.
This opens the search pane on the same side where you can type the search string.
Up to 10 features are listed, with the indexed properties displayed. 
If a pop-up is associated with the feature the user can click on it and the pop-up is displayed.

<h2>Options</h2>

The FuseSearch control can be created with the following options :
<ul>
<li><code>position</code> : position of the control, the search pane shows on the matching side. Default <code>'topright'</code>.</li>
<li><code>maxResultLength</code> : number of features displayed in the result list, default 10.</li>
<li><code>showResultFct</code> : function to display a feature returned by the search, parameters are the feature and an HTML container. Here is an example :</li>
</ul>
<pre>
        showResultFct: function(feature, container) {
            props = feature.properties;
            var name = L.DomUtil.create('b', null, container);
            name.innerHTML = props.name;
            container.appendChild(L.DomUtil.create('br', null, container));
            container.appendChild(document.createTextNode(props.details));
        }
</pre>

In addition these options are directly passed to Fuse - more details on <a href="http://kiro.me/projects/fuse.html">Fuse.js</a> :
<ul>
<li><code>caseSensitive</code> : whether comparisons should be case sensitive, default is false.</li>
<li><code>threshold</code> : a decimal value indicating at which point the match algorithm gives up. 
A threshold of 0.0 requires a perfect match, a threshold of 1.0 would match anything.</li>
</ul>

<h2>Example</h2>

I'm currently working on providing a simple example, for now have a look at <a href="http://www.naomap.fr">my NaoMap site</a>.
